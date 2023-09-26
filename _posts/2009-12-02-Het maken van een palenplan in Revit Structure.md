---
layout: post
title: "Het maken van een palenplan in Revit Structure"
date: 2009-12-02 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_1_kolom_boven_onder_vloer.jpg'
published: true
---

# Het maken van een palenplan in Revit Structure

Het maken van een palenplan zoals bij ingenieursbureaus gebruikelijk zit niet in de standaard content welke bij Revit geleverd wordt. Deze blog beschrijft kort hoe je in Revit Structure dit toch voor elkaar kunt krijgen.<br>
De paal als 3D-element is een 'Structural Foundation Isolated'.<br>
Het paalsymbool is een genest 'Detailcomponent'

**De paalfamily heeft de volgende eigenschappen/gebruiksaanwijzing:**

**Plaatsing** altijd op het level:'Peil'. De werkelijke locatie wordt door een parameter bepaald.<br>
**Zichtbaarheidsniveau**: 'Fine' is een gestippelde cirkel zichtbaar die het invloedsgebied van de paal aanduid: bv 4D, 3D of in geval van een trekpaal misschien wel 6 of 7D.<br>
**Paalsymbool**: Het paalsymbool wordt geregeld met een genest detailcomponent welke gekozen kan worden in de Type-properties.<br>
**Paaltypen**: Een paal is een apart type indien een v/d volgende eigenschappen verschillen: Puntniveau, Afhakhoogte, Diameter, Ok. Fundering,<br>
**Paaltabel in een schedule**: De parameters zijn veelal 'shared' gemaakt zodat deze in een schedule uitgelezen kunnen worden.

**De volgende eigenschappen** zouden geoptimaliseerd moeten worden. Ik ben er echter nog niet achter hoe. Als iemand een tip heeft hoor ik het graag:

**Peil t.o.v. N.A.P.**: Uitlezen van shared coordination wat het Peil t.o.v. N.A.P. is. Zodat je dit niet elke keer behoeft in te voeren.<br>
**Paalsymbool:** De weergave van het paalsymbool detailcomponent in een schedule.(dit is mogelijk met wat kunst en vliegwerk door een lettertype aan te passen met een 'font creator' maar ik vind het nog geen optimaal resultaat geven)<br>
**Schoorstand**: Zelf heb ik tot nu toe dit niet nodig gehad. Maar dit zou ook in de family ingebouwd kunnen worden.<br>
**Steunpuntsherkenning**: Bij het berekenen in Robot worden de palen als steunpunt herkent. Indien je gebruik maakt van de Revit-tool: 'static analysis of slabs' zou dit herkent moet worden als steunpunt. Dit is echter helaas niet het geval. Hetzelfde geld voor 'Load Take Down'. **Oplossing**: Palen vervangen door kolommen.<br>
**Puntniveaus i.c.m. sonderingen**: Het zou mooi zijn als je puntniveaus zou kunnen modelleren waarop de palenplan die in dat gebied staan automatisch dat puntniveau overnemen. Ik heb wat geexperimenteerd met levels/referenceplanes. Maar dit gaf geen bevredigend resultaat.

**1) Paalsymboolfamily:**

**Type**: Detailcomponent. Met behulp van vlakjes met 'yes/no' parameters is deze gedefinieerd.

![1_05](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_05.jpg)

**2)Parameters in de paal-family:**

**naam;**(Type of Parameter);(Instance/Type);(Toelichting)

**Type Paalsymbool;** (Family type: Detail Items);(Type); (doorgekoppeld aan genest detailcomponent)

**17_MV_afkaphoogte_tov_ok_fundering;**(Lengte);(Type);

**Width;**(Length);(Type); (Parameterisch aan de paalafmeting gekoppeld)

**Length;**(Length);(Type);(Doorgekoppeld aan lengte van de Solid, betreft de theoretische paallengte)

**17_MV_paalafstand_XXX_D;**(Number);(Type); (Geeft een cirkel in plattegrond waar het invloedsgebied van de paal zit)

**17_MV_paal_in_fundering;**(Length);(Type);(Lengte dat paal in de fundering zit na het koppen snellen)

**17_MV_ok_fundering_peil;**(Length);(Type)

**17_MV_inheiniveau_tov_NAP;**(Length);(Type);(Puntniveau v/d Paal ten opzichte van het N.A.P.)

**17_MV_peil_tov_NAP;(Length);**(Type);(Hoogte van het bouwpeil ten opzichte van N.A.P.)

**17_MV_paaltrekvermogen;**(Force);(Type);

**17_MV_paaldraagvermogen;**(Force);(Type);

**17_MV_xd;**(Length);(Type);(straal van invloedsgebied paal)

**17_MV_straal;**(Length);(Type);(straal v/d paal)

**17_MV_paallengte_onder_fundering;**(Length);(Type);(bepaald de depth v/d extrusion)

**17_MV_onderkant_fundering_peil_inverse;**(Length);(Type);(inverse van 17_MV_ok_fundering_peil zodat deze gekoppeld kan worden aan een maatlijn)

![1_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_1.jpg)

**3)Palenplanview in Revit Structure**

De palenplanview in Revit Structure is als het volgt opgebouwd:

![1_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_2.jpg)

-Aparte Type View--> Palenplan met view direction: 'up'

![1_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_3.jpg)

-View Depth instellingen aanpassen

![1_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_4.jpg)

-Visibily Graphics aanpassen

![1_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_5.jpg)

-Paalhernummeren kan met behulp v/d Revit Extensions

-Inheigebieden geef ik 'met de hand' aan. d.m.v. een detailline.

-De weergave v/h puntniveau in plattegrond is m.b.v. een tag.

![1_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2009-12-02/1_6.jpg)

De palentabel is met behulp van een schedule te maken. Hiermee kunnen allerlei parameters gedefinieerd worden om daarmee uiteindelijk het aantal palen met de bijbehorende gegevens te gegenereren.

Dat was in het kort gezegt een methode om een palenplan te maken in Revit Structure. Zonder twijfel zijn er meer methoden met allen z'n voor en nadelen.