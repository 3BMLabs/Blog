---
layout: post
title: "QR-codes op tekening"
date: 2016-07-25 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "-"
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_1_3D.png'
published: true
---

# QR-codes op tekening

**QR-codes op tekeningen**<br>
QR-codes zijn erg handig voor toepassingen op tekeningen is mijn recente ontdekking. Een beetje aan de late kant overigens want het wordt al op veel plaatsen gebruikt. Onderstaand een leuk voorbeeld.

![25_1_3D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_1_3D.png)

Een drijvende woning

![25_2_location-view](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_2_location-view.png)

Het is een hsb-opbouw op een drijvende betonbak. Op alle elementtekeningen staan 2 qr-codes. 1 code verwijst naar de tekening(deze kun je dan op je telefoon/tablet zien). De andere code laat bovenstaande 3D-view zien waardoor je weet waar het hsb-element in het gebouw zit.

Daarnaast zijn er stickers voor alle elementen waarop een qr-code staat. Op de bouw kan iemand deze code scannen en dan ziet hij de positie van het element in het gebouw.

![25_3_elementtekening](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_3_elementtekening.png)

![25_4_qr-codes](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_4_qr-codes.png)

Ik zou zeggen: probeer het even uit!

**Wat is hier nu een handige workflow voor?**<br>
1. Maak met dynamo een lijst van alle assemblies. Gebruik de package **QRcoder** om qr-codes te kunnen maken. Schrijf deze weg(Image.WriteToFile). Verwijs naar een locatie op het web die je kunt gebruiken.
2. Het plaatsen van de qr-codes op de sheet is me nog niet gelukt met dynamo. Maar het zou moeten kunnen denk ik.
3. Vervolgens maak je met een dynamo een script die voor elke assembly een 3D-view maakt en met override elements in view de assembly rood maakt en voorziet van een tag.
4. Deze 3D-views ook weer exporteren met Dynamo.
5. Plaats de 3D-locatie views op het internet(bijvoorbeeld je website) o.i.d.
6. Maak in access een tabel waar je de assemblies en de link naar de qr-code zet(deze kan ook automatisch met dynamo gemaakt worden)

![25_5_tabel_database](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_5_tabel_database.png)

Maak een query waarbij je de projectinformation ook toevoegd vanuit de database van het revit-model.

![25_6_query](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_6_query.png)

Maak een report om de query uit te lezen

![25_7_report](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_7_report.png)

![25_8_report2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_8_report2.png)

En vervolgens heb je een rapport die je als stickervel kunt printen en op elk element kan plakken. Op de bouw kan iedereen met een telefoon zien waar het desbetreffende element hoort.

En tot slot onderstaand een van de hsb-elementen in productie.

![25_9_foto](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2016-07-25/25_9_foto.png)

Een andere toepassing is het koppelen van de qr-code aan een link naar een 3D-dwf-model op autodesk A360. Helaas is dit nog niet te automatiseren van met dynamo voor zover ik kan nagaan.

Je zou hiermee een 3D-model van de plattegrond als dwf kunnen exporteren en met een qr-code naar verwijzen vanaf de tekening.