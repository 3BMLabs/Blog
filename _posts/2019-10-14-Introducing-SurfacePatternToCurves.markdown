---
layout: post
title: "Generating computerfloors using SurfacePatternToCurves"
date: 2019-10-14 17:30:00
author: Leslie Ing
categories: dynamo revit bim computer floor python
description: "In this blog post we will describe the usage of the first 3BMLabs.MakeUp node: SurfacePatternToCurves"
image: 'https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif' 
published: true
---

In this blog post we will describe the usage of the SurfacePatternToCurves node. This node is the first one in many to come, created for the 3BMLabs.DigiFab Dynamo Package. It is used to help generate raised computer floors, using the hatch pattern on a Revit floor.

## Why use SurfacePatternToCurves?

At 3BM engineering we often use computer floors in our projects. These floors are defined by their characteristic of being elevated above the floor slab by pedestals to create space for wiring, because this allows maximum freedom of workspace organisation. 

In our workflow we need to know the grid of these raised tiles and place adaptive components, in order to make use of clash detection. In the old process we imported exploded Autocad drawings. Using this node we can speed up this process, because it reads the hatch pattern of the material of the floor slab and recreates it in Dynamo.

## What is SurfacePatternToCurves?

Let's first take a look at the in- and output of the node. The node accepts as input a model element, using its top surface for the extraction of the surface pattern of the assigned material. The output consists of five values. 

The first of these values, Grouped Perimeter IntersectionPoints, is a list of points on the self-intersections of the surface pattern and on the intersection of the pattern with the surface boundary. These points are transposed, in such a way that they form pairs of startpoints and endpoints.

The next output, Surface, is the top surface of the model element.

The third one is the Gridlines output. This will output the surface pattern in a list of curves.

The last two outputs are GridU and GridV. These output the same curves as Gridlines, but are seperated in the two directions of the surface pattern, and thus in two outputs.

## How to use SurfacePatternToCurves?

In this example we will show you one way to use this node. 

## Where to get SurfacePatternToCurves?

It can be donwloaded here, or alternitveley 

### Example: Generating Computer Floors

![SurfacePatternToCurves_Demo_1](https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif)

## Understanding SurfacePatternToCurves

