---
layout: post
title: "Revit ODBC en Microsoft Access"
date: 2015-09-25 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "De mogelijkheden van Revit en de export naar een database."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_dbase.jpg'
published: true
---

# Revit ODBC en Microsoft Access

Bijgaand weer eens een blog. Deze keer over de mogelijkheden van Revit en de export naar een database.

![16_dbase](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_dbase.jpg) 

Vanuit Revit kun je via een [ODBC](https://nl.wikipedia.org/wiki/Open_DataBase_Connectivity)-driver exporteren naar verschillende databaseformaten. Afhankelijk van welke op je PC geinstalleerd zijn. In deze blog gebruiken we een MS Access-driver. [Microsoft Access](https://nl.wikipedia.org/wiki/Microsoft_Access) is een vrij toegankelijk programma voor het lezen van databases, maken van [query's](https://nl.wikipedia.org/wiki/Query), rapporten en formulieren.

Het resultaat is [hier](http://www.3bm.cloud/dutchrevitblog/RevitData.accdb) te downloaden. Let op dit is een niet een afgeronde versie, maar meer wat ideeën in een programma gestopt.

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

## **1) Database algemeen.**

Even kort iets over databases. In een database zijn gegevens op een gestructureerde manier opgeslagen.
Er zijn allerlei database-ontwerpen en systemen. Hier betreft het een relationele database.<br>
Enkele typen databases zijn:<br>
-SQL-server<br>
-MySQL<br>
-MariaDB<br>
-Access

In deze blog gebruik ik Microsoft Access omdat dat programma tevens een [databasemanagementsysteem](https://nl.wikipedia.org/wiki/Databasemanagementsysteem) is.<br>
-Verder kun je op met Microsoft Access formulieren en rapporten maken zonder al te veel programmeerwerk.<br>
-Ook kun je een van een Access-Database eenvoudig een applicatie maken die je met meerdere gebruikers tegelijk kunt gebruiken binnen een lokaal netwerk.<br>
-Verder werkt Access goed samen met SQL-server.(en Azure-sql-servers)<br>
-Je kunt een accessdatabase opsplitsen in een front-end(formulieren, rapporten, interface, queries) en een backend(tabellen).<br>
-Een nadeel is dat access niet slim met zijn netwerkgebruik omgaat. Als je dus op afstand met meerdere mensen in 1 database werkt, is het heel erg traag. In dat geval kun je beter andere software gebruiken.

Wat zijn tabellen, queries, formulieren en rapporten?

In een **tabel** ligt de feitelijke data vast. Kolommen zijn 'velden'. Rijen zijn 'records'. Een record is een verzameling van ingevulde velden met een unieke 'ID'. Dit kunnen bijvoorbeeld ruimten zijn(i.g.v. een revit-database export).

![16_2_algemeen_datbases](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_2_algemeen_datbases.png) 

Een **query** vraagt data op uit een databasetabel en kan meerdere tabellen combineren. In access kun je grafisch queries maken maar ook met SQL. [SQL](https://nl.wikipedia.org/wiki/SQL) staat voor Structured Query Language. 

Een voorbeeld van SQL-taal: <br>
SELECT * FROM Rooms WHERE Area < 15;<br>
Dit geeft een query met alle ruimten waar de oppervlakte kleiner is dan 15 m2.

Een **formulier** kan gebruikt worden om data in te vullen. Dit zijn velden, vinkjes, waarden enz.

Een **rapport** geeft vervolgens een uitdraai van bepaalde data(een brief, factuur, tekeninglijst e.d.)

## **2) Export vanuit Revit**

Dit kan op 2 manieren.<br>
1) Via 'file' ODBC

![16_0_revit_to_dbase_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_0_revit_to_dbase_1.png) 

2) Via import/export database addin. <br>
Hierbij kan gemanipuleerde data dus terug je revit-model ingelezen worden.

![16_1_revit_to_dbase](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_1_revit_to_dbase.png) 

Na wat doorklikken e.d. kun je een 'mdb-bestand' aanmaken. Dit is een bestand met alle tabellen vanuit Revit. Onderstaand zie je tabel 'Walls'. Hierin staan alle wanden uit het model met de eigenschappen en shared parameters uit het Revit-model.

![16_2_access](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_2_access.png) 

## **3) Aparte beheerdatabase**
Omdat je natuurlijk elke keer een nieuwe export maakt voor andere modellen is het niet handig om queries e.d. in de geexporteerde database te maken. Dat ben je namelijk de volgende keer kwijt.

Maak een nieuwe access-database aan. Link hierin de tabellen uit de database die je uit Revit hebt geexporteerd.

![16_3_access_link_tables](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_3_access_link_tables.png) 

Je kunt even een leuk startup formulier maken met knoppen.

![16_4_access_form](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_4_access_form.png) 

Achter de knop 'Choose Database' hangt een stukje VBA-code die ervoor zorgt dat je een schermpje krijgt waar je een database kunt kiezen.

![16_4_vba-startup](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_4_vba-startup.png) 

Vervolgens krijg je een venster waar je het pad van je revit-database kiest. Na het klikken van OK worden alle tabellen vernieuwd.

De gelinkte tabellen zijn voor Revit2016. Er zitten wat veranderingen in de tabellen tussen Revit2015 en Revit2016. Dit zorgt voor problemen bij het 'herlinken' van tabellen.

![16_4_choose_dbase_location](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_4_choose_dbase_location.png) 

## **4) Tekeninglijst en projectinformatie**
Met behulp van een 'form'  in access kun je eenvoudig een formulier maken waar alle projectinformatie op weergegeven staat.

![16_5_form_projectinformation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_5_form_projectinformation.png) 

De projectinformatie staat in de tabel 'ProjectInformation' bestaand uit 1 record.

![16_6_form_projectinformation2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_6_form_projectinformation2.png) 

Vervolgens maak je een formulier waar je alle parameters aan een veld kunt koppelen. Deze kun je vervolgens invullen.

**Idee 2:** Tekeninglijst

![16_7_query_sheets](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_7_query_sheets.png) 

Maak een query van sheets.

![16_8_query_uitgevoerd](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_8_query_uitgevoerd.png) 

Zie hierboven het resultaat van de query.

![16_9_report_tekeninglijst](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_9_report_tekeninglijst.png) 

Je kunt met de knop 'Report' in access op de 'grote-stappen-snel-thuis'-methode een eenvoudig rapport maken. Hierover de werkopmaak met koptekst, detailgedeelte(hier herhalen de records zich) en voetttekst.

![16_10_report_tekeninglijst2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_10_report_tekeninglijst2.png)

Hierboven het resultaat. De opmaak is uiteraard nog te verbeteren. Dit kun je eenvoudig afstemmen op de bedrijfsstandaard.

## **5) Daglichtrapportage**

![16_11_daglicht_tabel_eisen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_11_daglicht_tabel_eisen.png)

We gaan nu een daglichtrapportage maken vanuit de revit-database.
Bovenstaand heb ik eerst een algemene tabel gemaakt met de verschillende gebruiksfuncties en hun daglichteisen. Onder RevtiGGDescription staat de naam die gebruikt wordt volgens de RevitGG-standaard bij ruimten.

![16_12_daglicht_qry_daglichteisen](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_12_daglicht_qry_daglichteisen.png)

Vervolgens maken we een query die eigenlijk het volgende doet:<br>
-Maakt een lijst van de verblijfsruimten in het revitmodel en berekend hoeveel daglichtoppervlakte er nodig is:<br>
Onderstaande SQL-instructie(de WHERE van DesignOptions.Name is projectspecifiek en normaal gesproken niet nodig).

SELECT Rooms.Id, Rooms.Name, Rooms.Area, Rooms.BouwbesluitRuimtefunctie, S02_gebruiksfuncties_RK.KeyName, tblBbGebruikfunctieTypes.DaylightAreaMinimum, tblBbGebruikfunctieTypes.DaylightPercentage, [Area]*[DaylightPercentage] AS MinDayLightArea, Levels.Name
FROM (tblBbGebruikfunctieTypes INNER JOIN S02_gebruiksfuncties_RK ON tblBbGebruikfunctieTypes.Description2 = S02_gebruiksfuncties_RK.KeyName) INNER JOIN (Levels RIGHT JOIN (DesignOptions RIGHT JOIN Rooms ON DesignOptions.Id = Rooms.DesignOption) ON Levels.Id = Rooms.Level) ON S02_gebruiksfuncties_RK.Id = Rooms.Gebruiksfunctie
WHERE (((Rooms.Area)>0) AND ((Rooms.BouwbesluitRuimtefunctie)="verblijfsruimte") AND ((DesignOptions.Name) Is Null)) OR (((Rooms.BouwbesluitRuimtefunctie)="verblijfsruimte ") AND ((DesignOptions.Name)="Optie 2"));

![16_13_daglicht_qry_daglichteisen2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_13_daglicht_qry_daglichteisen2.png)

De 2e query kijkt via 'RoomFromToAssocations'  welke Windows in welke ruimten aanwezig zijn. Hij filter de 'glas-window-family's' eruit. Dit kan per tekenstandaard verschillen. De oppervlakte van het glas wordt berekend vanaf 600 mm boven het desbetreffende vloerniveau.

Dit geeft het volgende resultaat.

![16_14_daglicht_qry_daglichteisen3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_14_daglicht_qry_daglichteisen3.png)

![16_15_query_controle_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_15_query_controle_1.png)

De 3e query combineerd de eerste 2 queries

En geeft een lijst per ruimte die laat zien of de daglichtseis voldoet.

![16_16_query_controle_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_15_query_controle_1.png)

![16_17_frontpage_report](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_17_frontpage_report.png)

Vervolgens maken we een rapport. De 1e pagina komt uit de tabel 'ProjectInformation'

De 2e pagina laat de laatste query zien met wat algemene tekst ervoor.

![16_18_2e_pagina_report](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_18_2e_pagina_report.png)

Dat ziet er vervolgens zo uit.

![16_19_2e_pagina_report_plotview](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_19_2e_pagina_report_plotview.png)

De 3e pagina laat de kozijnen per ruimte zien met hun afmetingen.

![16_20_3e_pagina](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_20_3e_pagina.png)

![16_21_3e_pagina_plotview](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_21_3e_pagina_plotview.png)

Deze 3 zijn als subreport gekoppeld in een report.

## **6) Programmaatje maken: RevitDataHandler 0.1beta** 

In MS Access kun je de Ribbon met opmaak werkbalken verwijderen en vervangen door een eigen 'Ribbon'. Dat kan door een nieuwe tabel te maken en daar met 'xml' een nieuwe ribbon te beschrijven. 

![16_22_usys_ribbon](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_22_usys_ribbon.png)

Dit deze stuur je aan via een VBA-Module BasButton. 

In de options zet je deze Ribbon aan.

![16_23_ribbon_options](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_23_ribbon_options.png)

![16_24_startup_0.1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2015-09-25/16_24_startup_0.1.png)

En vervolgens zie het volgende resultaat als je het programmaatje opent.
Je kunt het [hier](http://www.3bm.cloud/dutchrevitblog/RevitData.accdb) downloaden. 

Misschien is het een idee om hier een opensource project van te maken waar meerdere mensen hun kennis en expertise instoppen.

Waarschuwing: Het is absoluut geen stabiel draaiend programma momenteel. Het is echt een snel opzetje wat ik nu gemaakt heb om te laten zien wat de mogelijkheden zijn.