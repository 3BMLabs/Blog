---
layout: post
title:  "Using the SurfacePatternToCurves node from 3BMLabs.MakeUp"
date:   2019-10-01 17:30:00
author: Leslie Ing
categories: dynamo
description: "In this blog post we will describe the usage of the SurfacePatternToCurves node"
image: 'https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif' 
published: false
---

Wow dit is echt fantastisch!! Het team van de TU Delft heeft een programma gemaakt bag3d.
Hiermee is de hoogtedata van het AHN3 gecombineerd met de gegevens van de Basis Administratie Gebouwen.

Een deel van het resultaat is beschikbaar gesteld als webservice: <http://3dbag.bk.tudelft.nl/data/wfs?request=getcapabilities>

Meer informatie is te vinden op <http://3dbag.bk.tudelft.nl/>.

Dit is natuurlijk top om binnen Dynamo te gebruiken. Eindelijk een snelle oplossing om de gebouwde omgeving in 3D in Revit in te laden.

Gebruik de nieuwe versie van GIS2BIM 0.8. Op de wiki op GitHub staan trouwens alle nodes uitgelegd. <https://github.com/DutchSailor/GIS2BIM/wiki/Nodes-version-0.8> 

De workspace is te downloaden via <https://github.com/DutchSailor/GIS2BIM/tree/master/nodes/support/DutchGEO/BAG> 3D.dyn

Deze staat tevens in de 'extra' map die bij GIS2BIM geïnstalleerd is.

Een voorbeeld webrequest voor een gebied van 500x500 meter rondom het centrum van Gouda:

http://3dbag.bk.tudelft.nl/data/wfs?&request=GetFeature
&typeName=BAG3D:pand3d
&outputFormat=GML3
&bbox=108311,446935,108711,447335

![orkingigf](https://github.com/3BMLabs/Blog/raw/master/img/1_BAG%203D.gif)

![alt test](./img/1_BAG 3D.gif)

src="./img/1_BAG 3D.gif"

<img src='./img/1_BAG 3D.gif'>

![Farmers Market Finder Demo](img/1_BAG 3D.gif)






https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif
