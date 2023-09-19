---
layout: post
title: "AHN-pointcloud 3D surfacereconstruction"
date: 2017-12-05 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/4AHN2Viewer.png'
published: true
---

# AHN-pointcloud 3D surfacereconstruction

Een eerste poging tot 'surface reconstruction' met gebruik van AHN-pointclouds.
Je kunt het AHN bekijken via:

- [https://ahn.arcgisonline.nl/ahnviewer/](https://ahn.arcgisonline.nl/ahnviewer/)
- [http://ahn2.pointclouds.nl](http://ahn2.pointclouds.nl/)

![4AHN2Viewer](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/4AHN2Viewer.png)

En tevens via het pdok downloaden: [https://www.pdok.nl/nl/ahn3-downloads](https://www.pdok.nl/nl/ahn3-downloads)

**Pointclouds**
Puntenwolken bestaan uit punten met een X,Y,Z-waarde en een optionele classificatie.

Een mogelijke workflow:

![GIS2BIMPointCloudWorkflow](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/GIS2BIMPointCloudWorkflow.png)

**1) Stel locatie in via de Revit 'Location'**

![1SetLocation](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/1SetLocation.png)

**2) Gebruik Dynamo om te achterhalen welke pointcloud uit het AHN je nodig hebt**
Stappen:
-Haal lat/lon uit de revitlocatie op.
-Transformeer(met GIS2BIM) van WGS-84 naar RD-coördinaten.
-Zoek downloadlink op met behulp van pdok

![2_download AHN2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/2_download AHN2.gif)

De pointcloud is nu erg groot:

![5_cloudcompare](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/5_cloudcompare.png)

**3) Gebruik LASZIP om het deel uit de pointcloud te knippen dat je nodig hebt.**

![3LasZipSettings](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/3LasZipSettings.png)

Of je kunt een batchbestand m.b.v. dynamo genereren.

![3_batchfile_laszip](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/3_batchfile_laszip.gif)

**4) Bekijk het resultaat in cloudcompare(open source pointcloud editor)**

![4_open_cloudcompare](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/4_open_cloudcompare.gif)

**5) Normals**

In de AHN-pointclouds zitten geen ['normaalvectoren'](https://en.wikipedia.org/wiki/Normal_(geometry)) op de punten. Voordat je een surfacereconstruction kunt maken moeten er 'normals' gemaakt worden. 

Er zijn verschillende instellingen hoe dit te genereren. Het is even een tijdje puzzelen. Eerst krijg je dit soort meshresultaten.(met [poissonsurfacereconstruction](https://en.wikipedia.org/wiki/Poisson%27s_equation#Surface_reconstruction))

![1BadMeshMonkey](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/1BadMeshMonkey.png)

In de praktijk blijkt AHN2 lastig te meshen omdat het een grovere puntenwolk is.
AHN3 werkt een stuk beter.

**6) AHN meshen**
Onderstaand een AHN3 pointcloud van een stuk strand waarbij het oorspronkelijke oppervlakte gereconstrueerd wordt met behulp van het Poisson Surface Reconstruction-Algoritme.

![5_poisson_surfacereconstruction](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/5_poisson_surfacereconstruction.gif)

Er zijn allerlei methoden voor surfacereconstruction. Onderstaand is [Delaunay](https://en.wikipedia.org/wiki/Delaunay_tessellation_field_estimator) gebruikt.

![6CloudComputeNormals3](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/6CloudComputeNormals3.png)

**Open source programma's met GUI voor pointclouds/surface reconstruction:**
-[CloudCompare](http://www.danielgm.net/cc/)
-[LibLAS](https://www.liblas.org/)
-[MeshLab](http://www.meshlab.net/)
-[Unity](https://unity3d.com/)

**Enkele interessante bibliotheken**
-[PDAL](https://www.pdal.io/)
-[CGAL](https://www.cgal.org/)
-[Pointcloud Library(PCL)](https://www.pointclouds.org/)
Alle drie in C++. 

**7) Mesh als .obj inladen in dynamo**

![6_mesh_to_dynamo](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/6_mesh_to_dynamo.gif)

Wat kun je allemaal nog meer met de pointclouddata?

**1) Als pointcloud inladen**

![7ImportPointcloudInRevit](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/7ImportPointcloudInRevit.png)

**2) Converteren naar Directshape**

![9MeshInRevit](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/9MeshInRevit.png)

**3) Doorsnedelijnen genereren(bijvoorbeeld voor dijklichamen)**

![10_DikeSection](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/9Mes10_DikeSectionhInRevit.png)

**4) Omzetten naar points in een toposurface(geschikt voor gebieden met weinig bebouwing en bomen zoals het strand)**

![11_beach](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2017-12-05/11_beach.png)

Er zijn diverse nodes beschikbaar in de GIS2BIM-package. Inmiddels is versie 0.4 uit. Voor meer informatie kijk op: <br>
[https://github.com/DutchSailor/GIS2BIM/wiki/Nodes-version-0.4](https://github.com/DutchSailor/GIS2BIM/wiki/Nodes-version-0.4)

Voor een actueel overzicht van alle huidige nodes: [https://dynamonodes.com/author/maartenvroegindeweij/](https://dynamonodes.com/author/maartenvroegindeweij/)

Een leuke volgende stap zou het integreren van [3dfier](https://github.com/tudelft3d/3dfier) zijn.