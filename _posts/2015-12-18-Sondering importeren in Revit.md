---
layout: post
title: "Sondering importeren in Revit"
date: 2015-12-18 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "..."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_1_sondering.png'
published: true
---

# Sondering importeren in Revit

Deze week begonnen met Dynamo: Wat een ongekende fantastische mogelijkheden. Van harte aanbevolen voor iedereen.

We maken een stukje dynamoscript om een GEF-bestand in te lezen. Deze is [hier](http://www.3bm.cloud/dutchrevitblog/2ImportGEFFile.zip) te downloaden.(beta)

GEF staat voor Geotechnical Exchange Format en is een bestandsformaat waarin een sondering of grondboring beschreven wordt.

Voor meer informatie over GEF klik [hier](http://www.geonet.nl/upload/documents/dossiers/grondonderzoek/GEF-CPT-Report.pdf). Als je sonderingen laat maken kan de grondmechanisch adviseur ook een GEF-bestand opsturen. Deze kun je weer bekijken met de GEFPlotTool. Deze is te  downloaden op de website van Deltabrain. Klik [hier](http://deltabrain.nl/bouwen/bouwtrillingen/downloads).

![22_1_sondering](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_1_sondering.png)

Hierboven een voorbeeld van een sondering met kleefmeting en waterspanningsmeting bekeken in GEFPlotTool. Links de conusweerstand in MPA met in blauw de waterspanning. Rechts het wrijvingsgetal en er tussenin de plaatselijke wrijving.

![22_2_GEF-bestand](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_2_GEF-bestand.png)

Hierboven is een GEF-bestand te zien geopend in Notepad++. Vanaf #EOH= beginnen eigenlijk een aantal kolommen waar de diepte, sondeerweerstand, plaatselijke wrijving en het wrijvingsgetal weergegeven zijn.

![22_3_overview_dynamocode](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_3_overview_dynamocode.png)

Hierboven de dynamocode om het GEF-bestand naar 3D-grondlagen te vertalen.

![22_4_part_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_4_part_1.png)

**Deel 1.** Hier wordt het GEF-bestand gekozen, vervolgens bekeken, daar gesplitst vanaf #EOH=.
Het laatste deel(List.LastItem) wordt gebruikt om verder te gaan.

![22_4_part_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_4_part_2.png)

**Deel 2:** Eerst wordt de lijst getransponeerd naar 9 lijsten met alle waarden. We hebben 2 kolommen nodig uit deze lijst: Diepte en Wrijvingsgetal. Dit is kolom 0 en 7. Met List.GetItemAtIndex haal je een kolom uit de getransponeerde list.

Om de 'string' naar een number te converteren moet eerst de 'e' opgelost worden. Dynamo lijkt niet te snappen dat dat een wetenschappelijke weergave is. De string wordt in 2 delen gesplitst met separater0='e'. Om vervolgens dit om te zetten naar een number in mm.

![22_4_part_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_4_part_3.png)

We hebben nu een lijst met de wrijvingsgetallen per 2 cm diepte. In de bovenstaande code zit een geneste IF statement waarbij per wrijvingsgetal een grondsoort toegewezen wordt. De gebruikte 'String' wordt tevens de materiaalnaam. Deze moet dus wel aanwezig zijn in het project.

Eigenlijk zou dit deel nog wat uitgebreider moeten: De relatie met de conusweerstand zou ook meegenomen moeten worden. Dit is voor de volgende versie.
Het eindresultaat is een lijst met grondsoorten per 2 cm diepte.

![22_4_part_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_4_part_4.png)

We herhalen het hele verhaal voor de diepte(kolom 0).

![22_4_part_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_4_part_5.png)

Vervolgens hebben we een family gemaakt(zie hieronder). Deze family heeft een afmeting, dikte en materiaal. Met behulp van 'FamilyTypes' en FamilyInstance.ByCoordinates worden ca 1200 families geplaatst met waarvan de coordinaten, dikten en materiaal uit de lijsten komen. Er zitten nog een paar errors in omdat sommige wrijvingsgetallen buiten het bereik vallen.

![22_5_grondsoorten](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_5_grondsoorten.png)

ovenstaand een overzicht van de kleuren en arceringen van de grondsoorten.

![22_6_grondlaagfamily](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_6_grondlaagfamily.png)

Bovenstaand de family die gebruikt is als laag.

![22_7_resultaat](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/22_7_resultaat.png)

En het resultaat in Revit met een funderingspaal erin!

**Er zijn diverse verbeterpunten:**<br>
-1 nieuwe family aanmaken met dynamo in plaats van 1200 families plaatsen in je project.<br>
-Meerdere grondsoorten toevoegen.<br>
-Het script om de sondering in te lezen kan nog beter. Er zijn meerdere mogelijkheden om kolommen te gebruiken. Dit gaat nu nog niet goed met alle soorten GEF-bestanden.<br>
-Grondwaterstand en conusweerstand toevoegen.<br>
-Het geheel in 1 node stoppen en vervolgens een nieuw script maken waar je meerdere sonderingen met RD-coordinaten kan toevoegen. Vervolgens hier met adaptive components een family maken waarin de grondlagen ook echt in diepte verlopen.

Er komt dus nog wel een keer een update. Zijn er mensen die het leuk vinden om mee te doen? Dan kan ik het script posten en met meerdere mensen aan werken.

Het dynamobestand is [hier](http://www.3bm.cloud/dutchrevitblog/2ImportGEFFile.zip) te downloaden.(beta)