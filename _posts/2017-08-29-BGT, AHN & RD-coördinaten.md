---
layout: post
title: "BGT, AHN & RD-coördinaten"
date: 2017-08-29 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "BGT, AHN & RD-coördinaten, GIS2BIM package"
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_11.png'
published: true
---

# BGT, AHN & RD-coördinaten, GIS2BIM package

Het blijft fantastisch om te allerlei data in Revit in te laden! Er is zo veel beschikbaar. Deze keer een lange blog over allerlei zaken op het gebied van het inlezen van omgevingsinformatie.

Allereerst het resultaat:

**Stap 1**<br>
-Vul locatiegegevens in(invoervelden zijn gemaakt met data-shapes package en werkbalk is gemaakt met dyno: [http://prorubim.com/en/tools/dyno/](http://prorubim.com/en/tools/dyno/))

![30_24](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_24.png)

**Stap 2**<br>
Klik op 'KadasterBAG'.

![30_25](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_25.png)

**Stap 3**<br>
Haal een kop koffie.

![30_26](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_26.png)

Je hebt het BAG, het kadaster en de luchtfoto 2016 op het RD-stelsel in Revit.

**Stap 4**<br>
Klik op BGT en haal nog 2 bakken koffie.

![30_11](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_11.png)

En daar is het BGT(nog niet volledig) als vectordata(lijnen en filled regions) op schaal in Revit.

**In deze blog komen aan de orde:**
1. GIS2BIM Dynamo Package.
2. Mogelijkheden voor het inladen van GIS informative.
3. Locatieserver v3.
4. Uitgebreider gebruik van BAG-informative.
5. BGT inlezen via GML met Python.
6. Luchtfoto via WMS inladen.
7. Shared coördinates en RD-coördinaten.
8. Ideëen en toekomst.

## **1. GIS2BIM Dynamo Package**
Het kader van 'delen is vermenigvuldigen' heb ik een Github project aangemaakt waarin alle hierboven genoemde nodes staan en support files. Er zijn nog tal van verbeteringen mogelijk en noodzakelijk. Van harte uitgenodigd om mee te doen!<br>
De package is te downloaden via de package manager in Dynamo<br>
Documentatie is te vinden op: [https://github.com/DutchSailor/GIS2BIM/wiki/Nodes-version-0.3](https://github.com/DutchSailor/GIS2BIM/wiki/Nodes-version-0.3)<br>
In de 'extra' map van de package zijn de voorbeeldworkspaces te vinden.

## **2. Mogelijkheden voor het inladen van GIS informatie**
We kunnen op een aantal manieren GEO-informatie inlezen. 

1 ) Via WFS(vectordata vanuit een webserver)<br>
**Voorbeeld:** Kadaster, Ruimtelijke plannen, BAG

Je doet een webrequest aan een server om gegevens te ontvangen van een bepaalde regio. Je krijgt als resultaat een xml met onderandere polygonen en metadata die omgezet kunnen naar lijnen, teksten, solids enzovoorts.

2 ) Via WMS(rasterdata vanuit webserver)<br>
**Voorbeeld:** Luchtfoto

Je doet een webrequest aan een server om gegevens te ontvangen van een bepaalde regio. Je krijgt als resultaat een png, jpg enz. Deze kun je in Revit inladen.

3 ) Via gedownloade xml/gml/laszip-bestanden<br>
**Voorbeeld:** BGT, AHN

Je kunt de BGT in delen van 2 bij 2 km(of groter downloaden). Je krijgt dan GML-bestanden. Deze kun je inlezen en omzetten naar lijnen, teksten, solids enzovoorts.

4 ) Via WMTS(rasterdata, vooraf gegeneerde tiles)<br>
**Voorbeeld:** Diverse

Lijkt op WMS. Het verschil is dat WMTS vooraf gegenereerde tiles zijn waar je er dus een x-aantal van wilt downloaden afhankelijk van de grootte van het gewenste gebied waar je in bezig bent en deze vervolgens samenvoegen.

In de GIS2BIM-package zijn voor alle methoden diverse nodes opgenomen.

## **3. Nieuwe locatieserver**

Er is een nieuwe versie van de locatieserver gelanceerd.<br>
[https://pdokforum.geonovum.nl/t/nieuwe-versie-locatieserver-v3-is-beschikbaar/647](https://pdokforum.geonovum.nl/t/nieuwe-versie-locatieserver-v3-is-beschikbaar/647)<br>
Deze is verwerkt in de node GetLocationdataNetherlands.<br>
Overige verbeteringen in de GetLocation-node: Kadastraal perceel, sectie, lengtegraad en breedtegraad zijn uit te lezen.

![GIS2BIM.GetLocationdataNetherlands](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.GetLocationdataNetherlands.png)

Verder is er een node met een aantal geoservices.

![30_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_4.png)

## **4. Uitgebreider gebruik van BAG-informative**

Er is er een BAG:pand en een BAG:gebruiksobject. Een pand kan meerdere gebruiksobjecten bevatten.(appartementen bijvoorbeeld) Voor de pandgeometrie willen we BAG:pand gebruiken en voor de huisnummers en onderstaande informatie BAG:gebruiksobject.

![30_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_3.png)

Er zijn meerdere opties om gebruik te maken van de BAG-informatie.

1) 3D families aanmaken met Dynamo, parameters aanmaken en de bovenstaande informatie hierin wegschrijven.<br>
2) Informatie als losse text in een view plaatsen.

Optie 1 is vanuit BIM-oogpunt wenselijk, alleen nogal langzaam als je bijvoorbeeld 400 panden hebt in de omgeving. Revit gaat namelijk 400 families maken en vervolgens plaatsen. Dit heeft even wat tijd nodig. Vandaar dat beide opties soms handig zijn.
Je kunt dan wel huisnummers, bouwjaar e.d. taggen en een kleur geven op basis van het bouwjaar zoals hieronder te zien is.

![30_6a](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_6a.png)

Optie 2 is met name handig om gewoon een situatietekening in 2D te maken.

![30_4a](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_4a.png)

Hierboven het resultaat van BAG:pand met teksten en filled regions.

![30_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_5.png)

Hierboven de dynamocode. De customnodes zijn in de GIS2BIM-package te vinden.

Het vervolg is om de informatie van de wegen e.d. in Revit te laden.

## **5. BGT inlezen via GML met Python**
Het BGT is helaas niet als webservice beschikbaar. Het is echter wel te downloaden en in te lezen in Revit. Je kunt een deel downloaden via deze [link](https://www.pdok.nl/nl/producten/pdok-downloads/download-basisregistratie-grootschalige-topografie).

![30_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_6.png)

Er is een node om automatisch de BGT-data te downloaden: GIS2BIM.DownloadBGTData. Hiervoor maak je gebruik van GIS2BIM.GetMortonCodeCoordinate. Deze maakt met behulp van bitshifting een mortoncode: [https://en.wikipedia.org/wiki/Z-order_curve](https://en.wikipedia.org/wiki/Z-order_curve)

![GIS2BIM.DownloadBGTData](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.DownloadBGTData.png)

Deze code kun je gebruiken om het desbetreffende deel van de BGT te downloaden.
Vervolgens is er een node om het zip-bestand uit te pakken.

Het BGT omvat een heel aantal GML-bestanden. Voor elke laag een apart bestand:

![30_7](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_7.png)

Sommige GML-bestanden bevatten een punt en bijbehorende informatie(bomen, verkeersborden e.d.)

![30_8](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_8.png)
<br><br><br>
![30_9](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_9.png)

Andere bevatten polygonen, zoals hierboven. Dit betreft het spoor.

Het geheel gaan we omzetten met Dynamo. Het blijkt best wel een dingjetje te zijn om grote xml of gml-bestanden in Dynamo in te laden en daar bewerkingen op uit te voeren. De hierboven genoemde GML-bestanden hebben soms meer dan 100.000 of meer punten. De truc is om deze GML-bestanden te filteren op basis van een boundingbox alvorens deze om te zetten naar geometrie.

Je kunt dit in Dynamo doen met point in Polygon. Maar dan heb je eerst al geometry gemaakt voordat je deze gaat filteren. Dit is heel erg traag en het geheel loopt regelmatig vast.

Het bleek veel sneller om dit met Python te doen. Bekijk de node GIS2BIM.FilterGML om de code te bekijken.

Binnen de BGT zijn er allerlei lagen. Zowel polygonen als punten.
Via deze [link](http://schemas.geonovum.nl/imgeo/2.1/imgeo-2.1.1.xsd) is te zien welke informatie in welke laag opgeslagen is.

Hieronder een tussenstand met wat nu in GIS2BIM-package zit.

**Panden(filled region)**<br>
bgt_overigbouwwerk

**Groen(filled region)**<br>
bgt_begroeidterreindeel

**Lijnen(Detaillines, aparte lagen)**<br>
bgt_functioneelgebied<br>
bgt_gebouwinstallatie<br>
bgt_kunstwerkdeel<br>
bgt_onbegroeidterreindeel<br>
bgt_ondersteunendwegdeel<br>
bgt_overigescheiding<br>
bgt_scheiding<br>
bgt_spoor<br>
bgt_tunneldeel

**Wegen bruggen en kunstwerken(filled region)**<br>
bgt_kunstwerkdeel<br>
bgt_overbruggingsdeel<br>
bgt_wegdeel

**Water(filled region)**<br>
bgt_ondersteunendwaterdeel<br>
bgt_waterdeel

**Labels(text)**<br>
bgt_openbareruimtelabel

**Puntobject(2d detailcomponent)**<br>
bgt_vegetatieobject

**Nu nog niet meegenomen**<br>
bgt_bak<br>
bgt_bord<br>
bgt_buurt<br>
bgt_installatie<br>
bgt_kast<br>
bgt_mast<br>
bgt_ongeclassificeerdobject<br>
bgt_openbareruimte<br>
bgt_paal<br>
bgt_put<br>
bgt_sensor<br>
bgt_straatmeubilair<br>
bgt_waterinrichtingselement<br>
bgt_wijk

![30_10](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_10.png)

We gaan de GML vertalen naar:<br>
1) Filled Regions<br>
2) Detail Lines<br>
3) Texten


Dat ziet er als onderstaand uit:(labels werken nog niet)

![GIS2BIM.BGT2D](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.BGT2D.png)

Onderstaand het resultaat

![30_11](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_11.png)

Het BAG komt dus via een WFS-webrequest en de BGT via een filtering van een automatische download van de gml-bestanden.

Even het adres wijzigen. Zie daar het resultaat!

![30_13](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_13.png)

Je kunt overigens natuurlijk ook gemakkelijk families maken van de data, alleen het wordt dan snel traag. Het zijn al snel bijvoorbeeld 10.000-50.000 lijnen en componenten e.d.

## **6.Luchtfoto via WMS inladen!**
We kunnen ook WMS data inladen.<br>
Je kunt een webrequest formuleren, bijvoorbeeld voor het inladen van luchtfoto van 2016.<br>
De delen van het webrequest zien er als volgt uit:

![30_14](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_14.png)

Bekijk het voorbeeld alvast via [link](http://geodata.nationaalgeoregister.nl/luchtfoto/rgb/wms?&request=GetMap&VERSION=1.3.0&STYLES=default&layers=2016_ortho25&bbox=104547,425048,105047,425548&width=2000&height=2000&format=image/png&crs=EPSG:28992). Werkt niet goed in Edge, wel in Firefox en Google Chrome.

Op basis van een boundingbox van RD-coördinaten maken we opnieuw een webrequest. De standaard webrequest-node van Revit functioneerd hier niet. Deze geeft namelijk direct een textfile als resultaat. We doen de webrequest daarom met Python.

![30_19](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_19.png)

En dat werkt, zie hieronder. Het bestand wordt tijdelijk ergens opgeslagen.

![30_15](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_15.png)

Vervolgens importeren we het bestand in een view. Dit ook weer met Python. Met dank aan Konrad Sobon. Zie de discussie op: [http://dynamobim.com/forums/topic/is-it-possible/](http://dynamobim.com/forums/topic/is-it-possible/)

![30_16](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_16.png)

Vervolgens stellen we de breedte van de rasterimage in conform de werkelijke breedte.

![30_17](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_17.png)

En vervolgens is deze op schaal en juiste positie in de view geplaatst!

![30_18](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_18.png)

Nu we het raamwerk van een WMS-request hebben kunnen we alle WMS-data die je maar kunt bedenken met 1 druk op de knop in Revit inladen.

Zoals bijvoorbeeld de CBS statistieken voor de WOZ-waarde van woningen:

Getcapabilitieslink: [http://geodata.nationaalgeoregister.nl/cbsvierkanten100mv2/wms?&request=GetCapabilities&service=WMS](http://geodata.nationaalgeoregister.nl/cbsvierkanten100mv2/wms?&request=GetCapabilities&service=WMS)

**Resultaat:**

![30_22](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_22.png)

**Legenda:**

![30_21](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_21.png)

## **7.Shared coördinates en RD-coördinaten**
Aangezien al de GIS-informatie die we gebruiken op RD-coördinaten staat kunnen we ook de RD-coördinaten uitlezen. Dit kan door het Surveypoint te verplaatsen.

![30_20](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_20.png)

Ook deze zit inmiddels in een GIS2BIM-node.

![GIS2BIM.SetSharedCoordinate](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.SetSharedCoordinate.png)

![30_23](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/30_23.png)

En vervolgens kun je overal rd-coordinaten uitlezen.

## **8. Ideëen en toekomst**

Wat nog meer allemaal mogelijk is:
- [http://topotijdreis.nl/](http://topotijdreis.nl/) met WMTS importeren(als bouwhistorie achtergrond)
- Bekijken of een pand een rijksmonument is; in een risicogebied voor funderingsproblemen ligt enz. enz.
- Topography maken op basis van ahn-pointcloud en deze voorzien van een WMS luchtfoto als rendermateriaal.

![GIS2BIM.example2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.example2.png)

- Google API en Open Streetmap gebruiken als webrequest

![6_6_result](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/6_6_result.png)

- WMTS webrequest voor bijvoorbeeld infrarood luchtfoto's.

![GIS2BIM.WMTSCombineImages](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.WMTSCombineImages.png)

![GIS2BIM.WMTSLayersNetherlands](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.WMTSLayersNetherlands.png)

- GEF importeren in Revit op basis van een willekeurig polygon. Dit najaar komt het dinoloket als wfs-service beschikbaar.

![GIS2BIM.GEFCPTTo3DSoilLayers](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/GIS2BIM.GEFCPTTo3DSoilLayers.png)

- In het BGT zitten definities van verkeersborden, lantaarnpalen, riooolputten, betaalautomaten, brievenbussen e.d. Je zou hier een hele serie 3D-families voor kunnen maken die automatisch geplaatst worden op basis van de desbetreffende GML. 
- QGIS via een python-script gebruiken om data in te lezen.
- **Locatierapportage**. Bij start van een project run je een mega-script waarbij honderden WMS en WFS-services bevraagd gaan worden. Onder andere geluid, natura2000, milieu, vleermuizen enzovoorts. Je zou hier nog een risico-analyse aan kunnen koppelen.
- KLIK-data inladen en omzetten naar vectordata.

Handige leerpunten. Ik ben nu steeds meer dingen in Python aan het doen in plaats van in Dynamo. Een paar tips:

1) IronPython 2.7 is **niet** hetzelfde als Python 2 of 3. IronPython is implementatie van Python voor .NET. Dat betekend dat je heel Python libraries niet kunt gebruiken in IronPython.

2) Een zeer handige manier om je Pythonscript te testen is PyCharm. [https://www.jetbrains.com/pycharm/](https://www.jetbrains.com/pycharm/) Let op dat je de interpreter op IronPython 2.7 zet en dus **niet** op Python 2 of 3.

3) Je kunt daardoor wel gebruik maken van de gehele .NET omgeving. Bijvoorbeeld de ZipFile Class.<br>
[https://msdn.microsoft.com/en-us/library/system.io.compression.zipfile%28v=vs.110%29.aspx](https://msdn.microsoft.com/en-us/library/system.io.compression.zipfile%28v=vs.110%29.aspx)

Om gebruik te maken van .NET moet je via clr.AddReference the desbetreffende Assembly en Namespace aanroepen.

clr.AddReference("**ASSEMBLY**")<br>
from **NAMESPACE** import **CLASS**

![code](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-08-29/code.png)

