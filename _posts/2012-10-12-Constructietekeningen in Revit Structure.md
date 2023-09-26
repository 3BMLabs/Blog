---
layout: post
title: "Constructietekeningen in Revit Structure"
date: 2012-10-12 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_1_kolom_boven_onder_vloer.jpg'
published: true
---

# Constructieplattegronden in Revit Structure

Het is even geleden. Goede voornemens om vaak te bloggen blijken toch lastig waar te maken. Bij deze een stuk over kolom en vloerannotatie in een constructieplattegrond in Revit Structure.

1. Kolom onder en boven vloer<br>
2. Overspanningspijlen

**1. Kolom onder en boven vloer**

![5_1_kolom_boven_onder_vloer](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_1_kolom_boven_onder_vloer.jpg)

Het is mogelijk om een kolom onder en boven de vloer weer te geven met 2 tags. Dit zijn 2 verschillende tags waarin de 'typename' van de desbetreffende kolom uitgelezen wordt.

**Bouw deze als volgt op:**<br>
Maak 1 tag voor boven de vloer waarin je kunt kiezen of het label linksonder, linksboven, rechtsonder of rechtsboven staat. Tevens kun je kiezen tussen tekstgrootte 1.8 mm of 2.5 mm.

![5_2_kolom_boven_vloer_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_2_kolom_boven_vloer_tag.jpg)

Als je een lijn of label selecteert kun je deze via de 'properties' met een 'visible' parameter doorkoppelen, zodat je 8 types voor deze family kunt maken.

![5_3_kolom_boven_vloer_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_3_kolom_boven_vloer_tag.jpg)

Doe hetzelfde voor een kolom onder de vloer.
Om ze handig te gebruiken in je project doe het volgende:
Stel je wilt de constructietekening van de 1e verdieping van tags voorzien:

1. Open de 1e verdiepings tekening
2. Open een 3D view
3. indow Tile(WT)
4. Zorg dat je in de 3D view vanuit een zijkant naar je model kijkt
5. Selecteer in je 3D view alles tussen de bg en 1e verdieping
6. Gebruik filter om alleen de kolommen te pakken te krijgen
7. ga naar je 1e verdiepingstekening met de huidige selectie
8. Ga naar het tabblad 'annotate'
9. Kies voor 'Tag All'
10. Let erop dat 'Only selected objects in current view' aan staa
11. Zoek de tag '28_MV_kolom_onder: 2.5 RB(rechts boven)
12. Klik 'Ok'
13. Kies vervolgens opnieuw voor 'Tag all'. Kies nu kolom boven

![5_4_kolom_boven_vloer_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_4_kolom_boven_vloer_tag.jpg)

Stap 4-6 kan ook vervangen worden als je de gratis selectietool van structural integrators gebruikt. http://www.structuralintegrators.com/products/si_tools_r.php\\
Hiermee kun je gemakkelijk alle kolommen op 1 verdieping selecteren.

### **2. Overspanningspijlen**
Overspanningspijlen in Revit vind ik nog steeds niet ideaal. Het is mogelijk om 'span direction symbol' te gebruiken.

![5_6_span_direction](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_6_span_direction.jpg)

Het grote nadeel vind ik hiervan dat als je meerdere vloervelden hebt en de overspanningspijlen netjes uitgelijnd heb, en je wijzigt de vloercontour, dan verspringt de pijl. Dit vind ik dermate vervelend dat ik deze niet gebruik. Ik geef de voorkeur aan een 'floortag'. Ben benieuwd hoe anderen dit ervaren.

**Nadelen van de floortag zijn:**<br>
- Span direction die in de 'sketch' van de floor gedefinieerd zijn komen niet perse overeen met de overspanningspijl in de tekening.
- e tag kan alleen 'horizontaal' of verticaal staan. Als je een vloerveld met een overspanning onder een hoek hebt ten opzicht van je 'project north' zul je een andere oplossing moeten gebruiken t.w: 'generic annotation' Deze heeft echter als nadeel dat hij niet gekoppeld is aan de vloer.

Een overzicht van de overspanningspijlen zoals ik ze gebruik i.c.m. 'spot elevations'.

![5_7_overspanningspijlen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_7_overspanningspijlen.jpg)

Om deze te realiseren heb je de volgende families met de volgende eigenschappen nodig:<br>
1. Tag overspanningspijl
2. Generic annotation overspanningspijl
3. Spot elevation family met vloerbol
4. Tag vloerbol

Voor het uitlezen van de eigenschappen uit de vloer kun je de volgende parameters gebruiken:<br>
- 'Description' voor omschrijving vloertype
- Aparte 'shared parameter' voor de vloerdikte

Het is mogelijk een vloerbol met een generic model floorbased te maken.<br>
- Maak een nieuwe family 'generic model floorbased'
- Hang een maatlijn aan de 'hostdikte' met een 'reporting parameter'
- Koppel deze reporting parameter door aan een geneste generic annotation die bestaat uit een cirkel met tekst.

Het werkt echter niet helemaal 100%. Als je een breedplaatvloer bijvoorbeeld uit 2 delen wilt opbouwen(2 floors), klopt de uitgelezen dikte al niet meer. Verder houd ik er niet zo van om zo een generic model te gebruiken.

**1. Tag overspanningspijl**

![5_8_overspanningspijl_family](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_8_overspanningspijl_family.jpg)

- Maak een kader van referencelines(je kunt geen extra referenceplanes in tags maken)
- Voorzie deze van parameters
- Plaats de overspanningspijl-lijnen
- Plaats verschillende 'labels' met teksthoogten
- Koppel deze door via 'yes/no' parameters
- Maak vervolgens meerdere typen die je in het project kunt gebruiken

![5_9_overspanningspijl_family_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_9_overspanningspijl_family_2.jpg)

**2. Generic annotation overspanningspijl**<br>
Deze werkt identiek als 1. Wijzig alleen het type in 'generic annotation'

**3. Spot elevation family met vloerbol** 

![5_10_spot_elevation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_10_spot_elevation.jpg)

Dit is een vrij eenvoudige family: Een cirkel waarvan de straal parametrisch is. Maak 3 typen voor verschillende teksthoogten.

Let erop dat het family-type op 'spot elevation symbol' staat. Dit kun je vinden onder 'family category and parameters'.

![5_11_spot_elevation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_11_spot_elevation.jpg)

Als je deze family je project hebt ingeladen moet je hem(of haar) vervolgens in de type properties van de 'spot elevation ' selecteren.

![5_12_spot_elevation_type_propertiesjpg](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_12_spot_elevation_type_propertiesjpg.jpg)

**4. Tag vloerbol**<br>
Dit is een floor-tag. Hij is vergelijkbaar opgebouwd als de spot elevation family.

![5_13_vloerbol](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-10-12/5_13_vloerbol.jpg)

**Overige onderdelen(volgen later)**<br>
3. Arcering van wanden, kolommen onder de vloer
4. Balklaagaanduiding
5. Allerlei tags
6. Balklaagaanduiding
7. Wapening/vorm tekeningen en wapeningsdetails.
