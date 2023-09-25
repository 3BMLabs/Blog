---
layout: post
title: "Revit ODBC en Microsoft Access"
date: 2015-09-25 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "De mogelijkheden van Revit en de export naar een database."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-12-18/16_dbase.jpg'
published: true
---

# Revit ODBC en Microsoft Access

Bijgaand weer eens een blog. Deze keer over de mogelijkheden van Revit en de export naar een database.

| ![16_dbase](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_dbase.jpg) | Vanuit Revit kun je via een ODBC-driver exporteren naar verschillende databaseformaten. Afhankelijk van welke op je PC geinstalleerd zijn. In deze blog gebruiken we een MS Access-driver. Microsoft Access is een vrij toegankelijk programma voor het lezen van databases, maken van query's, rapporten en formulieren.

Het resultaat is hier te downloaden. Let op dit is een niet een afgeronde versie, maar meer wat ideeën in een programma gestopt. |

Het voordeel van rapporten in MS Access ten opzichte van 'sheets' in Revit is dat je:<br>
a) Meer parameters tot je beschikking hebt dan in Revit.<br>
b) Rapporten kun je dusdanig inrichten dat deze over meerdere pagina's lopen. Als je in Revit grote schedules hebt kun je die niet makkelijk over meerdere pagina's laten lopen.<br>
c) Belangrijkste: Middels queries kun je veel meer dataverbanden leggen dan je in schedules in Revit kunt doen.

**Achtereenvolgens:**<br>
1) Database algemeen<br>
2) Exporteren vanuit Revit.<br>
3) Linken van tabellen naar aparte 'beheer database'<br>
4) Formulier projectinformatie en het maken van een tekeninglijst.<br>
5) Maken van daglichtrapportage<br>
6) Programmatje maken: RevitDataHandler 0.1beta