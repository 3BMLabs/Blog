---
layout: post
title: "Constructietekeningen in Revit deel 2"
date: 2012-11-17 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download.png'
published: true
---

# Constructietekeningen in Revit deel 2

### **3.1 Arcering van wanden, kolommen onder de vloer**
Het is wel zo prettig om bij tekeningen van betonconstructies in plattegrond de wanden en kolommen onder de vloer gearceerd te hebben. Er zijn verschillende manieren waarop dit gedaan wordt. Vaak word ter plaatse gestort beton boven het vloerniveau  voorzien van een solid arcering grijs RGB 192-192-192.
Onder de vloer een lijnarcering onder 45 graden.

![download6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download6.png)

Als er zowel een wand boven als onder de vloer zit zijn beide arceringen aanwezig. Verder worden betonwanden, betonbalken en kolommen onder de vloer gestippeld weergegeven.

Dit laatste gaat automatisch in Revit Structure als de visual style van een view op 'hidden line' staat en de discpline op 'structural'.

Het arceren van wanden en kolommen onder de vloer en boven de vloer is niet mogelijk in 1 view. De manier waarop Revit een plattegrond maakt is namelijk: doorsnijden op een bepaalde hoogte en een stuk naar beneden kijken.

Zie volgende link voor meer info:<br> 
[http://docs.autodesk.com/REVIT/2010/ENU/Revit%20Architecture%202010%20Users%20Guide/RAC/images/BSD/Revit_2010/English/PNG/rvt_illus_viewrangeplan.png](http://docs.autodesk.com/REVIT/2010/ENU/Revit%20Architecture%202010%20Users%20Guide/RAC/images/BSD/Revit_2010/English/PNG/rvt_illus_viewrangeplan.png)

Verder is het zo dat de arceringen binnen Revit aangemaakt worden met .pat-files. Hierin kun je een solid en lijnarcering niet combineren.

Dit probleem is gelukkig wel op te lossen en wel als volgt:<br>
- Maak een extra view van een bepaalde verdieping aan.
- Zet alle categorieen in de 'Visibility Graphics Overrides' uit, behalve 'Structural Columns' en 'Walls'.
- Snij de plattegrond door op 1 meter onder vloerniveau.
- Maak een filter aan voor 'structural columns en walls' en definieer een eigenlijk waarmee je alle betonkolommen en wanden kunt 'vangen', bijvoorbeeld:
    - Typename
    - 'Contains'
    - 'beton'
    - AND
    - Typename
    - 'does not contain'
    - prefab'

![download](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download7.png)

- Override deze filter met'
    - Cut lines pattern: 'hidden'
    - Cut pattern: 'diagonal'
    - Transparant: 'yes' 

![download](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download8.png)

- Maak nog een filter aan die alle wanden en kolommen die niet van beton zijn onzichtbaar maakt. Dit kun je doen door een inverse filter te maken.
    - Typename 
    - 'Does not contain'
    - 'beton'

Zet deze filter uit.

Vervolgens kun je deze 2 views op 1 blad over elkaar heen plaatsen.

![download](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download9.png)

Je kunt hier een viewtemplate van maken zodat deze gemakkelijk op meerdere views van toepassing is te verklaren.

### **3.2 Solid arcering van dragende lateien in steenachtige wanden onder de vloer**

Sommige mensen geven er de voorkeur aan om dragende lateien in steenachtige wanden boven de vloer in een solid-arcering te laten zien. Dit heeft als voordeel dat je ze gemakkelijk kunt herkennen.

![download](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2012-11-17/download10.png)

Ik heb er wat mee ge-experimenteert. Onder meer het volgende geprobeerd:<br>
- Detail item genest in een 'structural framing' latei en deze op een bepaalde hoogte boven de vloer laten weergeven. Dit werkte echter niet in alle situaties. Onder meer als er weer een metselwerkwand boven stond.

Uiteindelijk heb ik er toch weer een aparte view van gemaakt die alleen de lateien laat zien. Deze word in het plotblad weer op elkaar geplaatst.

**Werkvolgorde:**<br>
- Maak nieuwe view aan.
- Zet in de 'Visibility Graphics Overrides' alle categorieen, behalve 'structural framing' uit.
- Maak een filter aan waarmee je alles 'vangt' behalve prefab betonlateien
- Bijvoorbeeld:
    - Typename 
    - does not contain
    - 'latei'
- Override de surface pattern met een solid arcering RGB 128-128-128
- Plaats over een andere view in je plotblad.

De prefab betonlatei bevat ook een 'void' zodat je met 'cut geometrie' gemakkelijk de opening weg kan snijden. De family is zo gemaakt dat je deze ook kunt nesten in een kozijnfamily of kozijnopeningfamily en mee kunt laten wijzigen qua afmeting.