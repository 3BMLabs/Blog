---
layout: post
title: "Zweeds rabbat, potdekselwerk met geintegreerde wall-reveal"
date: 2013-10-22 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/2_family.png'
published: true
---

# Zweeds rabbat, potdekselwerk met geintegreerde wall-reveal

**(zweeds) rabbat en potdekselwerk**

Bij het toepassen van zweeds rabbat of potdekselwerk in een project in Revit kun je je allereerst afvragen hoe gedetailleerd je het wil gaan modelleren. Je kunt ervoor kiezen om een wand met een dikte van bijvoorbeeld 20 mm te modelleren en daar vervolgens een surfacepattern aan te koppelen.

Als je echter details wilt gaan maken direct uit het model is deze methode niet toereikend. Er zijn verschillende opties denkbaar:<br>
1. Losse wallsweeps per rabbat/potdekseldeel
2. Losse delen met generic models
3. Een grote wallreveal bestaande uit meerdere rabbatdelen

![download](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/download.png)

Optie 2 is erg handig als je alle informatie van een willekeurig rabbat deel uit wilt kunnen lezen. Als je deze informatie niet nodig hebt, maar met name de werkende hoogte en de detaillering goed wilt krijgen is optie 3 erg goed toepasbaar

**Optie 1**<br>
We maken een profile voor in dit geval zweeds rabbat, die eigenlijk datgene wat het rabbat moet worden weg gaat snijden.

![download2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/download2.png)

Nadelen van deze methode: Je moet erg veel reveals boven elkaar plaatsen, als de werkende maat wijzigt ben je veel tijd kwijt, als een wandsparing niet precies volgens de werkende maat klopt, werkt de reveal niet goed.

**Optie 3:**

![download3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/download3.png)

![download4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/download4.png)

Met deze methode maak je een profile wallreveal waarbij meerdere rabbatdelen boven elkaar geplaatst worden.  Je kunt deze bijvoorbeeld 6 meter hoog maken zodat je altijd hoge wanden kunt modelleren.
Eventueel is de werkende maat nog parametrisch te maken.

Aandachtspunt: Het 'nulpunt' van de reveal mag niet onderbroken worden door een opening, want dan word de reveal ook onderbroken.

![11_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_1.png)<br>
*Toegepast bij een wand*

![11_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_2.png)<br>
*Onder een kozijn*

![11_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_3.png)<br>
*In een detail*

![11_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_4.png)<br>
*Hetzelfde kun je doen met potdekselwerk*

![11_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_5.png)<br>
*Bij een fels of roeven dak is dit ook handig. Alleen kun je geen geintegreerde sweep
in een roof maken.*

Voorbeeld zoals hieronder weergegeven is een generic model facebased met meerdere voids sweep erin. Deze zijn parametrisch. Hoogte en werkende breedte zijn dus instelbaar. Plaats het op een dakvlak en je kunt gemakkelijk de verdeling aanpassen.

![11_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_6.png)

![11_7](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_7.png)

Klik [hier](http://www.3bm.cloud/dutchrevitblog/rabbat_felsdak.rvt) om het project te downloaden met de verschillende families erin.