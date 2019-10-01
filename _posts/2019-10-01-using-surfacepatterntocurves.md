---
layout: post
title:  "Introducing SurfacePatternToCurves to generate computerfloors"
date:   2019-10-01 17:30:00
author: Leslie Ing
categories: dynamo
description: "In this blog post we will describe the usage of the SurfacePatternToCurves node"
image: 'https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif' 
published: true
---

In this blog post we will describe the usage of the SurfacePatternToCurves node. This node was made to facilitate creating computer floors in Revit using Dynamo by extracting the surface pattern of the assigned material of the selected floor. This way you can edit the pattern of the floor, which will be reflected in the generated floor tile elements.

## What is SurfacePatternToCurves?

The node SurfacePatternToCurves has a multitude of possible uses. Let's first take a look at the in- and output of the node. The node accepts as input a model element, using its top surface for the extraction of the surface pattern of the assigned material. The output consists of five values. 

The first of these values, Grouped Perimeter IntersectionPoints, is a list of points on the self-intersections of the surface pattern and on the intersection of the pattern with the surface boundary. These points are transposed, in such a way that they form pairs of startpoints and endpoints.

The next output, Surface, is the top surface of the model element.

The third one is the Gridlines output. This will output the surface pattern in a list of curves.

The last two outputs are GridU and GridV. These output the same curves as Gridlines, but are seperated in the two directions of the surface pattern, and thus in two outputs.

## How to use SurfacePatternTOCurves?

In this example we will show you one way to use this node. 

## Example: Generating Computer Floors

![SurfacePatternToCurves_Demo_1](https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif)

## Understanding SurfacePatternToCurves

