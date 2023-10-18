---
layout: post
title: "nieuwe nodes binnen GIS2BIM"
date: 2022-12-27 19:33:42
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2022-12-27/1672169621689.jpg'
published: true
---

Een aantal nieuwe nodes binnen #GIS2BIM 0.12 om de stikstofdepositieberekeningen(Aerius) iets te sneller uit te voeren.

Laad de afbeelding van een Natura2000 gebied op schaal in Revit via Dynamo en exporteer de gebouwcontour op RD-coordinaten naar de Aerius Calculator.
 
#GIS2BIM is Open Source en gratis in gebruik! &#x1F44C;
 
-Bereken de minimale afstand van je project tot een Natura2000 gebied.<br>
-WMS met Natura2000 gebied(GIS2BIM_GetWebServerData)<br>
-Maak deze afbeelding transparant(GIS2BIM_ImageMakeTransparant)<br>
-Combineer deze met een luchtfoto(GIS2BIM_MergeImages)<br>
-Natura2000 gebieden als polygoon via WFS.(Nieuwe GML-node: GIS2BIM_GMLData)<br>
-Exporteer gebouwcontour als POLYGON die je in kan voeren in Aerius.(GIS2BIM_Aerius_Polygon)
 
Bekijk het YouTube filmpje voor gebruik. [https://lnkd.in/eZq_W5Kz](https://lnkd.in/eZq_W5Kz)
 
Meer informatie over GIS2BIM vind je hier. [https://lnkd.in/eijfhxwp](https://lnkd.in/eijfhxwp)

Script is te downloaden via deze link. [https://lnkd.in/e4pMutDt](https://lnkd.in/e4pMutDt)
 
Feedback en ideeën van harte welkom via Github: [https://lnkd.in/eijfhxwp](https://lnkd.in/eijfhxwp)<br>
#Aerius #GIS2BIM #Stikstofberekeningen #Opensource #Revit #Dynamo #GIS

![1672169621689](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2022-12-27/1672169621689.jpg)

![1672169620686](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2022-12-27/1672169620686.jpg)

![1672169620529](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2022-12-27/1672169620529.jpg)

![1672169620671](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2022-12-27/1672169620671.jpg)