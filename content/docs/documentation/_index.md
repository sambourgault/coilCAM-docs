+++
title = 'documentation'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 3
[params]
  math = true
+++

# CoilCAM Functions

### Toolpath Unit Generator
*Generates a toolpath for a 3D form based on the provided initialization and shaping parameters. Example shape making functions include: exponential, linear, sinusoidal, square, and staircase.*

`toolpathUnitGenerator(position, radius, layerHeight, nbLayers, nbPointsInLayer, radiusParameter, scaleParameter, scalingParameter, translateParameter, rotateParameter, thicknessParameter);` 

{{< details title="Toolpath Parameters">}}
- `position (int[3])` The (x, y, z) coordinates of the form's center.
- `radius (float)` The radius of the base form.
- `layerHeight (float)` Height of each layer. For best results, layerHeight should be half the nozzle diameter.
- `nbLayers (int)` The number of layers in the form.
- `nbPointsInLayer (int)` The number of points per layer.
- `radiusParameter (float, optional)` *Applies a 1D function to points in a layer, modifying the layer's perimeter.*
- `scaleParameter (float, optional)` *Applies a 1D function to the scale of all layers, modifying the profile of the form.*
- `scalingParameter (float, optional)` *Applies a 1D function to each layer, scaling the radius of the given layer with respect to its layer index. This creates the effect of varied strengths of radius shaping along the profile of the form.*
- `translateParameter (float, optional)` *Applies a 2D function to the position of all layers, modifying the layer offsets in the xy plane.*
- `rotateParameter (float, optional)` *Applies a 1D function to the rotation of all layers, modifying the angle of the layer.*
- `thicknessParameter (float, optional)` *Adjusts the print speed for each point along the toolpath, modulating the thickness. Thickness should be in the range `[-1, 1]` and is 0 by default.*

**Returns:** `path ([point = {x, y, z, t}])` An array of point objects corresponding to an x coordinate, y coordinate, z coordinate and point thickness for each point along the toolpath.
{{< /details >}}
{{< details title="Toolpath Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_1"  width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Linear"></iframe>
{{< /details >}}


## 1D functions

### Linear
$$((\text{amplitude} \cdot x) + \text{offset}) (+ \, \text{or} \times \text{values0})$$


`linear(amplitude, offset, nbPoints, values0, mode);`
{{< details title="Linear Parameters">}}
   - `amplitude (float)` Value multiplied with x.
   - `offset (float, optional)` *Value added to (amplitude)x.*
   - `nbPoints (int)` Number of points in layer, or number of layers.
   - `values0 (float, optional)` *Array of floats added to or multiplied by the function.*
   - `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values (float[nbPoints]):` An array of floats.
{{< /details >}}
{{< details title="Linear Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_linear" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Linear"></iframe>
{{< /details >}}


### Sinusoidal
$$((\text{amplitude} \cdot \sin(\frac{2\pi}{\text{period}}) \cdot x) + \text{offset}) (+ \, \text{or} \times \text{values0})$$

`sinusoidal(amplitude, period, offset, nbPoints, values0, mode);`
{{< details title="Sine Wave Parameters">}}
- `amplitude (float)` Value multiplied with the sinus.
- `period (int)` Number of points per cycle.
- `offset (float, optional)` *Offset value added to 2pi/T\*x.*
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0 (float, optional)` *Array of floats added to or multiplied by the function.*
- `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values (float[nbPoints])` An array of floats.
{{< /details >}}
{{< details title="Sine Wave Example" open="true" >}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_sine" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Sinusoidal"></iframe>
{{< /details >}}

### Staircase
$$(\text{stepHeight} \cdot \lfloor x / \text{stepWidth} \rfloor + \text{offset}) (+ \, \text{or} \times \text{values0})$$

`staircase(stepWidth, stepHeight, offset, nbPoints, values0, mode);`

{{< details title="Staircase Parameters" >}}
- `stepWidth (float)` Number of points before going to next step.
- `stepHeight (height)` Increment for each new step.
- `offset (float, optional)` *Offset value added to step function.*
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0 (float, optional)` *Array of floats added to or multiplied by the function.*
- `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values` (`float[nbPoints]`): An array of floats.

{{< /details >}}
{{< details title="Staircase Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_staircase" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Staircase"></iframe>
{{< /details >}}

### Square Wave
$$
(\text{amplitude} \cdot ((x + \text{offset}) \geq \frac{\text{bumps}}{\text{period}})) (+ \, \text{or} \times \text{values0})
$$


`square(amplitude, period, offset, bumps, nbPoints, values0, mode);`
{{< details title="Square Wave Parameters" >}}
- `amplitude (float)` Value multiplied with the sinus.
- `period (int, optional)` Number of points per cycle.
- `offset (float, optional)` *Offset value added to 2pi/T\*x.*
- `bumps (int, optional)` *Bumps: number of points when y != 0.*
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0 (float, optional)` *Array of floats added to or multiplied by the function.*
- `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values (float[nbPoints])` An array of floats. -->
{{< /details >}}

{{< details title="Square Wave Example" open="true" >}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_squarewave" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Square Wave"></iframe>
{{< /details >}}


### Exponential
$$
\text{amplitude} \cdot \text{base}^{((\text{amplitudeExponent} \cdot x) + \text{offset})} (+ \, \text{or} \times \text{values0})
$$

`exponential(base, amplitudeExponent, amplitude, offset, nbPoints, values0, mode);`
{{< details title="Exponential Parameters">}}
- `base (float)` Base value of the exponential.
- `amplitudeExponent (float)` Value multiplying x in the exponential.
- `amplitude (int)` Number of points per cycle.
- `offset (float, optional)` *Offset value added to 2pi/T\*x.*
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0 (float, optional)` *Array of floats added to or multiplied by the function.*
- `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values (float[nbPoints])` An array of floats.
{{< /details >}}
{{< details title="Exponential Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_exponential" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Exponential"></iframe>
{{< /details >}}


## 2D functions

### Linear2D
$$x' = ((\text{amplitudeX} \cdot x) + \text{offsetX}) (+ \, \text{or} \times \text{values0X})$$
$$y' = ((\text{amplitudeY} \cdot y) + \text{offsetY}) (+ \, \text{or} \times \text{values0Y})$$

`linear2D(amplitudeX, offsetX, amplitudeY, offsetY, nbPoints, valuesX, valuesY, mode);`

{{< details title="Linear 2D Parameters" >}}
- `amplitudeX (float)` Value multiplied with x.
- `offsetX (float, optional)` *Value added to (amplitudeX)x.*
- `amplitudeY (float)` Value multiplied with y.
- `offsetY (float, optional)` *Value added to (amplitudeY)y.*
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0X (float, optional)` *Array of floats added to or multiplied by the x function.*
- `values0Y (float, optional)` *Array of floats added to or multiplied by the y function.*
- `mode (string, optional)` *Determines if linear functions are `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values ([float[nbPoints], float[nbPoints]])` An array storing two arrays of floats.
{{< /details >}}
{{< details title="Linear 2D Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_linear2D" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Linear2D"></iframe>
{{< /details >}}


### Sinusoidal2D
\[
\begin{aligned}
    x' &= \text{amplitudeX} \cdot \cos\left(\frac{2\pi}{\text{periodX}} x + \text{offsetX}\right) (+ \, \text{or} \times \text{values0X}) \\
    y' &= \text{amplitudeY} \cdot \sin\left(\frac{2\pi}{\text{periodY}} y + \text{offsetY}\right) (+ \, \text{or} \times \text{values0Y})
\end{aligned}
\]


`sinusoidal2D(amplitude1, period1, amplitude2, period2, offset, nbPoints, values0, mode);`
{{< details title="Sine Wave 2D Parameters">}}
- `amplitudeX (float)`: Value multiplied with the cosinus.
- `periodX (float)`: Number of points per cycle for amplitudeX.
- `offsetX float, optional)` *Value added to (amplitudeX)x.* 
- `amplitudeY (float)` Value multiplied with the sinus.
- `periodY (float)` Number of points per cycle for amplitude2.
- `offsetY (float, optional)` *Value added to (amplitudeY)y.* 
- `nbPoints (int)` Number of points in layer, or number of layers.
- `values0X (float, optional)` *Array of floats added to or multiplied by the x function.*
- `values0Y (float, optional)` *Array of floats added to or multiplied by the y function.*
- `mode (string, optional)` *Determines if linear function is `additive` or `multiplicative`. Mode is `additive` by default.*

**Returns:** `values ([float[nbPoints], float[nbPoints]])` An array storing two arrays of floats.
  
{{< /details >}}
{{< details title="Sine Wave 2D Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_sine2D" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Sinusoidal2D"></iframe>
{{< /details >}}

## Boolean Functions

### Union
*Joins together two toolpaths by the layers at each z coordinate.*

`union(path0, path1);`
{{< details title="Union Parameters">}}
- `path0 (float[nbPoints * nbLayers])` Main toolpath.
- `path1 (float[nbPoints * nbLayers])` Secondary toolpath.

**Returns:** `path (float[])` Union toolpath.

**Note:** Paths must share the same z-coordinate at each layer. Paths cannot be spiralized before calling union(path0, path1).

{{< /details >}}

{{< details title="Union Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_union" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Union"></iframe>
{{< /details >}}


### Difference
*Subtracts path0 by path1.*

`difference(path0, path1);`

{{< details title="Difference Parameters">}}
- `path0 (float[nbPoints * nbLayers])` Main toolpath.
- `path1 (float[nbPoints * nbLayers])` Secondary toolpath.

**Returns:** `path (float[])` Difference toolpath.

**Note:** Paths must share the same z-coordinate at each layer. Paths cannot be spiralized before calling difference(path0, path1).
{{< /details >}}

{{< details title="Difference Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_difference" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Difference"></iframe>
{{< /details >}}


## Path Manipulation

### Base Spiral
*Adds a spiral base to the form.*

`baseSpiral(position, nbPointsInLayer, nozzleDiameter, radius, zOffset=0, rotation=0);`

{{< details title="Base Spiral Parameters">}}
- `position (int[3])` The (x, y, z) coordinates of the form's center.
- `nbPointsInLayer (float)` The number of points per layer.
- `nozzleDiameter (float)` The nozzle diameter. 
- `radius (float)` The radius of the base form.
- `zOffset (float, optional)` *Offset added to z coordinate.*
- `rotation (float, optional)` *Angle of rotation added to the spiral (set to 0 by default).*

**Returns:** `path ([point = {x, y, z, t}])` An array of points representing the spiral base toolpath.
{{< /details >}}

{{< details title="Base Spiral Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_baseSpiral" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Difference"></iframe>
{{< /details >}}


### Base Fill
*Adds a flat base to the form.*
`baseFill(position, radius, nbPointsInLayer, nozzleDiameter, path, zOffset=0, rotation=0);`

{{< details title="Base Fill Parameters">}}
- `position (int[3])` The (x, y, z) coordinates of the form's center.
- `radius (float)` The radius of the base form.
- `nbPointsInLayer (float)` The number of points per layer.
- `nozzleDiameter (float)` The nozzle diameter. 
- `path ([point = {x, y, z, t}])` The path of the base form.
- `zOffset (float, optional)` *Offset added to z coordinate.*
- `rotation (float, optional)` *Angle of rotation added to the spiral (set to 0 by default).*

**Returns:** `path ([point = {x, y, z, t}])` An array of points representing the flat base toolpath.
{{< /details >}}

{{< details title="Base Fill Example" open="true">}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-functions&example=functions_baseFill" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Difference"></iframe>
{{< /details >}}


### Spiralize Path
`spiralize(path, layerHeight);`
*Evenly wraps points in layer around the form.*


