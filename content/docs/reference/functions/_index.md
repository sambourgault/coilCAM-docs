+++
title = 'functions'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 10
+++

# Function Operators
## 1D functions
### Linear
`linear(amplitude, offset, nbPoints, values0, mode);`

*y = ((amplitude \* x) + offset) (+ or \*) values0*
<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_linear" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Linear"></iframe>

<!-- **Parameters**
- `amplitude` (`float`): Value multiplied with x.
- `offset` (`float, optional`): Value added to (amplitude)x.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats. -->
  

### Sinusoidal
`sinusoidal(amplitude, period, offset, nbPoints, values0, mode);`

*y = ((amplitude \* sin(2π/period) \* x) + (offset)) (+ or \*) values0*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_sine" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Sinusoidal"></iframe>

<!-- **Parameters**
- `amplitude` (`float`): Value multiplied with the sinus.
- `period` (`int, optional`): Number of points per cycle.
- `offset` (`float, optional`): Offset value added to 2pi/T\*x.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats. -->


### Staircase
`staircase(stepWidth, stepHeight, offset, nbPoints, values0, mode);`

*y = (stepHeight\*[x/stepWidth] + offset) (+ or \*) values0*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_staircase" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Staircase"></iframe>

<!-- **Parameters**
- `stepWidth` (`float`): Number of points before going to next step.
- `stepHeight` (`height`): Increment for each new step.
- `offset` (`float, optional`): Offset value added to step function.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats. -->



### Square Wave
`square(amplitude, period, offset, bumps, nbPoints, values0, mode);`

*y = (amplitude \* ((x + offset) >= bumps/period)) (+ or \*) values0*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_squarewave" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Square Wave"></iframe>

<!-- **Parameters**
- `amplitude` (`float`): Value multiplied with the sinus.
- `period` (`int, optional`): Number of points per cycle.
- `offset` (`float, optional`): Offset value added to 2pi/T\*x.
- `bumps` (`int, optional`): Bumps: number of points when y != 0.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`float[nbPoints]`): An array of floats. -->



### Exponential
`exponential(base, amplitudeExponent, amplitude, offset, nbPoints, values0, mode);`

*y = amplitude \* base^((amplitudeExponent \* x) + offset) (+ or \*) values0*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_exponential" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Exponential"></iframe>
<!-- 
**Parameters**
- `base` (`float`): Base value of the exponential.
- `amplitudeExponent` (`float`): Value multiplying x in the exponential.
- `amplitude` (`int, optional`): Number of points per cycle.
- `offset` (`float, optional`): Offset value added to 2pi/T\*x.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.
**Returns**
- `values` (`float[nbPoints]`): An array of floats.
-->



## 2D functions

### Linear2D
`linear2D(amplitude1, offset1, amplitude2, offset2, nbPoints, values0, mode);`

*y1 = amplitude1\*x1 + offset1, y2 = amplitude2\*x2 + offset2*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_linear2D" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Linear2D"></iframe>

<!-- **Parameters**
- `amplitude1` (`float`): Value multiplied with x1.
- `offset1` (`float, optional`): Value added to (amplitude1)x1.
- `amplitude2` (`float`): Value multiplied with x2.
- `offset2` (`float, optional`): Value added to (amplitude2)x2.
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`[float[nbPoints], float[nbPoints]]`): An array storing two arrays of floats. -->


### Sinusoidal2D
`sinusoidal2D(amplitude1, period1, amplitude2, period2, offset, nbPoints, values0, mode);`

*y1 = amplitude1\*x1 + offset1, y2 = amplitude2\*x2 + offset2*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_sine2D" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Sinusoidal2D"></iframe>

<!-- **Parameters**
- `amplitude1` (`float`): Value multiplied with the cosinus.
- `period1` (`float, optional`): Number of points per cycle for amplitude1.
- `amplitude2` (`float`): Value multiplied with the sinus.
- `period2` (`float, optional`): Number of points per cycle for amplitude2.
- `offset` (`float, optional`): b, value added to the argument of the cos and the sin to offset the wave. 
- `nbPoints` (`int`): Number of points in layer, or number of layers.
- `values0` (`float, optional`): Array of floats added to or multiplied by the function.
- `Mode` (`string, optional`): Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.

**Returns**
- `values` (`[float[nbPoints], float[nbPoints]]`): An array storing two arrays of floats.
   -->
## Boolean Functions

### Union
`union(path0, path1, by_layer);`

*Joins together two toolpaths by the layers at each z coordinate. If by_layer = false, the printer will print each toolpath separately.*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_union" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Union"></iframe>

### Intersection
`intersection(path0, path1, by_layer);`

*Takes the intersection of two toolpaths by the layers at each z coordinate. If by_layer = false, the printer will print each toolpath separately.*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_intersection" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Intersection"></iframe>

### Difference
`difference(path0, path1, by_layer = true);`

*Subtracts path0 by path1. If by_layer = false, the printer will print each toolpath separately.*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_difference" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Difference"></iframe>



## Data Manipulation

### Waveform
`waveform(filename, nbPoints='default', offset = 0, heightRange=[-1,1]);`

*Converts a midi or wav file to an array of floats.*

<iframe src="https://esmepuzio.com/simple-coilCAM-js?example=functions_waveform" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Waveform"></iframe>

