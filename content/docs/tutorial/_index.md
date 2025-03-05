+++
title = 'tutorial'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 5
[params]
  math = true
+++


# Toolpath Unit Generator Tutorial
This tutorial demonstrates how to alter points along the toolpath using the Toolpath Unit Generator. To test this code using the [CoilCAM-js web editor](https://sambourgault.github.io/coilCAM-js/), simply copy and paste the code at each step into the web editor. At each step, try altering the variables of each shaping parameter to see what effects they have on the toolpath.

## Creating a Form
In the editor below, press the "Run" button at the upper left.
In the visualization window to the right, you should see a simple toolpath appear. 

<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_1" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 1"></iframe>

The toolpath in the visualization window is created through the ToolpathUnitGenerator function. This function accepts eleven parameters.
* The first five parameters initialize the form.
    * `position (array)` Sets the x, y, z coordinates for the center of the form.
    * `initialRadius (float)` Sets the radius of the form.
    * `layerHeight (float)` Sets the height of all layers in the form. For best results, layer height should be around half of the nozzle diameter.
    * `nbLayers (int)` Sets the number of layers for the form.
    * `nbPointsInLayer (int)` Sets the number of points in each layer.
* The last six optional parameters are used to shape the vessel. We will apply each of these parameters one by one through the remainder of this tutorial.

Once those parameters have been passed to the ToolpathUnitGenerator function, we can display the toolpath using the updatePath function. Try modifying the radius, number of layers and number of points in each layer to affect the shape of the toolpath.

## CoilCAM workflow


## Shaping the Form
### radiusShapingParameter
The first optional parameter is the radiusShapingParameter, which shapes the radius of each layer. To create a star-shaped vessel, we apply a sine wave to the toolpath. 

<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_2" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 2"></iframe>

### scaleShapingParameter
The second optional parameter is the scaleShapingParameter, which modifies the size of each layer, shaping the profile of the toolpath. To shape the toolpath into a vase, we apply a sine wave to the profile of the toolpath. 

<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_3" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 3"></iframe>

### scalingRadiusShapingParameter
The third optional parameter is the scalingRadiusShapingParameter, which modifies the intensity of each layer, shaping the profile of the toolpath. 
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_4" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 4"></iframe>

To make the base of the toolpath circular, we multiply the scalingRadiusShapingParameter by a linear function to decrease the intensity of the scalingRadiusShapingParameter near the base of the toolpath. Chaining together functions like this enables complex geometry that would be difficult to acheive with a single function.
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_5" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 5"></iframe>

### translateShapingParameter
The fourth optional parameter is the translateShapingParameter, which offsets the position of each layer in the form.
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_6" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 6"></iframe>

### rotateShapingParameter
The fifth optional parameter is the rotateShapingParameter, which rotates each layer in the form.
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_7" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 7"></iframe>

### thicknessShapingParameter
The sixth optional parameter is the thicknessShapingParameter, which sets the speed at which the form will be printed, altering the thickness of each point in the form.
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_8" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 8"></iframe>

## Preparing to Print
### Adding a Base (WIP)
Before printing this vessel, we add a base to the toolpath.
This base is constructed from two functions: baseFill and baseSpiral. Construtcing a base from two layers with different toolpaths increases base stability, but three or more base layers dry slower than the rest of the toolpath.
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_9" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 9"></iframe>

The baseFill function accepts six parameters, which are dependent on the parameters of the form it will be attached to.
* `position:` The x, y, z coordinates for the center of the form.
* `path:` The toolpath of the form.
* `nbPointsInLayer:` The number of points in the first layer of the form.
* `nozzleDiameter:` The thickness of the nozzle that will be used to print the toolpath.
* `radius:` The radius of the form. 

### Spiralizing and Centering

Because every point in a layer is added at the same height, the toolpath has a "seam" where the nozzle jumps from one layer height to the next. To eliminate this effect, we pass the toolpath through the spiralize function, which accepts two parameters: the path and the layer height. As the path is currently centered at [0, 0, 0] (the upper right corner of the printer bed) we can move the path to the center using the centerPath function.

<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_10" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 9"></iframe>

## Generating GCode
Once the form is complete, we can generate gcode using the generateGCode function. 
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=tutorial-quickstart&example=tutorial_11" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Tutorial 9"></iframe>

The generateGCode function accepts 4 parameters.
* `path` List of points.
* `layerHeight` Layer height. Should be half the nozzle size.
* `nozzleDiameter` Diameter of the nozzle (in mm).
* `printSpeed` Print speed (in mm/s)

You can copy the GCode string using console.log, or download the GCode string directly to your computer using the downloadGCode function.


## Common Issues
While there are no limits for the kinds of forms that can be constructed through CoilCAM, there are a few common mistakes that lead to faulty prints. 
* Each layer in the toolpath must be able to support the weight of the layers above it. Each layer of the toolpath should stay within 45 degrees of difference of the layer below it.
* Joining two forms together through the boolean union function can cause "artifacts" in the toolpath if the two layers are not aligned. To eliminate these artifacts, rotate forms using the rotation parameter so that the start of the first toolpath is aligned with the start of the second toolpath.
* Layer height should be around half of the nozzle diameter. When the layer height is too small, clay cannot extrude properly, causing pressure buildup. When the layer height is too large, clay cannot stick to the base or previous layers. 

## Other examples
Other examples are listed in the [examples]({{< ref "/docs/examples/_index.md" >}}) page.