---
layout: post
title: "Paalsymbool in schedule"
date: 2014-06-09 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/1_shared_parameter.png'
published: true
---

# Paalsymbool in schedule

Een van de verbeteringen in Revit 2015 is dat je een afbeelding in schedule kunt laten zien. Dit werkt op het moment dat je deze op een plotblad(sheet) plaatst. Een denkbare toepassing is mogelijk voor het palenplan met de palenstaat. Het paalsymbool is hierbij de afbeelding.

1. Maak een shared parameter van het type 'Image'  aan.

![1_shared_parameter](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/1_shared_parameter.png)

2. Voeg deze toe aan de categorie ' Structural Foundations'

![2_shared_parameter](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/2_shared_parameter.png)

3. Voeg vervolgens plaatjes toe als paalsymbool. In het voorbeeld bestand heb ik er 15 toegevoegd. (6 voor ronde palen, 9 voor rechthoekige)

![3_kies_paalsymbool](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/3_kies_paalsymbool.png)

4. Voeg de parameter toe aan de schedule voor de palenstaat en zie daar het resultaat.

![4_palenplan_schedule](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/4_palenplan_schedule.png)

5. Op het plotblad staan nog 2 schedules voor het weergeven van het totale aantal palen en het peil t.o.v. NAP. 

![5_overig](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-06-09/5_overig.png)

Klik [hier](http://www.3bm.cloud/dutchrevitblog/14_palenplan.rvt) om het project te downloaden met de paalfamily en dit voorbeeld.

tags: paal, schedule, image, pile