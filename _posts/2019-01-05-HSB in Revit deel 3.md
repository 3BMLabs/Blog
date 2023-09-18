---
layout: post
title: "HSB in Revit deel 3"
date: 2019-01-05 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "HSB in Revit"
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/6_3D doorsnede.png'
published: true
---

# HSB in Revit deel 3

**Dataset behorend bij deze blog is [hier](https://github.com/DutchSailor/blog/tree/master/Bouwtechniek%20%26%20Revit/2019-01%20HSB%20deel%203) te downloaden.**
<br><br>
Een vervolg op de blog over het modelleren van houtskeletbouw(HSB) binnen Autodesk Revit. Er zijn nog 2 delen die over HSB geschreven zijn:
<br><br>
[HSB Deel 1](https://revitstructure-nl.blogspot.com/2014/05/hsb-in-revit.html?view=flipcard)<br>
[HSB Deel 2](https://revitstructure-nl.blogspot.com/2015/06/revit-2016-hsb-in-revit-deel-2.html?view=flipcard)

De houtfamily die hierin genoemd is, is inmiddels weer verbeterd. Ook de samenstellingsfamily. En mijn collega Piet Mol heeft een aantal Dynamoroutines gemaakt.

Enerzijds kun je deze gebruiken als je met behulp van Revit detailengineering van HSB wilt uitvoeren. Anderzijds is het denk ik met deze families ook mogelijk om als architect/ingenieursbureau/aannemer het HSB snel te modelleren voor bouwtechnisch modelleerwerk/tekenwerk van een hoog detailniveau.<br>

![6_3D doorsnede](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/6_3D_doorsnede.png) <br><br>

**1. De houtfamily**

Tijdens het gebruik hebben we weer diverse zaken aangepast aan de houtfamily.

**Center**: De afschuiningen worden vanuit het hart berekend in plaats vanaf de zijkant. Dit heeft veel voordelen bij het wisselen van hoeken. Tevens zijn een aantal bugs bij het gebruik van dubbele hoeken eruit gehaald.

![1 Centerline](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/1_Centerline.png)

![1 Centerline 2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/1_Centerline2.png)

**Hoek XY, YZ.** Als je een combinatie van de hoek XY en YZ gebruikt wordt ook de hoek haak op dit vlak ook berekend. Dit is feitelijk de hoek als je bijvoorbeeld met een afkortzaag een houten balk wilt afkorten.

![12_HSB_hoek](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/12_HSB_hoek.png)

In het bovenstaande geval is de ingestelde hoek XY 58 graden en YZ 128 graden.
De eerste hoek die je nodig hebt voor de afkortzaag is 128-90 = **38 graden.**

![12_HSB_hoek_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/12_HSB_hoek_2.png)

De tweede hoek die je wilt weten is de X from YZ-plane. Dat is feitelijk de helling van de afkortzaag. 90-cotan( cos(90-128) x tan(90-48))= 63.78 graden. Deze kun je dus in de zaagstaat zetten.

**Structural Framing:** Het gebruik van een Generic Model heeft een aantal nadelen. Het gebruik van een Structural Framing ook. Ik gebruik tegenwoordig een aparte Structural Framing family waarin de houtfamily genest in zit. Daardoor zijn wel alle elementen in 1 hoeveelhedenstaat(Generic Model) uit te lezen. 

![GenericModel_Structural_Framing](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/GenericModel_Structural_Framing.png)

![2_Extend](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/2_Extend.png)

**2. Samenstellingsfamily**
Toevoegingen ten opzichte van de vorig blog:

**Extra bovenregel/onderregel:** Deze kan bijvoorbeeld gebruikt worden voor een haakregel bij de muurplaat.

![4_Haakregel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/4_Haakregel.png)

**Crosssection Rotation Top Stud en Side Stud kunnen tegelijk ingesteld worden.**

![2_Double_Corner_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/2_Double_Corner_2.png)

De 'Left Side Stud' is hier 35 graden. De 'Top Stud' 45 graden. Het vraagstuk was hoe je de hoek XY en YZ van deze zijregel en bovenregel kunt berekenen.

![2_Double_Corner_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/2_Double_Corner_1.png)

Uiteindelijk bleek het heel erg makkelijk. Ik heb de hele avond zitten te stoeien met bovenstaande afbeelding. 

Na enorme bergen formules bleek de het onderstaande het geval:

**Alpha:** Rotation of Top Stud.<br>
**Beta:** Rotation of Side Stud.

**XY-hoek van de Side Stud:** 90 - cotan( tan(beta) * **sin**(alpha) )<br>
**YZ-hoek van de Side Stud:** 90 - cotan( tan(beta) * **cos**(alpha) )

[Revit-bestand met bovenstaande afbeelding](http://www.3bm.cloud/dutchrevitblog/2018-12%20Wood%20Framing.rvt)

Je kunt het natuurlijk ook met vectoren doen. Binnen Dynamo zou dit erg makkelijk zijn. Alleen binnen de family editor is dit erg omslachtig.

Best grappig dat het dus uiteindelijk erg eenvoudig is. Soms maak je het ook gewoon te moeilijk voor jezelf.

**Top Stud/Bottom Stud:** Afschuining onder en boven in kunnen stellen. 

![3_Angle_Bottom_Top](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/3_Angle_Bottom_Top.png)

**Bovenplaat/Onderplaat:**
Er is een beplatingsfamily toegevoegd als onder en bovenplaat.Je kunt een offset ten opzichte van de zijkant instellen.

![5_Panel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/5_Panel.png)

**Keep uit stijl en regelwerk:**

![13_Void_Top](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/13_Void_Top.png)

**3. Tips tijdens het uitwerken van HSB.**

**Een mogelijke werkvolgorde:**
1. Begin met het maken van **principedetails in een drafting view.** Ga na goedkeuring door alle betrokken partijen pas starten met 3D modelleren.
2. Start met modelleren van de **HSB-contouren** bestaande uit het stijl en regelwerk met de houten beplating. Gebruik hiervoor floor, roof en walls. 
3. Modelleer **sparingen.**
4. Bepaal **elementindeling** inclusief toleraties.
5. **Splits** wanden,vloeren daken op in deze elementen. Maak direct groups voor unieke merken.
6. **Modelleerwijzen.** Er zijn verschillende manieren om snel HSB-elementen te plaatsen:
    1. **Samenstellingsfamily** plaatsen(daken, vloeren).
    2. **Losse** Structural Framingfamilies plaatsen.(met name bij schuine elementen)
    3. **Dynamo** gebruiken om automatisch Structural Framingfamilies te plaatsen.(ik hoop hier ooit nog een blog over te gaan schrijven
7. **Voeg** de elementen toe aan de group.
8. **Ungroup de group** en maak Assembly(doe dit pas als alles in 3D correct is.)
9. **Controleer** alle nulpunten van de assemblies.
10. Maak van elk vergelijkbaar soort HSB-element **een tekening** aan(dak, vloer wand bijvoorbeeld.) Je kunt dit ook standaard in je template zetten in de fase Renvooi.
11. Gebruik **Dynamoscripts** om automatisch alle assemblytekeningen te maken.
12. Maatvoeren moet nog wel gewoon met de hand.

Tips&Trics bij bovenstaande werkvolgorde:

**1. Details**

![8_Details](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/8_Details.png)

Hoe het eigenlijk zou moeten werken is dat je eerst een detail opzet in 2D. En vervolgens kunt aangeven in Revit dat dit detail op een bepaalde aansluiting van toepassing is. Vervolgens moeten dan alle elementen op die plaats in 3D gemodelleerd worden. Hier later meer over.

![9_Details_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/9_Details_2.png)

We gebruiken tegenwoordig gekleurde arceringen sinds Revit 2019. Dit is echt fantastisch. Je kunt alle werkelijke kleuren van de materialen instellen waardoor een tekening beter gaat spreken.

![10_Arceringen_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/10_Arceringen_1.png)

![10_Arceringen_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/10_Arceringen_2.png)

Alle filled regions zitten in het te downloaden bestand. Ook zijn al deze arceringen beschikbaar via filters zodat het ook in plattegronden, doorsneden en details werkt met de juiste schaal!

![19_3D_Detail](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/19_3D_Detail.png)

![20_3D_Doorsnede](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/20_3D_Doorsnede.png)

Het leuke is dat je dus een 3D-doorsnede kunt maken waarbij de doorsnede arceringen een kleur hebben en de rest van de doorsnede niet.

**6 Modelleerwijzen**

**Hoekkepers**
Hoekkepers zijn nu nog best lastig met name bij 2 verschillende dakhoeken. Ik ben nog met een nieuwe versie bezig waarbij dit echt erg eenvoudig gaat worden.

![7_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/7_3D.png)

**Dakkapel**

![16_Dakkapel](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/16_Dakkapel.png)

Zijwangen zijn gemaakt met behulp van Structural Framing.


**8 Groups/Assemblies:**

**Nieuwe gouden tip:** Plaats generic models en samenstellingsfamilies **by face** op een roof.. Hierdoor is het mogelijk om elementen te draaien en te spiegelen zonder dat je allerlei 'workplane' problemen krijgt. Je moet hiervoor wel de 'host' meekopiëren/roteren. Als je een hellend dak op een workplane plaatst op basis van een referenceplane kun je deze assemblies niet kopiëren.

**Gouden tip 2(vanuit vorige blog):** Create Group --> Ungroup --> Create Assembly. Je hebt na het ungroupen namelijk ook alle geneste families geselecteerd.

![15_Schoorsteen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/15_Schoorsteen.png)

Probeer het aantal merken te beperken door de elementverdeling slim te kiezen.

**10. HSB elementtekening**

![11_HSB_elementtekening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/11_HSB_elementtekening.png)

![17_Schuin_Element_Panlatten](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/17_Schuin_Element_Panlatten.png)

**Schedules**

![18_Schedule](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/18_Schedule.png)

**11. Dynamo scripts**
De opzet van het Dynamoscript is om op basis van een templatesheet andere assemblies automatisch te voorzien van een opmaak. Dit is het project van mijn collega Piet Mol. Wellicht dat we hier nog een Dynamopackage van gaan maken.

![14_Dynamo_Sheet_Template](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-01-05/14_Dynamo_Sheet_Template.png)

Handige packages: Steamnodes, Spring Nodes, Clockwork en Archi-lab.

**Dataset behorend bij deze blog is hier te downloaden:**<br>
[https://github.com/DutchSailor/blog/tree/master/Bouwtechniek%20%26%20Revit/2019-01%20HSB%20deel%203](https://github.com/DutchSailor/blog/tree/master/Bouwtechniek%20%26%20Revit/2019-01%20HSB%20deel%203)

[Families, Revit-bestand en Dynamo Scripts.](https://www.blogger.com/)