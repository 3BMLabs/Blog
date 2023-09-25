---
layout: post
title: "Revit, Oculus en Virtual Reality"
date: 2014-07-03 11:00:00
author: Maarten Vroegindeweij
categories: BIM
description: ""
image: 'https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-07-03/17-1.png'
published: true
---

# Revit, Oculus en Virtual Reality

Een korte post over Revit en VR-brillen. Het is mogelijk om een 3D-model te bekijken met een 3D-bril. Er zijn momenteel meerdere modellen op de markt. Begin deze week hebben we een Oculus Rift VR-bril aangeschaft. Dit een Oculus Rift DK1. Na de zomer komt DK2 uit. Momenteel is DK1 niet nieuw meer te koop voor zover wij konden achterhalen. [Markplaats](http://www.marktplaats.nl/z.html?query=oculus+rift&categoryId=0&postcode=&distance=0) bood uitkomst. Voor 300 euro een 2e hands oculus rift. En verder een gratis [FBX-viewer](http://www.realis3d.com/download-now) met Oculus ondersteuning.

Een aantal gemakkelijke workflows om een Revit-model met een Oculus Rift te bekijken.(Er zijn veel meer mogelijkheden)

**1) Revit --> FBX--> (3D-max --> FBX -->)Unity3D**
[http://bim.wikispaces.com/Revit+to+Unity](http://bim.wikispaces.com/Revit+to+Unity)

[Unity](http://unity3d.com/) is wel een vrij prijzig pakket.

![17-1](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-07-03/17-1.png)

Een andere optie is(die hebben wij gebruikt):

**2) Revit --> FBX --> Realis3D Viewer(gratis)**<br>
[http://www.realis3d.com/download-now](http://www.realis3d.com/download-now)

Het werkt fantastisch. De diepte die je in een model hebt met de VR-bril op is geweldig. De graphics zijn nog niet op het niveau van bijvoorbeeld [Lumion](http://lumion3d.com/), maar dat gaat ongetwijfeld komen.

Voor degenen die het niet kennen. Een oculus merkt als je naar boven en naar beneden kijkt en rondom. Dus je beweegt je hoofd en tegelijkertijd kijk je rond in een virtuele omgeving.

![17-2](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2014-07-03/17-2.png)

**Stappenplan:**<br>
- Koop een oculus rift.
- Download de oculus rift Developers Kit.
- Configureer en kalibreer je oculus.
- Download en installeer de Realis3D-viewer.
- Exporteer je Revit-model naar FBX.
- Open in Realis3D.
- Zet in de settings de checkbox 'Oculus Rift' aan.

**Tags:** Revit, Oculus Rift, Realis3D, FBX, Virtual Reality