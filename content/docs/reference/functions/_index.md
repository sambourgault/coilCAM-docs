+++
title = 'functions'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 5
+++

## 1D functions
## function operators
`Linear`: Returns an array of floats of the form y = ((amplitude)x + (offset)) + Values0 or y = ((amplitude)x + (offset)) * Values0. 

**Parameters**
- `amplitude` (`float`): Value multiplied with x.
- `offset` (`float, optional`): Value added to (amplitude)x.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats.
  

`Sinusoidal`: Returns an array of floats of the form y = (amplitude)\*sin(2pi/(period)\*x + (offset)) + Values0 or y = (amplitude)\*sin(2pi/(period)\*x + (offset)) * Values0.

**Parameters**
- `amplitude` (`float`): Value multiplied with the sinus.
- `period` (`int, optional`): Number of points per cycle.
- `offset` (`float, optional`): Offset value added to 2pi/T\*x.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats.

`Staircase`: Returns an array of floats of the form y = (stepHeight*[x/stepWidth] + offset) + values0 or y = (stepHeight*[x/stepWidth] + offset) * values0.

**Parameters**
- `stepWidth` (`float`): Number of points before going to next step.
- `stepHeight` (`height`): Increment for each new step.
- `offset` (`float, optional`): Offset value added to step function.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats.





## 2D functions

## Boolean functions

