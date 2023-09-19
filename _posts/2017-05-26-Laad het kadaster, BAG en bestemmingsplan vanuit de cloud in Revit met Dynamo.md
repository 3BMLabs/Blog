---
layout: post
title: "Laad het kadaster, BAG en bestemmingsplan vanuit de cloud in Revit met Dynamo"
date: 2017-05-26 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "Laad het kadaster, BAG en bestemmingsplan vanuit de cloud in Revit met Dynamo"
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_0.png'
published: true
---

# Laad het kadaster, BAG en bestemmingsplan vanuit de cloud in Revit met Dynamo

Een andere manier waarop Dynamo erg interessant is het gebruik maken van Geoservices. In Nederland zijn er honderden beschikbaar zoals:

-Kadaster<br>
-Actueel Hoogte Bestand Nederland<br>
-Basis Administratie Gebouwen<br>
-Bestemmingsplannen<br>
-Waar wel en geen drones mogen vliegen.<br>
-Cultuurhistorische zaken.<br>
-Waterstanden in rivieren.<br>
-enz enz enz.

Gebruik de [PDOK-viewer](http://pdokviewer.pdok.nl/) om te zien wat er allemaal beschikbaar is!

Er is ook een [locatieservice](https://pdokforum.geonovum.nl/t/documentatie-en-voorbeelden-locatieserver/262). In dit voorbeeld gaan we vanuit een adres en een boundingbox gegevens uit het kadaster, BAG en het bestemmingsplan importeren.

De werkmethode voor het kadaster, de bag en het bestemmingsplan verschillen niet zoveel van elkaar. In deze blogaflevering doen we alleen het kadaster.
Download de dynamonodes [hier](http://www.3bm.cloud/dutchrevitblog/Kadaster.zip).

Het stappenplan:

1. Vul adres in.
2. We gebruiken de [PDOK-locatieserver](https://pdokforum.geonovum.nl/t/documentatie-en-voorbeelden-locatieserver/262) om een [RD-coördinaat](https://nl.wikipedia.org/wiki/Rijksdriehoeksco%C3%B6rdinaten) en de postcode op te halen.
3. Vervolgens doen we een webrequest aan de kadaster-server.
4. Als resultaat krijgen we een xml-bestand die we verder gaan uitlezen en omzetten naar curves.
5. De curves verplaatsen we naar het nulpunt van het model en plaatsen detaillines in de actieve view.
6. Aanvullende informatie.

**1. Adres**
We gebruiken bij dit voorbeeld een adres in dordrecht: Oranjelaan 7 Dordrecht.
Hieronder het resultaat van het kadaster, BAG en bestemmingsplan. **Het is echt fantastisch om het bouwvlak uit het bestemmingsplan als vector i.p.v. raster te hebben!!!!!!**

![26_0](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_0.png)

Zwart zijn de kadastrale grenzen.<br>
Groen is het bestemmingsplan<br>
Rood is het BAG.

Het geheel is wel heeeeel erg traag. Als je het BAG, Kadaster en Bestemmingsplan runt voor een boundingbox van 500 meter kan het wel 10 minuten duren voordat alle lijnen getekend zijn. En je hebt regelmatig vastlopers. Sla vooraf op!
De webrequest zelf is relatief snel, maar het omzetten naar lijnen kost veel tijd.


**2. PDOK-locatieserver.**<br>
Er hangt iets in de lucht namelijk de locatieserver. Als je een webrequest doet met de volgende syntax: http://geodata.nationaalgeoregister.nl/locatieserver/free?wt=json&q=PLAATSNAAM and STRAATNAAM and HUISNUMMER
Krijg je als resultaat een bestand in [JSON](https://nl.wikipedia.org/wiki/JSON) retour waarin onder andere het RD-coördinaat en de postcode van dit adres staan. Klik [hier](http://geodata.nationaalgeoregister.nl/locatieserver/free?wt=json&q=dordrecht%20and%20oranjelaan%20and%207) voor een voorbeeld.

We maken hier een Dynamo-Node van.

![26_1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_1.png)

Deze heeft als input de straat, huisnummer, plaats en geeft als resultaat het RD-coördinaat en de postcode.

![26_3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_3.png)

**3. Vervolgens doen we een webrequest aan de kadaster-server.**<br>
Deze webrequest ziet er als volgt uit:

[http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?<br>
&request=GetFeature<br>
&typeName=kadastralekaartv3:kadastralegrens<br>
&bbox=106385,425119,106885,425619](http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?&request=GetFeature&typeName=kadastralekaartv3:kadastralegrens&bbox=106385,425119,106885,425619)

De boundingbox is een rechthoek met linker onderhoek en rechter bovenhoek in RD-coordinaten. We maken een nieuwe node om deze boundingbox te omschrijven.

![26_2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_2.png)

Dat is vervolgens de volgende stap. Stel de link samen waarmee het webrequest gedaan kan worden.
Dit is een kwestie van een string samenvoegen.

![26_4](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_4.png)

Het resultaat is een lang xml-bestand. Klik [hier](http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?%20&request=GetFeature%20&typeName=kadastralekaartv3:kadastralegrens%20&bbox=106385,425119,106885,425619) om deze in je browser weer te geven.

![26_55](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_55.png)

**4,5. XML omztten.**

![26_5](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_5.png)

Bovenstaande code is bedoeld om de xml in een list te krijgen en dan de list een dusdanig formaat te maken dat je hier coördinaten en lijnen mee kunt creëren. Vooral een kwestie van opsplitsen enzovoorts.

De coördinaten uit de xml zijn RD-coordinaten in meters. Deze zijn meer dan 33 kilometer. Helaas is er iemand die ooit bedacht heeft dat je in Revit niet verder dan 33 km hoeft te tekenen/modelleren.
De coördinaten worden dus weer teruggezet naar het nulpunt van het model op basis van de gevonden RD-coördinaat van het adres.

![26_6](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-05-26/26_6.png)

Plekken waar nog heel veel meer informatie te vinden is:

| Website | Informatie |
| - | - |
| [www.nationaalgeoregister.nl](http://www.nationaalgeoregister.nl/) | Een overzicht met vele beschikbare geoservices. |
| [http://pdok-ngr.readthedocs.io/services.html#web-feature-service-wfs](http://pdok-ngr.readthedocs.io/services.html#web-feature-service-wfs) | Uitleg over doen van webrequest en het verschil tussen WMS, WFS, WMTS |
| [https://pdokforum.geonovum.nl/](https://pdokforum.geonovum.nl/) | PDOK-forum |
| [http://docs.geoserver.org/latest/en/user/services/wfs/reference.html#getcapabilities](http://docs.geoserver.org/latest/en/user/services/wfs/reference.html#getcapabilities) | Algemene toelichting over de getcapabilitiesfunctionaliteit. |
| [https://www.pdok.nl/nl/producten/pdok-services/uitleg-over-services](https://www.pdok.nl/nl/producten/pdok-services/uitleg-over-services) | Toelichting op PDOK-services |

**Aanvullende informatie handige geoservices**

De geocoding-services zijn volgens een bepaalde standaard opgebouwd. Als je achter de url van de service **request=GetCapabilities** toevoegd krijg je een xml-bestand met alle mogelijkheden van de desbetreffende geocodingservice.

| Services | GetCapabilities Link | Voorbeeldrequest |
| - | - | - |
| **AHN2**<br>WMS<br>(raster(helaas)) | [https://geodata.nationaalgeoregister.nl/ahn3/wms?request=GetCapabilities](https://geodata.nationaalgeoregister.nl/ahn3/wms?request=GetCapabilities) | [http://geodata.nationaalgeoregister.nl/ahn2/wms?service=WMS&request=GetMap&layers=ahn2_5m&bbox=106385,425119,106885,425619&width=400&height=500&format=image/png&srs=EPSG:28992](http://geodata.nationaalgeoregister.nl/ahn2/wms?service=WMS&request=GetMap&layers=ahn2_5m&bbox=106385,425119,106885,425619&width=400&height=500&format=image/png&srs=EPSG:28992)
| **Kadaster**<br>WFS<br>(vectoren dus) | [http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?&request=GetCapabilities&service=WFS](http://geodata.nationaalgeoregister.nl/kadastralekaartv2/wfs?&request=GetCapabilities&service=WFS) | [http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?&request=GetFeature&typeName=kadastralekaartv3:kadastralegrens&bbox=106385,425119,106885,425619](http://geodata.nationaalgeoregister.nl/kadastralekaartv3/wfs?&request=GetFeature&typeName=kadastralekaartv3:kadastralegrens&bbox=106385,425119,106885,425619) |
| **BAG**<br>WFS<br>(vectoren dus) | [http://geodata.nationaalgeoregister.nl/bag/wfs?&request=GetCapabilities&service=WFS](http://geodata.nationaalgeoregister.nl/bag/wfs?&request=GetCapabilities&service=WFS) | [http://geodata.nationaalgeoregister.nl/bag/wfs?service=wfs&version=2.0.0&request=GetFeature&typeName=bag:verblijfsobject&bbox=106385,425119,106885,425619](http://geodata.nationaalgeoregister.nl/bag/wfs?service=wfs&version=2.0.0&request=GetFeature&typeName=bag:verblijfsobject&bbox=106385,425119,106885,425619) |
| **Ruimtelijke plannen**<br>WFS<br>(vectoren dus) | [http://afnemers.ruimtelijkeplannen.nl/afnemers/services?&request=GetCapabilities&service=WFS](http://afnemers.ruimtelijkeplannen.nl/afnemers/services?&request=GetCapabilities&service=WFS) | [http://afnemers.ruimtelijkeplannen.nl/afnemers/services?&service=WFS&version=1.1.0&request=GetFeature&typeName=app:Bouwvlak&bbox=106385,425119,106885,425619](http://afnemers.ruimtelijkeplannen.nl/afnemers/services?&service=WFS&version=1.1.0&request=GetFeature&typeName=app:Bouwvlak&bbox=106385,425119,106885,425619) |
| **BGT**<br>**Grootschalige Topografie(voormalig GBKN)**<br>WMTS<br>(raster dus helaas) | [http://geodata.nationaalgeoregister.nl/tiles/service/wmts/bgtstandaard?&request=GetCapabilities&service=WMTS](http://geodata.nationaalgeoregister.nl/tiles/service/wmts/bgtstandaard?&request=GetCapabilities&service=WMTS) |  |

**Wat nog beter zou kunnen?**

-De BGT is helaas alleen als WMS-beschikbaar in de cloud. Je kunt het wel [handmatig downloaden](https://www.pdok.nl/nl/producten/pdok-downloads/download-basisregistratie-grootschalige-topografie) en dan importeren maar dat is minder gemakkelijk dan via een webrequest.

-De AHN als pointcloud kunnen benaderen i.p.v. rasterimage. Dan kun je 3D-solids maken van de bouwvlakken.

**Wat voor mogelijkheden zijn er nog meer?**<br>
- De locatieserver geeft ook de coördinaat in L/B. Hiermee kun je dus ook de revit-location goed instellen.<br>
- De huisnummers en kadastrale percelen tekstueel vermelden.<br>
- De percelen inkleuren.<br>
- Het bouwjaar erbij zetten.<br>
- Het soort functie van het bestemmingsplan bouwvlak vermelden.<br>
- 3D bestemmingsplan maken door meer data uit te lezen.<br>
- enzovoorts<br>
- Luchtfoto's downloaden.