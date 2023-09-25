---
layout: post
title: "Wapenen in Revit deel 1"
date: 2015-04-18 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_1_3D_poer.png'
published: true
---

# Wapenen in Revit deel 1

Het bestand met families is [hier](http://www.3bm.cloud/dutchrevitblog/19_wapening.rvt) te downloaden.

Wapening in Revit tekenen(of modelleren) is een veelzijdig verhaal. Afhankelijk van het doel waarvoor je het wil gebruiken. Onderstaand een drietal scenario's van wat het doel zou kunnen zijn van het modelleren.
1. Hoofdconstructeur geeft wapeningsprincipes aan in balken, vloeren, wanden, kolommen.
2. Aannemer/constructeur/fabrikant/tekenbureau werkt wapening verder uit tot detail.
3. Aannemer/constructeur/fabrikant/tekenbureau werkt wapening uit tot het niveau van een buigstaat.

Deze 3 scenario's kunnen op meerdere manieren ingevuld worden. Globaal zijn er minstens 4 manieren hoe je met wapening in Revit kunt omgaan:
1. **Alleen 2D:** 2D-detailcomponenten in detail-views en drafting views.(en in de plattegronden aanzichten)
2. **3D in het model** alleen op de locaties waar je een tekening of detail hebt.
    1. Area-reinforcement om basiswapening in vloeren en wanden aan te geven.
    2. Plaatselijk in een doorsnede of detail met 'Rebar' om staven en beugels aan te geven.
3. **Volledig 3D in het model** met Rebar, Area-reinforcement en Path-reinforcement of eventueel een loadable-family.
4. **Volledig in 3D met werkelijke staaflengten:** In dit geval is de wapening op het niveau van een buigstaat.

Achtereenvolgens:
1) Funderingsplan voor een woonhuis met verschillende wapeningskorven.
2) Poerwapening.

![19_wapening_1_3D_poer](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_1_3D_poer.png) <br>
*Een H-poer in 3D gewapend*

## **1) Alleen 2D: Funderingsplan en details**

Als voorbeeld een eenvoudig balkenrooster. Het principe is om de verschillende korven als 2D standaard detail te tekenen.
- Dit gaat namelijk sneller als wapening als rebar in 3D tekenen.
- De 2D componenten zijn makkelijker herbruikbaar in andere projecten.
- Als je niet helemaal in 3D aan het wapenen bent(maar deels) en je plaatst vrij lokaal wat wapening is dit bij uitwisseling met derden verwarrend.

![19_wapening_3_fragment_fundering](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_3_fragment_fundering.png) <br>
*Fragment van een funderingsplan. De korven zijn in de 'beam' aangegeven met een shared parameter.*

**Bijlegwapening** is een 2D detailcomponent. Dit is een handig component met meerdere variaties om aantallen staven+hoh+lengte enzovoorts weer te geven.

![19_wapening_5_bijlegwapening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_5_bijlegwapening.png)

**Extra beugels.** Dit is ook een detailcomponent

![19_wapening_7_extra_beugels](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_7_extra_beugels.png)

De **korven** zoals hieronder staan in een drafting view. Je kunt er ook een group van maken en dan in detailviews gebruiken.

![19_wapening_4_fragment_fundering_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_4_fragment_fundering_2.png)

**Rechts een korf in 2D gewapend**<br>
(1) is een tag die 'comments uitleest uit het funderingsbalk detailcomponent.<br>
(2) is een tag die de hoofdwapening/flankwapening uitleest met shared parameters.<br>
(3) is een component waarin je aantal staven+diameter+locatie aanhaallijn aan kunt geven.<br>
(4) een detailcomponent voor de beugels.

![19_wapening_2_drafting_view_korftype](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_2_drafting_view_korftype.png)

![19_wapening_6_extra_beugels](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_6_extra_beugels.png)

## **2) Poerwapening**

Dit is poerwapening opgezet volgens principe 3. Volledig in 3D dus.

![19_wapening_7_poerwapening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_7_poerwapening.png)

Bovenstaand een driepaalspoer.

![19_wapening_8_poerwapening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_8_poerwapening.png)

Bovenstaand het voorbeeld uit het bijgevoegde bestand met uitleg over onderdelen:

(1) Tag die 'bgls' uitleest uit de wapeningstaaf.

(2) 2 tags die de hoofdwapening uitlezen

(3) Detailcomponent line-based die de aanhaallijn is. De multi-rebar dimensiontag is zo lelijk dat je die liever wilt gebruiken. Het zou mooi zijn als Autodesk daar iets voor zou gaan maken.

(4) Tag die aantal+diameter uitleest. Het aantal staven is in deze variant te manipuleren. Dit is soms handig als je bij schuine balken meerdere losse staven hebt waar je wel 1 annotatie in doorsnede aan wil geven. Bijvoorbeeld bij een deel van onderstaande poer.

![19_wapening_11_poer_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_11_poer_3D.png)

![19_wapening_9_3D_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_9_3D_1.png)

Soms wordt het 3D wapenen in Revit ook wel een beetje onoverzichtelijk. Zie onderstaand.

![19_wapening_10_3D_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-04-18/19_wapening_10_3D_2.png)

Het bestand met families is [hier](http://www.3bm.cloud/dutchrevitblog/19_wapening.rvt) te downloaden.