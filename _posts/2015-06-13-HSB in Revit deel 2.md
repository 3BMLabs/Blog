---
layout: post
title: "HSB in Revit deel 2"
date: 2015-06-13 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "Revit 2016"
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/1_vloerniveau.png'
published: true
---

# HSB in Revit deel 2

Revit 2016 is al weer 2 maanden uit. De verbeteringen vallen me heel erg tegen. Revit 2015 R2 leek de goede kant op te gaan, maar in 2016 is erg weinig verbeterd.
Ik gebruik Revit nu 9 jaar. Zoveel oude problemen die nog steeds niet zijn opgelost. Het lijkt echt alsof ze daar in Amerika aan het slapen zijn. Bouwkundig eigenlijk bijna geen verbeteringen.

Maar ondertussen betaal je wel 1200 euro excl. BTW per jaar. **Autodesk is echt een trage flutclub.** Ze kopen een pakket op en de ontwikkeling daarvan gaat vervolgens op stand 0 verder. Neem nu bijvoorbeeld de Revit Extensions. Robot was hiermee bezig. Een supersnelle ontwikkeling. Maar zodra ze overgenomen en geïntegreerd werden bij Autodesk stopt de ontwikkeling. Ik kan me zo voorstellen dat er dan allerlei managementlagen tussenkomen met een hoop blabla maar zonder resultaat.
Nu gebeurt er al jaren vrijwel niets met de extensions. Bij Autodesk staat de gebruiker **niet** centraal! Dat is me na 9 jaar Revit-gebruik wel duidelijk geworden.

**De formule lijkt te zijn:**<br>
-Koop een softwarepakket op wat in basis ontwikkeld is.<br>
-Gooi er een nieuw  interface-sausje overheen.<br>
-Maak het compatibel met je andere producten<br>
-En ontwikkel er vervolgens zo min mogelijk aan want dat is niet nodig voor de verkoop. Of hoogstens om bij te blijven met concurrent.

Hopelijk komt er eens een fatsoenlijke concurrent op de markt. Onderstaande problemen en wensen zijn ook al echt minimaal 9 jaar oud. De verwachting dat dat de komende 10 jaar gaat veranderen is dan ook niet zo heel groot, maar hopelijk heb ik het mis.<br>
- **De 0.2 mm:** Waar slaat het op dat je in een tekenpakket niet kleiner kunt tekenen dan 0.2 mm? Ondermeer bij aluminium vliesgevels in 3D is dit erg vervelend.
- **Balk-kolomverbindingen:** Waarom kun je niet gewoon aangeven dat het einde van een balk op een goede manier afgeschuind kan worden op een aansluitende balk of kolom. De manier van reageren van stalen balken en kolommen is nog steeds niet wat het zou moeten zijn.
- **Verbindingen:** Wanneer komt er eens een fatsoenlijke module/familysoort voor verbindingen in hout, staal en prefab beton zoals bij Tekla. 
- **Wand/vloer/daksystemen:** Wanneer komt er eens een fatsoenlijke wandmodule waar je wand en gevelsystemen met repeterende onderdelen(horizontaal en verticaal (tot 3 of 4x dubbel) kunt modelleren(HSB, alu gevelbeplating, houten gevelbeplating, sandwichpanelen, keramische gevelsystemenen enz.), dakpannen, gevelstenen,  
- **Verouderde en trage 3D-kernel.**
- **Verschillende arceringen** gebruiken voor verschillende schalen in 1 materiaal.
- **Fatsoenlijke kozijnmodule.**

Genoeg geklaagd. Er zijn gelukkig ook een heel aantal zaken wel verbeterd die erg handig zijn.
Wat erg prettig is: Bestandsgrootte is gereduceerd. En de eerste versie lijkt erg stabiel. Weinig fatal errors. Het niveau van een vloer is nu in een floortag uit te lezen.

![1_vloerniveau](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/1_vloerniveau.png) 

## **Verder HSB deel 2**

Achtereenvolgens:<br>
1) Houtfamily v6<br>
2) Diverse HSB-wand/vloerelementen<br>
3) Overig

Je kunt het bestand met de families [hier](http://www.3bm.cloud/dutchrevitblog/20_model.rvt) downloaden.(Revit 2016)

## **1) Houtfamily nieuwe versie**

De houtfamily uit de vorige HSB-blog is aangepast.<br>
1)  Keuze uit 7 doorsnedevormen.<br>
2) In elk vlak 2 kepen kunnen toepassen(ook gecombineerd met de doorsnedevormen)<br>

![2_doorsneden](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/2_doorsneden.png) 

De dubbele keep werkt nog niet helemaal goed. Als dat ook goed werkt kun je dus ook hoek en kilkepers maken die in de hoeken boven en onder correct aansluiten.

![3_kopse_bewerkingen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/3_kopse_bewerkingen.png) 

**3) Tag als 'wizard' voor de invoer. De tag is overigens nog niet compleet**<br>
Je kunt dus in de tag de maten en hoeken intypen en je ziet direct het resultaat.<br>
Je ziet dat je tags dus ook voor andere doeleinden kunt gebruiken. Voor het invullen van parameters in complexe families kun je het meer grafisch maken zonder dat je gelijk een programma daarvoor hoeft te schrijven.

![4_tag_wizard](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/4_tag_wizard.png) 

## **2) HSB-wand families**

Type 1 is een schuine wand met een keep boven en onder als optie.

**Functies:**<br>
-Stijlen zijn geneste families.<br>
-Keep onder/boven kan aan of uit<br>
-Lengte/hoogte/breedte/hoek of delta h/ diverse stijlen aan of uit zetten.<br>
-Stijltype/hoh afstand.<br>
-Tussenstijlen aan of uit zetten.<br>
-Onder/boven/zijregel aan of uit zetten.<br>
-Stijlen gelijk verdelen of startafstand stijl

Type 2 is een rechte wand met vergelijkbare functionaliteit.

![5_hsb-rekken_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/5_hsb-rekken_1.png) 

Type 3 is een rechte wand maar dan met een array in de family. In deze family kun je dus geen stijlen aan of uit zetten.

![6_hsb_rek_zoom](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/6_hsb_rek_zoom.png) 

![7_hsb_2_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/7_hsb_2_3.png) 

Je kunt elke tussenstijl aan of uitzetten in type 2 en 3.  Het nadeel is dat hij daardoor wel trager wordt en een beetje ingewikkeld.

![7a_hsb](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/7a_hsb.png) 

Het voordeel is echter dat je daardoor gemakkelijk sparingen kunt maken. Zie onderstaand.

![7b_hsb_met_sparing](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/7b_hsb_met_sparing.png) 

## **3)Overig**
Met de houtfamily(1e paragraaf) kun je vervolgens vrij eenvoudig allerlei spantvormen, hsb-elementen maken waar ook alle data bekend is en die parametrisch zijn.

![8_hsb_vloerelement](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/8_hsb_vloerelement.png) <br>
*Schuinlopend balklaag element*

![12_steekspant](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/12_steekspant.png) <br>
*Steekspanten*

![11_spant](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/11_spant.png) <br>
*Houten Vakwerkenspant*

![13_fragment](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/13_fragment.png) <br>
*Wanden met rachelwerk e.d.*

Een andere family: Nagelpatroon: Een Adaptive component. Deze bestaat uit een dubbele repeater.

![9_nagelpatroon](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/9_nagelpatroon.png) <br>
*Nagelpatroonfamily waarbij de nagels in een rij verspringen*

![10_verspringing](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-06-13/10_verspringing.png) <br>
*In de family kun je de nagels laten verspringen i.v.m. splijten. Je kunt dan een hogere
kef-factor rekenen conform EC5 tabel 8.1*

Je kunt het bestand met de families [hier](http://www.3bm.cloud/dutchrevitblog/20_model.rvt) downloaden.(Revit 2016)