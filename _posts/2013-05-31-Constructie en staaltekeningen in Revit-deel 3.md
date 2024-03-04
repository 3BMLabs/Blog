---
layout: post
title: "Constructie en staaltekeningen in Revit deel 3"
date: 2013-05-31 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/2_voorbeeld_staaloverzicht.jpg'
published: true
---

# Constructie en staaltekeningen in Revit, deel 3

Gelukkig is in Revit 2014 het een en ander verbetert met betrekking tot de aansluitingen van liggers en kolommen. Nog steeds niet perfect maar het gaat de goede kant op.

De laatste tijd ben ik bezig om op een slimme manier relatief eenvoudige staalconstructies in revit te modelleren. Na wat experimenteren lukt dit vrij goed en erg snel.

De extension voor staalverbindingen die bij Revit geleverd word is voor ons om allerlei redenen niet goed bruikbaar.

![2_voorbeeld_staaloverzicht](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/2_voorbeeld_staaloverzicht.jpg)

![3_uitvoering](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/3_uitvoering.jpg)

**Ingrediënten:**<br>
1. Slimme families voor staalverbindingen
2. Maatlijnen in kolommen en liggerfamilies die met een shared instance reporting parameter de exacte lengte uitlezen.
3. Aantal goede viewtemplates
4. Tags 
    1. Tag die een afmeting van een strip en de lengte uitleest
    2. Tag die het aantal en soort bout uitleest
    3. Tag die de profielnaam, materiaalsoort, merk, lengte uitleest
    4. Tag die de maat van de las uitleest.<br>
**1. Slimme families**

Benodigde families:<br>
- **SC**: Strip-family:(shared)
    - lengte, breedte, dikte zijn shared instance parameters
- **SC**: Schot-family:(shared)
    - Als strip-family, maar nu met afschuiningen tbv plaatsing in kolom/ligger.
- **SC**: Bout/family(shared)
    - Bouten, boutfamily van autodesk is bruikbaar maar niet zo gedetailleerd
- **SC**: Anker-family(shared)
    - Als bout, maar dan een anker: met/zonder rechte haak.
- **SC**: Enkele hoeklas(shared)
    - Lijnvormige family bestaande uit een hoeklas, a-maat is een instance-parameter
Vervolgens willen we ze gaan combineren. Als voorbeeld een momentvaste verbinding, ligger-kolom, bestaande uit H-profielen:

**Opbouw:**<br>
- **Verbindingsfamily:**<br>
    1. Bouten
    2. Profiel 1/Profiel 2
        1. Solid die profiel weergeeft
        2. strip-family voor:
            1. opdikplaat
            1. afdekplaat/kopplaat
        1. schot-family voor:
            1. liggerschot 1
            1. ligger schot 2
Onderstaand de profielfamily. Alle nested families hebben instance parameters die doorgekoppeld zijn.

![1_aanzicht_profielfamily](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/1_aanzicht_profielfamily.jpg)<br>
*Aanzicht profielfamily*

![2_3D_profiel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/2_3D_profiel.jpg)

![3_parameters_profiel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/3_parameters_profiel.jpg)

Vervolgens maken we voor alle I-profielen een type aan(via het inladen van een type-catalog-bestand).

![3_types_profiel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/3_types_profiel.jpg)

Deze profiel family laden we in de verbindingsfamily. Ook hier maken we een flinke lading parameters aan. De profielfamilies worden van een family-type parameter voorzien, zodat je kunt kiezen wat voor een kolom en ligger je wilt gebruiken.

![5_3D_verbinding](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/5_3D_verbinding.jpg)

![4_parameters_verbinding](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/4_parameters_verbinding.png)

Je kunt de profielfamily voor zowel de kolom als je ligger gebruiken. De profiel-solid kun je uitzetten in het project.

Met evenveel gemak kun je een verbinding maken waar de ligger het doorgaande profiel is.

![6_3D_verbinding_ligger_kolom_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/6_3D_verbinding_ligger_kolom_2.jpg)

![7a_TS_raamwerken](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/7a_TS_raamwerken.jpg)

De maatvoering is hetzelfde als bij TS Verbindingen. Hierdoor is het vrij gemakkeljik om  de maten over te nemen. Een TS-verbindingen-bestand is overigens vrij leesbaar. Wellicht een leuke klus voor iemand om hier een routine voor te schrijven.
 
Of een voetplaatverbinding...

![7_voetplaatverbinding](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/7_voetplaatverbinding.jpg)

Of een dwarskrachtverbinding..

![8_dwarskrachtverbinding_ligger-ligger](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/8_dwarskrachtverbinding_ligger-ligger.jpg)

![9_varianten](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/9_varianten.jpg)

Het enige wat nog verbeterd moet worden is het toevoegen van lassen en het mogelijk maken dat het profiel onder een hoek staat. Ik kom hier later op terug.

Of een houtverbinding. Het verschil is dat bij houtverbinding er iets uit een houten balk gesneden moet worden. De verbindingen bestaan dus voornamelijk uit 'voids' die het hout wegsnijden en op die manier een verbinding vormen. Gemakkelijk over te nemen naar een berekening in excel.

![10_houtverbinding](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/10_houtverbinding.jpg)

Je hebt 1 houtverbindingsfamily met daarin 2 voids. 1 void om het hout uit de kapspruit te snijden. De andere om het hout uit de balk te snijden.<br>
-Je plaatst er 2 op dezelfde plaats.<br>
-M.b.v. een instance parameter laat je de void 'verspringen.<br>
-Vervolgens 2x 'cut geometry' 

![12_houtverbinding_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/12_houtverbinding_2.jpg)

![11_houtverbinding_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/11_houtverbinding_1.jpg)

![13_houtverbinding_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/13_houtverbinding_3.jpg)

![14_houtconstructie](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/14_houtconstructie.jpg)

![15_houtverbinding_8](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/15_houtverbinding_8.jpg)

![16_houtverbinding_koppeling_met_spreadsheet](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/16_houtverbinding_koppeling_met_spreadsheet.jpg)

![17_spant](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/17_spant.jpg)

![18_detail](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/18_detail.jpg)

**2.Maatlijnen in kolommen en liggerfamilies.**

Voeg in elke staalfamily een instance reporting shared parameter van het type 'length' toe. Let op je de dimensionline niet aan de 'member right' referenceplane hangt maar aan degene die op dezelfde plaats aanwezig is(weak reference).

![19_liggerfamily](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/19_liggerfamily.jpg)

**3. Goede viewtemplates.**<br>
Spreek voor zich.

**4.Tags**

![20_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/20_tag.jpg)

![21_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/21_tag.jpg)

![22_tag](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/22_tag.jpg)

**Staaltekening**

![23_staaltekening_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/23_staaltekening_1.jpg)

![24_staaltekening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2013-05-31/24_staaltekening.jpg)

Conclusie voor het soort werk wat wij ermee doen is dat je prima staal werktekeningen in revit kunt maken. Het enige is dat je wat tijd moet stoppen in het maken van standaard verbindingen. Hier heb je autoCAD structural detailling dus niet perse voor nodig.