---
layout: post
title: "Stramienen in 3D"
date: 2016-02-15 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "Stramienen in 3D in Revit met behulp van Dynamo."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_1.png'
published: true
---

# Stramienen in 3D

Stramienen in 3D in Revit met behulp van Dynamo.

In Revit kun je normaal geen stramienen in 3D laten zien. Onderstaand een stukje dynamocode waarin dit wel mogelijk is.

We gaan er stap voor stap doorheen. Eerst even het resultaat.<br>
De dynamonode is [hier](http://www.3bm.cloud/dutchrevitblog/24_grid3D.zip) te downloaden<br>
Het project met de stramienlijnen en de stramienbolfamily is [hier](http://www.3bm.cloud/dutchrevitblog/24_model.rvt) te downloaden.

![24_grid_3d_revit_dynamo_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_1.png)

De dynamocode kijkt naar de aanwezige stramienen in het project. Er worden modellines geplaatst op de plaats van de grid-curve. Verder wordt er een generic-model geplaatst in de vorm van de stramienbol.

![24_grid_3d_revit_dynamo_7](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_7.png)

Deze family omvat een modelline en een modeltext die doorgelinkt is aan de parameter 'Text'.

![24_grid_3d_revit_dynamo_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_2.png)

Bovenstaand de dynamocode

![24_grid_3d_revit_dynamo_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_3.png)

**1 Categories:** Hier wordt een revit-category geselecteerd. In dit geval 'Grids'<br>
**2 All Elements of Category:** Alle elementen van deze category worden geselecteerd.<br>
**3 Grid.Curve:** Dit is node die van de geselecteerde stramien een 'curve' maakt

![24_grid_3d_revit_dynamo_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_4.png)

Group 4 plaatst de stramienbollen en stelt de parameter 'Text' in overeenkomstig met het stramiennummer.

**4.1 Curve.StartPoint:** Deze node geeft als resultaat de xyz-coördinaat van het begin van de curve.<br>
**4.2 Family Types:** Hier wordt de family uit het project gekozen die geplaatst gaat worden(de stramienbol)<br>
**4.3 FamilyInstance.ByPoint:** Deze node plaatst daadwerkelijk de family op het weergegeven punt.<br>
**4.4 Family.Name:** Deze node selecteerd de familyname van de grids(de familyname van het grid is namelijk het stramiennummer.<br>
**4.5 String:** Dit is de naam van de parameter uit de stramienbolfamily die het stramiennummer moet gaan bevatten.<br>
**4.6 Element.SetParameterByName:** Deze node gaat een bepaalde eigenschap instellen van een aantal families. In dit geval de stramienbollen.

![24_grid_3d_revit_dynamo_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_5.png)

Group 5 plaatst 3D-modellines op de plaats van de stramienen en stelt de juiste linestyle in.

**5.1 Element Types:** Deze node selecteerd een eigenschap die ingesteld moet worden namelijk 'GraphicStyle. Dit is de linestyle van de nog te plaatsen modelline.<br>
**5.2 Code Block:** Een string in een Code Block plaats je tussen "..". Dit is de naam van de linestyle.<br>
**5.3 All Elements of Type:** Deze selecteerd alle linestylen uit het project.<br>
**5.4 Elements.FilterByName:** Deze node filtert uit de lijst van alle linestyle de ID van de linestyle die de naam heeft conform 5.2<br>
**5.5 Boolean:** Een boolean is een yes/no parameter. In dit geval 'No'<br>
**5.6 Code Block:** Dit is de naam van de parameter die gesteld moet worden. Dit is dus een eigenschap van de modelline.<br>
**5.7 ModelCurve.ByCurve:** Deze node plaatst een modelline op basis van een 'curve'. <br>
**5.8 Element.SetParameterByName:** Deze node neemt alle geplaatst modellines en stelt de eigenschap van de Line Style in.<br>

![24_grid_3d_revit_dynamo_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-02-15/24_grid_3d_revit_dynamo_6.png)

Group 6 draait de stramienbol zodat deze in lijn ligt van de stramienlijn.

**6.1 Vector.ByTwoPoints:** Hier wordt een vector gemaakt die de richting weergeeft van de stramien. Een vector is een lijn met een bepaalde lengte in een bepaalde richting. Deze bestaat uit een x,y,z component.Wikipedia. Het is erg handig om hoeken in de ruimte mee uit te rekenen. Hier wordt een vector gemaakt op basis van 2 coördinaten.<br>
**6.2 Curve.EndPoint:** Deze node geeft de coördinaat van het einde van de stramienlijn.<br>
**6.3 Vector.XAxis:** Dit is de eenheidsvector van de x-as(1,0,0).<br>
**6.4 Vector.AngleBetween:** Deze node berekent de hoek tussen 2 vectoren.(hier wordt gebruikt gemaakt van het scalair product.)<br>
**6.6:** De hoek wordt vermenigvuldigd met -1 omdat de family in lijn moet staan met de gridline.<br>
**6.7 FamilyInstance.SetRotation:** met deze node worden de geplaatste stramienbollen geroteerd.

Je kunt in de je viewtemplate een filter maken zodat deze lijnen en 3D-stramienbollen uit staan. Anders zie je ze in plattegrond dubbel en in de doorsnede.

De volgende stap is maatvoeren. Dit lijkt alleen nog wat ingewikkelder te zijn.