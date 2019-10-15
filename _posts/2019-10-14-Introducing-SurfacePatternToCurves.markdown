---
layout: post
title: "Generating Computer Floors using SurfacePatternToCurves"
date: 2019-10-14 17:30:00
author: Leslie Ing
categories: dynamo revit bim computer floor python
description: "In this blog post we will describe the usage of the SurfacePatternToCurves node"
image: 'https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif' 
published: true
---

In this blog post we will describe the usage of the SurfacePatternToCurves node. This node is the first one in many to come, created for the [3BMLabs.DigiFab Dynamo Package](https://github.com/3BMLabs/.DigiFab "3BMLabs.DigiFab repository"). It is used to help generate raised computer floors, using the hatch pattern on a Revit floor.

## Why?

At 3BM engineering we often use computer floors in our projects. These floors are defined by their characteristic of being elevated above the floor slab by pedestals to create space for wiring, because this allows maximum freedom of workspace organisation. 

![Computer Floors](https://raw.githubusercontent.com/3BMLabs/LABS/master/assets/blog_assets/2019-10-15/PBF_HighRes-Project_DOW_Terneuzen-Wurks-36-ps.jpg)

In our workflow we need to know the grid of these raised tiles and place adaptive components to make use of clash detection. In the old process we imported exploded Autocad drawings. Using this node we can speed up this process, because it reads the hatch pattern of the material of the floor slab and recreates the pattern in Dynamo.

## What?

Let's first take a look at the in- and output of the node. The node accepts as input a model element, in our case a floor.

"Grouped Perimeter IntersectionPoints", is a list of points on the self-intersections of the surface pattern and on the intersection of the pattern with the surface boundary. These points are transposed, in such a way that they form pairs of startpoints and endpoints.

"Surface" is the top surface of the model element.

The "Gridlines" output will output the surface pattern in a list of curves.

The two outputs "GridU" and "GridV" output the same curves as Gridlines, but are seperated in the two directions of the surface pattern, and thus in two outputs.



using its top surface for the extraction of the surface pattern of the assigned material. The output consists of five values. 


## How?

##### Example 1: Generating a grid for Computer Floor tiles
![SurfacePatternToCurves_Demo_1](https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif)
##### Example 2: Generating points for 


## Where?

The node and the example file can be installed from the Dynamo package mananger, or downloaded from our [Github Page](https://github.com/3BMLabs/.DigiFab "3BMLabs.DigiFab repository").

## Help?

In a next installment of the blog we will go into a deeper understanding of the node. However, if you have any questions or issues about the node feel free to create a [new issue](https://github.com/3BMLabs/.DigiFab/issues "3BMLabs.DigiFab repository issues") on our GitHub repository. 
