---
layout: post
title: "Kozijnen in Revit"
date: 2013-07-31 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_1.png'
published: true
---

# Kozijnen in Revit

Deze aflevering gaat over kozijnen. In Revit is het mogelijk om kozijnen te maken met een window family(of curtain wall). Als je gedetailleerde parametrische kozijnen wilt gaan maken stap je al snel over op geneste families om zodoende herhaling van veel referenceplanes te voorkomen.

Verder zie dat verschillende leveranciers zoals SmartRevit en DeltaPi for Revit de detaillering van het kozijn in een aparte family plaatsen en het kozijn zelf ook. Het kozijn zit genest in de wandsparingfamily.

Deze aflevering concentreerd zich op het kozijn zelf. Als je bij voorkeur geen extra tools boven op revit aanschaft, onder meer vanwege de kosten, dan moet je toch wat anders bedenken.

Eerst even een paar voorbeelden:

![10_window_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_1.png)<br>
*Kozijn uit 1920*

![10_window_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_2.png)

![10_window_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_3.png)

![10_window_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_4.png)<br>
*Pen en gat verbinding en scharnier*

![10_window_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_5.png)

![10_window_20](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_20.png)<br>
*Overzicht van kozijnen in een project*

![10_window_21](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_21.png)<br>
*Kozijn met een ventilatierooster uit bouwconnect*

![10_window_22](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_22.png)

![10_window_23](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_23.png)

### **Principe opbouw**
We maken 4 families aan waar we alle kozijnen, ramen en deuren mee kunnen maken:<br>
- Kozijnfamily
    - Kozijnstijlfamily
    - Dorpelfamily
    - Glasfamily
        - eventueel ventilatierooster
    - Raam
        - raamstijl
        - aluminium profielen
        - tochtband
    - Deur
        - deurstijl

Het nadeel is dat je redelijk diep gaat nesten. Je kunt echter ook minder diep nesten als je wilt(bijvoorbeeld de raamstijlen direct in het kozijn, maar heeft ook weer nadelen)

Het principe van de family is dat we een eenvoudige rechthoekige sweep maken waar we vervolgens met een void de profielvorm snijden. Met 2 anders voids maken we de kozijnaansluitingen.

![10_window_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_6.png)

Elke aansluiting staat met een referenceplane geparametriseerd zodat deze als je hem nodig hebt uit het 'rek' kan pakken.

### **Werking aansluiting**

Het principe is dat je een 'voorraad rek' maakt van alle kozijnprofielen die je nodig hebt. Deze zijn gemaakt uit een void sweep met een parametrisch profiel. Je kiest een profiel door een nummer in te voeren. De void 'springt' op zijn plek en snijd het profiel. Voor de aansluitingen werkt dit identiek.

![10_window_7](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_7.png)<br>
*Plattegrond van de family waarbij alle aansluitmogelijkheden zichtbaar zijn*

![10_window_8](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_8.png)<br>
*Onderste profiel is de solid sweep. Daarboven 2 void sweeps die 2 verschillende kozijnprofielen maken.*

![10_window_9](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_9.png)<br>
*In dit geval is de onderste void sweep gebruikt om het kozijnprofiel te maken.*

![10_window_10](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_10.png)

![10_window_11](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_11.png)

![10_window_12](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_12.png)

![10_window_13](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_13.png)

![10_window_14](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_14.png)

![10_window_15](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_15.png)<br>
*Er zijn wel beperkingen ten aanzien van de geometrie. Als je de sponningsdiepte bij een profiel van 67 mm hoog groter dan 23 maakt kan de tussenstijl niet meer gemaakt worden. Dit zou overigens nog op te lossen zijn door in de profielfamily een if-statement te gebruiken.*

![10_window_16](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_16.png)<br>
*De plattegrond waarin enkele van de mogelijke aansluitingen zichtbaar zijn.*

### **Extra profiel toevoegen**
- Maak een parametrische profielfamily aan(let op de extra omkadering)
- Laat in de kozijnprofielfamily en koppel de parameters door
- Kopieer in aanzicht links de bovenste referenceplane en void 500 mm omhoog
- Wijzig de profile-family in de void
- Selecteer de referenceplane en zet deze op 'not a reference'
- Plaats een maatlijn vanaf deze referenceplane t/m onderaan en geef deze een type-parameter mee.
- Hang hieraan een formule zodat hij kan verspringen
- Maak een nieuw type aan en zet de profielparameter op het nieuwe profiel
- Gebruik cut geometry om uit te snijden

### **Aandachtspunten**
- Alle referenceplanes die relatief ver van het nulpunt van de family af staan moeten op 'not a reference' staan anders
- De parameters zijn begrenst in hun gebruik. In het geval dat het profiel 67 breed is en je wilt een sponningshoogte groter dan 23 zal er een error verschijnen omdat dan de tussenstijl met scharniersponning als profiel niet meer voldoet
- Je moet erop letten dat er geen geometrie ontstaat kleiner dan 0.8 mm omdat je anders allerlei 'cannot make'-meldigen krijgt.

### **Nadelen**
Alleen te gebruiken door een gevorderde gebruiker.
Relatief complex


### **Speciale gevallen**
Je kunt onder meer ronde kozijnprofielen maken en ook een kozijnstijl met 2 profielen. Het is ook mogelijk om in verstek aansluitingen aan te maken.

![10_window_17](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_17.png)

![10_window_18](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_18.png)

![10_window_19](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-07-31/10_window_19.png)<br>
*Voor monumentale kozijnprofielen zijn aparte parameters aanwezig omdat deze qua afmetingen erg afwijkend zijn ten opzichte van de NBvT 2010.*

Als er nog suggesties zijn hoor ik het graag. De beta-versie is [hier](http://www.3bm.cloud/dutchrevitblog/31_WI_stijl.zip) te downloaden.