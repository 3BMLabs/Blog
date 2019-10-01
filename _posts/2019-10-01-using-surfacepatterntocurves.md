---
layout: post
title:  "Using the SurfacePatternToCurves node from 3BMLabs.MakeUp"
date:   2019-10-01 17:30:00
author: Leslie Ing
categories: dynamo
description: "In this blog post we will describe the usage of the SurfacePatternToCurves node"
image: 'https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif' 
published: true
---

In this blog post we will describe the usage of the SurfacePatternToCurves node. This node was made to facilitate creating computer floors in Revit using Dynamo by extracting the surface pattern of the assigned material of the selected floor.

## Using SurfacePatternToCurves

SurfacePatternToCurves has a multitude of possible uses. Let's first take a look at the in- and output of the node. The node accepts as input a model element, using its top surface for the extraction of the surface pattern of the assigned material. The output consists of five values. 

The first one, Grouped Perimeter IntersectionPoints, is a list of points on the intersections of the surface pattern and on the interesction of the pattern with the surface boundary. These points are transposed, in such a way that they form pairs of startpoints and endpoints. These points can be used for the input Using a adaptive component t

## Example: Generating Computer Floors

![SurfacePatternToCurves_Demo_1](https://github.com/3BMLabs/LABS/raw/master/assets/blog_assets/2019-10-01/SurfacePatternToCurves_Demo_1.gif)

## Understanding SurfacePatternToCurves

