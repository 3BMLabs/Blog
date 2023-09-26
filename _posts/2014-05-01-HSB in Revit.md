---
layout: post
title: "HSB in Revit"
date: 2014-05-01 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/3_tekening.png'
published: true
---

# HSB in Revit

Deze blog gaat over houtskeletbouw in Revit. En dan met name gericht op het maken van werktekeningen en hoeveelhedenstaten.

Klik [hier](http://www.3bm.cloud/dutchrevitblog/12_HSB.rvt) om het bijbehorend bestand met enkele families te downloaden.

![3_tekening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/3_tekening.png)

Achtereenvolgens:<br>
1. Mogelijkheden om HSB te modelleren
2. Stijl/regelfamily met kopse bewerkingen
3. Samenstellingsfamilies(dakelementen, vloerelementen, wandelementen recht/schuin)
4. Beste practice complexere families.
5. Assemblies/Groups
6. Werktekeningen

![2_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/2_3D.png)

### **1. Mogelijkheden om HSB te modelleren**
Verschillende manieren om HSB in revit te modelleren.<br>
**-Curtain wall:** Heeft als voordeel dat je snel een hele wand met stijl en regelwerk kunt tekenen. Isolatie kan als curtain panel, eventueel ook met geneste beplating of een losse plaat. Nadelen zijn dat een dubbele stijl toevoegen lastig is omdat het curtain panel dan een breedte van 0 krijgt. Verder zijn de hoeken van de mullions niet uit te lezen. Sparingen en andere afwijkingen zijn ook minder makkelijk mogelijk.<br>
**-Structural Columns en/of structural Framings:** De wood-framing tool die bij de extensions4revit zit kan handig zijn om snel stijl en regelwerk toe te voegen. Het nadeel blijft wel dat beams vervelend reageren op aansluitende liggers en zich verplaatsen als je dit niet wilt. Voor specifieke details en afschuiningen verval je snel in het gebruik van referenceplanes en voids om de juiste elementen te krijgen.

![1_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/1_3D.png)

Nadeel van beide methoden is met name dat er een gebrek is aan data die je in schedules uit kunt lezen. Met name het volgende:<br>
-Je wilt van een houten balk die aan 2 zijden schuin is de maximale lengte weten(wat de bestellengte van het hout is). Verder is het handig om de kopse bewerkingen uit te kunnen lezen. Dit kun je gemakkelijk gebruiken bij cnc-machines.

![4_schedule](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/4_schedule.png)

Elektra is ook prima mogelijk in 3D, gekoppeld aan de symbolen in de plattegrond en ook in de wandelementen.

![5_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/5_3D.png)

![6_elektra](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/6_elektra.png)

### **2. Stijl/regelfamily met kopse bewerkingen**
Hier komt het alternatief. Dit is een generic model family(niet linebased) met de volgende functionaliteiten:

1,  **Afmeting** is in te stellen(logisch)<br>
1. **Hoek in** xy en yz-vlak zijn instelbaar.
2. **Profiel** is eenvoudig te wijzigen(profile) deze family is dus bruikbaar voor elk willekeurig lijnvormig element.
3. Workplane-based en niet 'always vertical'
4. Hij is te **roteren** om zijn as(net als een structural framing) zodat je niet elke keer een andere workplane nodig hebt.
5. Je hebt een parameter **'element-lengte'** dit is de lengte die je instelt.
6. Je hebt een shared parameter **lengte**(RevitGG) wat altijd de maximale lengte van het element is.(met behulp van formules). Als je dus 2 hoeken verstek hebt
7. Alle relevante parameters zijn 'shared' zodat deze uit te lezen zijn.
8. Er zijn op beide balkkoppen **4** mogelijke bewerkingen:
    1. hoek in lokaal **xy-vlak.**
    2. hoek in lokaal **yz-vlak.**
    3. **keep** onder in 3 richtingen.
    4. keep **boven** in 3 richtingen.
9. Handelslengte is uitleesbaar. Je kunt 14 handelslengten van het hout invoeren. Vervolgens is er een parameter met een geneste if de maximale lengte uitleest.   if(lengte_hulp < handelslengte_1, lengte_hulp, if(lengte_hulp < handelslengte_2, handelslengte_2, if(lengte_hulp < handelslengte_3, handelslengte_3, if(lengte_hulp < handelslengte_4, handelslengte_4, if(lengte_hulp < handelslengte_5, handelslengte_5, if(lengte_hulp < handelslengte_6, handelslengte_6, if(lengte_hulp < handelslengte_7, handelslengte_7, if(lengte_hulp < handelslengte_8, handelslengte_8, if(lengte_hulp < handelslengte_9, handelslengte_9, if(lengte_hulp < handelslengte_10, handelslengte_10, if(lengte_hulp < handelslengte_11, handelslengte_11, if(lengte_hulp < handelslengte_12, handelslengte_12, if(lengte_hulp < handelslengte_13, handelslengte_13, if(lengte_hulp < handelslengte_14, handelslengte_14, 0 mm)))))))))))))).
10. Deze zou nog uit te breden zijn voor reststukjes kleiner dan de minimale handelslengte.

![7_houtfamily_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/7_houtfamily_1.png)

![9_houtfamily_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/9_houtfamily_3.png)

Er zijn best wat mogelijkheden met deze ene family.

![13_mogeljkheden_family](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/13_mogeljkheden_family.png)

**Samenvatting werking:**<br>
-Er wordt een sweep gemodelleerd tussen 2 referenceplanes.<br>
-Deze sweep zit vast aan referenceplane die voorzien is van een hoek om het profiel te kunnen roteren

![8_houtfamily_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/8_houtfamily_2.png)

-Op de koppen van deze sweep zit een refenceline haaks op de eerder genoemde referenceplane.<br>
-De lengte van de sweep wordt bepaald door 2 lengte-parameters die afhankelijk zijn van de hoek van de kopse bewerking die je instelt.<br>
-Op de eerder genoemde referenceline zit een swept blend void met 2 parametrische profiles

![7_houtfamily_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/7_houtfamily_1.png)

-Deze zijn met een reeks sinus/tangens/cosinus formules gekoppeld aan de instelbare hoek van een kopse bewerking.

-De kepen werking op een vergelijkbare manier.

-Als je de kepen eruit haalt zoals bij de family die als bijlage is toegevoegd is deze een stuk eenvoudiger.

-Het leuke is dat een profiel gemakkelijk te wijzigen is(Pas eerst uitwendige afmeting aan en teken vervolgens het profiel hier binnenin)

![9_houtfamily_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/9_houtfamily_4.png)

-Als je naar LOD400 gaat is een dergelijke family onmisbaar, met name als je goede hoeveelheden staten wilt hebben met de juiste lengten van een element.

Deze family is de basis voor al het stijl, regelwerk, balken, kolommen, latten enzovoorts. Er wordt dus geen gebruik gemaakt van de structural column, structural framing. Dit heeft een aantal terechte nadelen:<br>
-BIM-technisch klopt het niet, aangezien je een structural framing zou verwachten bij een balk.<br>
-Je kunt het niet gebruiken bij de koppeling naar een rekenprogramma.

Dit komt echter met name omdat de structural framingfunctie van revit(voor staal en hout) als je op een hoog detailniveau wilt werken niet handig werkt en de geometrie van de aansluitingen is niet uit te lezen.

Overigens zou je eenvoudigweg het family-type kunnen wijzigen in 'structural framing'. Echter hiermee krijg je nog geen analytical line omdat deze anders opgebouwt is dan een standaard 'structural framing' family.

De families zijn [hier](http://www.studio3bm.nl/12_HSB.rvt) te downloaden.

### **3. Samenstellingsfamilies(dakelementen, vloerelementen, wandelementen recht/schuin)**
Deze houtfamilie kun je natuurlijk gewoon overal los plaatsen, dit kan echter ook gemakkelijker met een samenstellingsfamily.

Hier hebben we een aantal voorbeelden:

**1) Dakelementen**<br>
Dit is een voorbeeld van een dakelement voor een prefab kap. Er zijn hier geen schuine elementen mee te maken. Maar deze kun je gewoon dan met losse elementen modelleren.

**2) Wandelement/vloerelement.**

Deze zijn in beginsel op dezelfde manier opgebouwt. Bij het wandelement wil je echter andere zaken kunnen wijzigen als bij een vloerelement.

Opbouw wandelement(rechthoekig).

**Opties:**<br>
- hoogte/lengte element
- hoh-afstand stijlen
- afstand 1e stijl(om rekening te houden met begin van plaatmaat
- MOD-aantal stijlen. Met een array in de family reken je het aantal stijlen uit. Soms zit er 1 teveel of 1 weinig in, dan kun je dit corrigeren.
- tussenstijlen, stijl links, stijl rechts, onderregel, bovenregel zijn allemaal aan en uit te zetten. Bij een raamsparing kun je hierdoor bijvoorbeeld 3x een family plaatsen, de onder en bovenregel uitzetten en - hier weer een losse regel modelleren.

Zie bijlage

![14_HSB_wandelement](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/14_HSB_wandelement.png)

Deze samenstellingsfamily voorzie ik niet van assemblycode waardoor deze gemakkelijk weg te filteren zijn in een schedule.

![15_parameter_wandelement_rechts](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/15_parameter_wandelement_rechts.png)

Met wat parameters kun je ook een schuine maken(alleen een tikje traag)

![16_wand_element_schuin](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/16_wand_element_schuin.png)

![17_wand_schuin](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/17_wand_schuin.png)

**3) Wandbeplating.**<br>
Als je de wandbeplating ook echt als losse plaatjes wilt modelleren en wilt uit lezen kun je een samenstellingsfamily maken voor wandbeplating. De basis is 1 wandplaatfamily met een hoogte/breedte/dikte.

![10_wandplaat](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/10_wandplaat.png)

Deze wordt vervolgens genest in een samenstellingsfamily.

In deze samenstellingsfamily wil je eigenlijk zowel 1,2,3 of x platen naast elkaar. Maar ook 1 of 2 platen bovenelkaar, afhankelijk van je plaatbreedte. Verder moet het mogelijk zijn om de reststukken van de plaat links en rechts gelijk te verdelen. Dit zorgt voor de volgende 4 situaties:<br>
1) 1 plaat<br>
2) 2 platen<br>
3) 3 platen, reststuk links en rechts)<br>
4) 4 of meer platen(reststuk links en rechts) middelste 2 platen zijn een array

Om de family overzichtelijk te houden worden ze in een rij van 4 gezet en vervolgens naar het midden verplaatst indien van toepassing.

![11_wandplaat](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/11_wandplaat.png)

Het vereist wel wat if-statements om te zorgen dat op het moment dat de plaat 100 mm breed is, de overige elementen in de family niet kleiner dan 1 mm is(anders krijg je hele batterijen errors).

![12_wandplaat](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/12_wandplaat.png)

### **4. Beste practice complexere families.**
De lessen die ik geleerd heb bij het eenvoudig aanmaken van complexere families zijn de volgende:<br>
1. Gebruik  **sweeps** i.p.v. extrusions. Dit voorkomt een spinneweb van referenceplanes in je family met grote kans op de beruchte 'contrains are not satisfied' melding. 
2. Gebruik voor deze sweeps van een **profile**-family i.p.v. 'by sketch'-vorm. Deze kun je gemakkelijk parameterisch maken. Je krijgt hierdoor een meer gelaagde opbouw.
3. Maak bijna altijd gebruik van **geneste shared** families, bij voorkeur max 1 a 2 niveaus diep i.v.m. snelheid. Als je arrays in een family gebruikt is dit ook veel gemakkelijker.
4. Het aantal **'kopjes'** in revit zijn voorgedefinieerd. Groupeer parameters per soort, eventueel onder een andere kop. Voorzie deze group van een **omschrijving** over welke parameters dit gaat.
5. Wees consequent in **naamgeving** van parameters om een rommel te voorkomen.
6. Maak meer gebruik van **referencelines**, met name bij families met hoeken en dergelijke zijn dit erg handige elementen. Deze zijn verplaatsbaar met maatlijnen+parameters in tegenstelling tot referenceplanes.
7. Maak meer gebruik van **if**-statements als bepaalde geometrie niet mogelijk is. Bijvoorbeeld om te voorkomen dat een bepaalde waarde kleiner dan 0 wordt. Dit voorkomt veel errors. Het is net programmeren in zekere zin.
8. **Voorbeeld**: Stel een bepaalde waarde mag niet lager zijn dan 23 mm, anders wordt de profile ongeldig. Maak dan een aparte parameter waarin een if statement zit: `if(parameter<23 23="" li="" parameter="">Maak **eerst** referenceplanes en voorzie deze van parameters. Probeer uit en koppel daarna pas geometrie aan deze referenceplanes

### **5. Assemblies/Group**
Als je (HSB)-werktekeningen in revit wilt maken is er onder meer de assembly functie. In beginsel een fantastische functie voor het maken van werktekeningen.

![18_assembly](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-05-01/18_assembly.png)

Hoe werkt het? Gewoon een aantal elementen selecteren en vervolgens kiezen: 'create assembly'. Van deze assemblies kun je vervolgens views maken

**Beste Practice:**<br>
- Let op met de **schedule** in een assembly. Er zit een bug in(revit 2014 update 2) waardoor deze soms niet geüpdatet wordt na wijzigingen in de assembly. Behalve als je het bestand opnieuw opent. 
- Alternatief is om een **gewone** schedule te maken en te filteren op een assemblyname. Hiermee kun je gemakkelijk schedules kopieren en alleen de filter aanpassen in plaats van elke keer   Nadeel is dat de zichtbare hoeveelheden, de hoeveelheden zijn van alle assemblies van dit soort in plaats van 1 assembly.
- **Geneste** families moeten **apart** in een assembly toegevoegd worden. Dit is een vervelend karwei als je 40 families genest hebt die in een assembly moeten. **Gouden tip:** Maak een group(GP) en ungroup, vervolgens heb je alle geneste families automatisch geselecteerd. Maak vervolgens een assembly.
- Maak **assemblies** zo **laat** mogelijk, bij wijzigingen van assemblies krijg je vaak dat er nieuwe assemblies aangemaakt worden. Je mist eigenlijk een functie na het 'editen' waarmee je kunt kiezen tussen:<br>
    - Pas alle assemblies aan(net als een group)
    - Maak nieuwe assembly na wijziging.(dit gebeurt er nu)
- Het is mogelijk om van iets zowel een **group** als een **assembly** te maken. Deze kun je dan tegelijkertijd kopiëren. Dit is wel bewerkelijk.

 Als alternatief kun je ook gewone views maken, dit geeft echter wel een enorme hoeveelheid gewone views. De ordening conform LACS(NEN 2574)(zoals in nieuwe RevitGG) is dan echt onmisbaar om het overzicht te houden. http://www.nen.nl/pdfpreview/preview_8163.pdf

Je kunt ook assembly-tags gebruiken.

### **6. Werktekeningen**
De laatste stap is het maken van werktekeningen. Dit kost nog altijd wel wat tijd in revit. Je moet de maatvoering zelf plaatsen(tenzij je een aparte tool daarvoor beschikbaar hebt). Cadac heeft hier wel een tool voor(view generator) maar ik vind hem nogal prijzig.

Het is handig om voor aanzichten, doorsneden en 3D-views aparte view-templates aan temaken.

#### **7) Verbeterwensen Revit:**
- Het gebruik van MAX, MIN-statements. Je kunt het simuleren met geneste IF-statements, maar dit kost erg veel .
- Assembly-functie uitbreiden met de group-functionaliteit: Kunnen kiezen voor of voor assembly aanpassen(voor alle assemblies die gemodelleerd zijn. Ofwel kiezen om een nieuwe assembly te maken.

Tags: HSB, Revit, Assembly, houtskelet, houtskeletbouw, families, family, parameters
