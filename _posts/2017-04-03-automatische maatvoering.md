---
layout: post
title: "Automatische maatvoering"
date: 2017-04-03 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "Je kunt met Dynamo ook automatisch maatvoeren."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/Stramienmaatvoering.png'
published: true
---

# Automatische maatvoering

Je kunt met Dynamo ook automatisch maatvoeren.
1) Stramienmaatvoering
2) Funderingsbalkmaatvoering

**1) Stramienmaatvoering**<br>
De stramienmaatvoering is een wat lange routine om uit te leggen.<br>
Onderstaand het overzicht van de routine. Download de bestanden [hier](http://www.3bm.cloud/dutchrevitblog/24Files.zip).

![Stramienmaatvoering](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/Stramienmaatvoering.png)

![24_voor](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/24_voor.png)

![24_na](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/24_na.png)

**2) Funderingsbalkmaatvoering**<br>
Voor de maatvoeringsroutine van de stramienen is de node 'Dimension.ByElements' gebruikt. Je kunt ook een Python Script gebruiken.(met dank aan Revit Experiments)

Onderstaand een eenvoudig voorbeeld.

![Funderingsbalkmaatvoering](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/Funderingsbalkmaatvoering.png)

Een analyse van de code:<br>
**Select Model Elements:** Hier worden de 3D elementen geselecteerd voor het maatvoeren.

**Topology.Faces:** De geselecteerde revit-families worden omgezet naar Dynamo-faces.

**Surface.FilterBYOrientation:** De faces worden gesorteerd op basis van hun oriëntatie. We willen in dit geval alleen een selectie van de vlakken die verticaal staan(en dus haaks op een structural plan)

**Surface.NormalAtParameter:** De vlakken worden omgezet naar een normaalvector.(een vector die haaks op het vlak(de face) staat.

**Vector.IsParallel:** Het codevoorbeeld werkt alleen voor funderingsbalken in y-richting. Daarom zijn we op zoek naar de verticale vlakken waarbij de normaalvector evenwijdig is aan de x-as.

![25_extra](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/25_extra.png)

Als je de node Vector.XAxis vervangt door een vector in een andere richting kun je uiteraard ook in meerdere richtingen maatlijnen plaatsen.

**List.FilterByBoolMask:** De lijst met verticale vlakken wordt gefilterd op basis van de uitkomst van de Vector.IsParallel-node.

**Flatten:** De lijst wordt platgeslagen om de 'niveaus' eruit te halen.

**RevitFaceReference.FromDynamoSurface:** In de code werkten we met DynamoSurfaces. Deze worden omgezet naar RevitFaceReferences zodat de maatlijnen hier aan kunnen blijven 'hangen'.

![python](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/python.png)

De 2e 'Select Model Elements'-node is bedoeld om een lijn haaks op de geselecteerde revit-elementen te selecteren. Dat is de locatie waar de maatvoeringslijn komt te staan.

![24b_voor](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/24b_voor.png)<br>
*Voor*

![24b_na](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-04-03/24b_na.png)<br>
*Na*