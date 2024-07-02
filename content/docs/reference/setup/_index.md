+++
title = 'setup'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 5
+++

## setup
### toolpath unit generator
`toolpathUnitGenerator`: Generates a toolpath for a 3D form based on the provided initialization and shaping parameters. Example shape making functions include: exponential, linear, sinusoidal, square, and staircase.

**Parameters**

- `Position` (`point3D`): The (x, y, z) coordinates of the form's center.

- `Initial radius` (`float`): The radius of the base form.
  
- `nbLayers` (`int`): The number of layers in the form.

- `nbPointsInLayer` (`int`): The number of points per layer.

**Shaping Parameters (optional)**

- `radiusShapingParameter` (`float`): Applies a 1D function to points in a layer, modifying the layer's perimeter.

- `scaleShapingParameter` (`float`): Applies a 1D function to the scale of all layers, modifying the profile of the form.

- `scalingRadiusParameter` (`float`): Also known as scalingRadius, applies a 1D function to each layer, scaling the radius of the given layer with respect to its layer index. This creates the effect of varied strengths of radius shaping along the profile of the form.

- `translateShapingParameter` (`float`): Applies a 2D function to the position of all layers, modifying the layer offsets in the xy plane.

- `rotateShapingParameter` (`float`): Applies a 1D function to the rotation of all layers, modifying the angle of the layer.

**Returns**

- `path` (`float[nbLayers * nbPointsInLayer * 3]`): A list of floats corresponding to x, y, z coordinates for each point along the toolpath.


## 1D functions


## 2D functions

## Boolean

