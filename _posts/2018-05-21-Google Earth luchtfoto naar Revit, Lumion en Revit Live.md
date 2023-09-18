---
layout: post
title: "Google Earth luchtfoto naar Revit, Lumion en Revit Live"
date: 2018-05-21 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: "Een aanvulling op de vorige blog."
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-10-15/BILT Europe.png'
published: true
---

# Google Earth luchtfoto naar Revit, Lumion en Revit Live

Een aanvulling op de vorige blog.
1. Download een luchtfoto via Google Earth.
2. Gebruik de Revit API om deze foto als rendermateriaal in te stellen.
3. Download een AHN3-bestand. Gebruik poisson surface reconstruction, dynamo naar directshape  en exporteer naar Lumion en Revit Live.

![Workflow](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/Workflow.png)

**1. Downloaden van een luchtfoto in Google Earth.**<br>
Stel je locatie in via 'Location'.

![1SetLocation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/1SetLocation.png)

Als je de GIS2BIM-package versie 0.6 geïnstalleerd hebt kun je in de map '1.3\packages\GIS2BIM\extra\' het bestand 'TMS Example Google.dyn' openen. Of download dit bestand via [github](https://github.com/DutchSailor/GIS2BIM/blob/master/nodes/support/Aerial/GoogleEarthTileMapServiceHighResolution.dyn).

![2GetRevitSiteLocation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/2GetRevitSiteLocation.png)

De node **GetRevitSiteLocation** leest de coördinaten uit de Revit Site Location. De node **CreateBoundingBoxLATLONG** berekend een linker onderhoek en rechterbovenhoek in  geodetische coördinaten in het [WGS-84](https://en.wikipedia.org/wiki/World_Geodetic_System)coördinatensysteem.

![3TMS](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/3TMS.png)

Google Earth gebruikt een protocol wat bijna hetzelfde is als het [TMS-protocol](https://wiki.openstreetmap.org/wiki/TMS) (Tile Map Service).  De node **TMSGetTileNumbersFromBboxLATLON** berekend de nummers van de tegels. De luchtfoto is namelijk opgeknipt in tegels. Voor meer informatie over deze verdeling zie [http://www.maptiler.org/google-maps-coordinates-tile-bounds-projection/](http://www.maptiler.org/google-maps-coordinates-tile-bounds-projection/)

De node **TMSWebServices** maakt op basis van de tilenummers alle directe url-links van alle tiles.
Bijvoorbeeld [deze](https://mt1.google.com/vt/lyrs=s&x=268972&y=173517&z=19).

![4TMSURL](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/4TMSURL.png)

De node **TMS_WMTS_WebrequestAndCombineImages** gaat alle images downloaden en samenvoegen tot 1 afbeelding.

![5TMSWebrequestImage](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/5TMSWebrequestImage.png)

![6SaveImage](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/6SaveImage.png)

Vervolgens kun je de afbeelding opslaan er vervolgens importeren in een view in Revit. Of als materiaal gaan gebruiken.

**2. Revit API 2019 gebruiken om luchtfoto als materiaal in te stellen.**

Er zijn diverse zaken in Revit API 2018.1/2019 gewijzigd waardoor ook materiaaleigenschappen en asseteigenschappen aan te maken en te wijzigen zijn. Voor meer informatie over dit onderwerp zie onder andere:
- [https://thebuildingcoder.typepad.com/blog/2017/11/modifying-material-visual-appearance.html#3](https://thebuildingcoder.typepad.com/blog/2017/11/modifying-material-visual-appearance.html#3)
- [https://thebuildingcoder.typepad.com/files/sd124625_visual_appearance_of_materials_api_boris_shafiro_slides.pdf](https://thebuildingcoder.typepad.com/files/sd124625_visual_appearance_of_materials_api_boris_shafiro_slides.pdf)

Dit geeft ons de mogelijkheid om de luchtfoto op schaal aan het materiaal te hangen.

Veel informatie is te vinden op [www.revitapidocs.com](http://www.revitapidocs.com/). Dit deel valt onder Autodesk.Revit.DB.Visual Namespace.

Ondanks het feit dat ik een beginner ben in programmeren is het me toch gelukt om een stukje Python code te schrijven waar de eigenschappen van een generic asset bij een materiaal in te stellen zijn.

![6_set_material](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/6_set_material.png)

**import** clr<br>
clr.**AddReference**("RevitNodes")<br>
**import** Revit<br>
clr.**ImportExtensions**(Revit.Elements)<br>
clr.**AddReference**("RevitAPI")<br>
**import** Autodesk<br>
**from** Autodesk.Revit.DB __import *__<br>
**from** Autodesk.Revit.DB.Visual __import *__

clr.**AddReference**("RevitServices")<br>
**import** RevitServices<br>
**from** RevitServices.Persistence **import** DocumentManager<br>
**from** RevitServices.Transactions **import** TransactionManager

doc = DocumentManager.Instance.CurrentDBDocument

**import** sys

pyt_path = 'C:\Program Files (x86)\IronPython 2.7\Lib'<br>
sys.path.**append**(pyt_path)

mat1= IN[0]<br>
var1 = IN[1]<br>
offsetX1 = IN[2]<br>
offsetY1 = IN[3]<br>
scaleX1 = IN[4]<br>
scaleY1 = IN[5]<br>
lockScale = IN[6]<br>
angle = IN[7]

offsetX = offsetX1/25.4<br>
offsetY = offsetY1/25.4<br>
scaleX = scaleX1/25.4<br>
scaleY = scaleY1/25.4

mat = **UnwrapElement**(mat1)<br>
doc = DocumentManager.Instance.CurrentDBDocument

AppearanceAsset = doc.**GetElement**(mat.AppearanceAssetId)<br>
RenderingAsset = AppearanceAsset.**GetRenderingAsset**()<br>
AppearanceAssetid =AppearanceAsset.Id

TransactionManager.Instance.**EnsureInTransaction**(doc)

editScope = **AppearanceAssetEditScope**(doc)<br>
AssetEditable = editScope.**Start**(AppearanceAssetid)

BitMapLocation = AssetEditable[UnifiedBitmap.UnifiedbitmapBitmap] #AssetProperty String Object<br>
BitMapLocation.Value = var1

BitmapOffsetX = AssetEditable[UnifiedBitmap.TextureRealWorldOffsetX]<br>
BitmapOffsetX.Value = offsetX

BitmapOffsetY = AssetEditable[UnifiedBitmap.TextureRealWorldOffsetY]<br>
BitmapOffsetY.Value = offsetY

BitmapscaleX = AssetEditable[UnifiedBitmap.TextureRealWorldScaleX]<br>
BitmapscaleX.Value = scaleX

BitmapScaleY = AssetEditable[UnifiedBitmap.TextureRealWorldScaleY]<br>
BitmapScaleY.Value = scaleY

Scalelock = AssetEditable[UnifiedBitmap.TextureScaleLock]<br>
Scalelock.Value = lockScale

TextureWAngle = AssetEditable[UnifiedBitmap.TextureWAngle]<br>
TextureWAngle.Value = angle

editScope.**Commit**(IFailuresPreprocessor)

TransactionManager.Instance.**TransactionTaskDone**()

Uiteraard zou de code veel beter moeten met if/exceptions enzovoorts. Maar ja, je moet ergens beginnen. 

**3. AHN3 poisson surface reconstruction, directshape  en exporteren naar Lumion en Revit Live.**

De hierboven genoemde workaround geeft tal van mogelijkheden.

**a) In Revit de luchtfoto automatisch als materiaal in laten stellen.** Hier zitten nog wel wat moeilijkheden aan vast. Bij gebruik van een toposurface is een materiaal gespiegeld. Dit is een bug. Je kunt dit oplossen door de foto te spiegelen.

**b) AHN3 downloaden, croppen en importeren in cloudcompare.(zie vorige blog)**<br>
Vervolgens meshen en importeren via dynamo als directshape. 

Na veel exporteren was het volgende werkbaar voor mij:

**Cloudcompare:**

![7_Cloudcompare_settings_normals](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/7_Cloudcompare_settings_normals.png)

**Normals berekenen met Triangulation**

![7_Cloudcompare_settings_poisson_surface_reconstruction](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/7_Cloudcompare_settings_poisson_surface_reconstruction.png)

Langzamerhand begin ik enigzins gevoel bij bovenstaande opties te krijgen.
Als je AHN3 gebruikt kun je weinig sampels per node gebruiken omdat er veel data is. Bij grovere pointclouds met meer vervuiling kun je meer samples per node kiezen. 
Kies voor boundary 'Free' zodat er geen 'bubble' onder de pointcloud gaat onstaan en je het material niet meer goed kunt instellen.

![7_update_AHN](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/7_update_AHN.png)

Octree depth 11 geeft fantastische resultaten!!(dit is een duingebied, let op de paden) Alleen is dit te zwaar om in Dynamo te importeren. 

Ter info mijn ervaring qua bestandsgrootten bij bovenstaand project.

- AHN3-bestand pointcloud: 1 GB
- Gecropt naar 500x500 meter(laz): 17 mb.
- Poisson Surface Reconstruction in CloudCompare met Octree 9 en opslaan als .obj: 50 MB.
- Poisson Surface Reconstruction in CloudCompare met Octree 10 en opslaan als .obj: 250 MB.
- Importeren in Dynamo als Mesh en vervolgens reduceren tot ca 200.000-500.000 triangles. Daarna loopt Dynamo vast op mijn laptop(Dell XPS 15, 16GB, i7-7700HQ, GTX 1050)

![9_dynamo](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/9_dynamo.png)

De workflow hiervoor is vrij eenvoudig. 
Verder is het zo dat je boolean operaties stukken uit de mesh kunt knippen. 

Daarna komt de vuurproef. Krijg je een mesh met 400.000 triangles vanuit Revit(niet echt ontworpen voor gebruik van meshes) naar Lumion of Revit Live?

Jazeker dat lukt met fantastische resultaten!

![8_AHN_in_lumion](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/8_AHN_in_lumion.png)

Dus ook met de VR-bril op loop je door je model met de omgeving in 3D zonder dat je hier enig modelleerwerk voor hebt hoeven te doen.

**3D DWF**
Als je het model als 3D DWF gaat exporteren klopt het renderpatroon niet meer.(90 graden rotatieverschil). Dit is wel jammer. DWF is een mooi uitwisselformaat met opdrachtgevers en aannemers.

![7_DWF_bug](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2018-05-21/7_DWF_bug.png)