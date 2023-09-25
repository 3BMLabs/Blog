---
layout: post
title: "Adaptive Components in de praktijk"
date: 2014-09-30 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/1_rollaag_3D.png'
published: true
---

# Adaptive Components in de praktijk

Een van de fantastische functies in Revit zijn de adaptive components. Op internet is er erg veel informatie over te vinden die ik hier niet ga herhalen. Met name gericht op allerlei bizarre vreemde vormen die je als gemiddelde bouwkundig modelleur in de praktijk minder vaak tegen komt.

Ik had eerlijk gezegd nog nooit echt serieuze aandacht aan adaptive components besteed. Onlangs moest ik een project modelleren met taps toelopende panelen. Dit was een mooie aanleiding om me erin te verdiepen. Het is werkelijk een fantastische functie met ongekende mogelijkheden.

Download het Revit-bestand met alle families [hier](http://www.3bm.cloud/dutchrevitblog/15_adaptive_components.rvt).

**Achtereenvolgens:**
1) Toog/rollaag<br>
2) Overige mogelijkheden<br>
3) Tips, voordelen en nadelen

![1_rollaag_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/1_rollaag_3D.png)

## **1) Toog/rollaag**
Een adaptive component is erg gemakkelijk als je een array hebt van elementen die in meerdere richtingen en patronen en vlakken lopen. Als je dan een normale revit-family gebruikt wordt je nogal moe van het maken van parameters.

Neem nu bijvoorbeeld de volgende toog-family. Dit is een parametrische toog met een normale revit-family.

![3_rollaag_family](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/3_rollaag_family.png)

Omdat radiale arrays in de normale family-omgeving binnen revit niet geheel parametrisch gemaakt kunnen worden is er voor de volgende 3-laagse opbouw gekozen:

![3_toog_family](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/3_toog_family.png)

1)**Samenstelling** van **sluitsteen** + 2 halve togen

2) **Halve toog** opgebouwd uit deelfamily bestaande uit 4 stenen

![4_rollaag_deelcomponent](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/4_rollaag_deelcomponent.png)

3) **Deelfamily** uit 4 stenen

Het is dus met wat kunst en vliegwerk mogelijk om deze parametrisch te maken. Je komt alleen helemaal om in de parameters.

Met adaptive components kan dit een stuk minder complex(nog wel redelijk bewerkelijk)

We kijken naar een Hanekam.

1) **Maak een nieuwe family(Generic Model Adaptive).**

- Plaats enkele referenceplanes en voorzie deze van parameters zoals onderstaand aangegeven.

![5_rollaag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/5_rollaag.png)

- Plaats een Referencepoint, maak deze adaptive.

![6_rollaag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/6_rollaag.png)

- Plaats met referencelines de overige 2 punten en referencelines.

![6_rollaag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/6_rollaag.png)

- Vervolgens gaan we het path dividen.
- Selecteer de linker referenceline(gebruik tab)
- Klik op 'divide path'.
- Zet Number op '2'
- Stel Beginning of End Indent in op bv 320, maak parametrisch: 'afstand_3'

![9_hanekam](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/9_hanekam.png)

- Doe dit ook aan de andere zijde
- Teken 3 extra referencelines. 1 op wat de onderzijde van de rollaag is.
- En 2 stuks links en rechts aan de zijkant van de rollaag.
- Divide deze ook. Links en rechts in 4 punten. Boven in ca 30 punten en voorzie deze van parameters

![10_hanekam](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/10_hanekam.png)

- Test regelmatig of de punten allemaal goed op lines gehost zijn door de parameters te veranderen
- Teken nog 2 referencelines extra en divide deze voor de tussengedeelten.

Gebruik vervolgens de 6-points adaptive steen om de rollaag te bouwen. Deze uitleggen gaat een beetje te veel blogruimte kosten. Wellicht een volgende keer. Onderstaand is weergegeven hoe hij eruit ziet. Je kunt hem downloaden in het totaalbestand en bekijken hoe hij in elkaar steekt.

![11_steenfamily](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/11_steenfamily.png)

 Vervolgens komt de kracht van de 'repeater' om de hoek kijken. Plaats de steenfamily op het grid(let op, by face' niet 'by workplane' anders werkt de 'repeater' niet.

![12_steen_op_grid](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/12_steen_op_grid.png)

- Je moet dus 6 punten plaatsen. Let goed op de volgorde.

![13_steen_op_grid_repeater](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/13_steen_op_grid_repeater.png)

- Gebruik de repeater.

![14_rollaag_parameters](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/14_rollaag_parameters.png)

- Herhaal dit voor de andere stenen. Let op de formules voor even/oneven in de parameters.
- Herhaal dit voor de andere stenen. Je hebt dus uiteindelijk 3 repeaters gebruikt.

De randcondities blijven wel lastig. Ik krijg het niet voor elkaar om de rand standaard correct te hebben. Wellicht iemand een suggestie. Voor een gewone rollaag is het geen probleem uiteraard. 

Een andere variant is denkbaar met een getoogde onderzijde zoals hieronder. Dit is ook niet al te ingewikkeld.(Zie bijgevoegd Revit-bestand)

![15_rollaag_varianten](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/15_rollaag_varianten.png)

## **2)Overige mogelijkheden**
Andere mogelijke toepassingen zijn: Houtskeletbouw. De families die als voorbeeld in het model zitten hebben wel de 'concept-status'. Ze zijn in ontwikkeling. Onderstaand een hsb-wand waarbij de stijlen met een repeater gemaakt zijn.

![16_HSB](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/16_HSB.png)

Je kunt ook gemakkelijk vreemde vormen voorzien van houtskeletbouwelementen. Hierover in een volgende blog meer.

**Andere mogelijkheid**<br>
Parametrische **huizen**. Je kunt gemakkelijk vanuit een parametrische massa een heel configureerbaar huis maken zonder het spoor bijster te raken met parameters.

![17_parametrische_huizen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/17_parametrische_huizen.png)

Een volgend idee: Tegelvloeren etcetera en  alles wat herhalend voorkomt in meerdere richtingen:

![18_tegelvloeren](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/18_tegelvloeren.png)

Hier komt wel gelijk een lastig iets boven water van patterns. De randcondities zijn niet altijd goed automatisch op te lossen, handmatig wel overigens. Eigenlijk zouden de randcondities automatisch op 'fit to tile' gezet moeten worden. Dit kan niet bij sommige paneelvormen. Iemand een suggestie?

![19_metselwerkwanden](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/19_metselwerkwanden.png)<br>
*Metselwerkverbanden en gekleurde stenen komen ineens binnen handbereik.*

Een andere optie zijn gestucte sierlijsten. Deze is gebaseerd op 4 punten. De hoekoplossingen zijn correct en de lengte kan ook uitgelezen worden.

![20_stuclijst_4_points](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/20_stuclijst_4_points.png)

## **3) Tips, voordelen en nadelen**

**Aandachtspunten en tips:**<br>
Als je met Adaptive components begint:<br>
- **Vergeet** even alles wat je al wist van families en parametriseren in Revit. Adaptive components is een andere manier van denken. **Denken** in **punten** en **lijnen** in plaats van referenceplanes en maatvoeringen met parameters.
- Een Revit profile-family is **niet** bruikbaar in een adaptive component. Je kunt wel een **adaptivecomponent**-family maken die je als profile gebruikt. Zie hiervoor bijvoorbeeld de stuclijst.
- Zoek vooral op **internet** naar bruikbare **tips** en voorbeelden. De handleiding van autodesk is erg **summier** waar het gaat over het gebruik van de adaptive components.

**Repeaters:**<br>
Een repeater is een intelligente array.<br>
- Als je een adaptive component op een 'divided line' of 'divided surface' **plaatst**, let erop dat je deze tijdens plaatsen op **'by face'** hebt staan. Als je dit niet doet, maar bijvoorbeeld op het **workplane** 'ref level' werkt de repeater-functie niet.
- Als je meerdere 'divided lines' gebruikt(bijvoorbeeld bij de schuine rollaag) let op de **richting** waarin de deze tekent. Als ze in tegengestelde richting lopen ontstaat werkt de repeater ook 
- Uitlezen van parameters: Doe dit vooral met **'shared reporting instance parameters'. Adaptive points** laten zich niet dwingen. 

**Nadelen adaptive components:**<br>
- Je kunt geen voids uitsnijden in een project. 
- Parameters uitlezen heeft soms zijn beperkingen. Het gebruiken van reporting parameters in formules ook. Dit is soms lastig.
- Randcondities in patronen en repeaters blijven gevoelig.
- De **families** zijn erg traag. Bij grote projecten niet te veel en niet te diep nesten anders wordt het onwerkbaar. Je vraagt je wel af wanneer dit snelheidsprobleem nu een keer opgelost gaat worden door autodesk.

Tot slot: Heeft u al opgemerkt dat in Revit 2015 R2 verschillende erg handige dingen nieuw zijn:<br>
1) **Search**-mogelijkheid bij kiezen van families!!!!! Geweldig!

![21_search_venster](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/21_search_venster.png)

2) Load into project and close. Dat voorkomt dat je 20 families open hebt staan tegelijkertijd.

![22_load_into_project_and_close](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-09-30/22_load_into_project_and_close.png)

Dat lijkt veel goeds te beloven voor Revit 2016. Wellicht gaat Autodesk zaken verbeteren waar de gebruiker echt iets aan heeft.

Download het Revit-bestand met alle families [hier](http://www.3bm.cloud/dutchrevitblog/15_adaptive_components.rvt).