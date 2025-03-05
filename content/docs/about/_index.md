+++
title = 'about'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 5
[params]
  math = true
+++


# About

## Video Tutorial
*Coming soon*

## What is CoilCAM?
CoilCAM is a digital fabrication workflow for designing toolpaths using parametric functions. CoilCAM was originally written in Python as a scripting plug-in for [Grasshopper](https://simplyrhino.co.uk/3d-modelling-software/grasshopper). CoilCAM-js implements core functionalities from CoilCAM as an open-source [javascript library](https://www.npmjs.com/package/coilcam). The original CoilCAM library can be accessed [here](https://github.com/sambourgault/coilCAM "coilCAM"), while a web editor for CoilCAM-js can be accessed [here](https://sambourgault.github.io/coilCAM-js/).

## What is Digital Fabrication?
| ![digital-fab](../../images/about/cad-cam-coilcam.png) | 
|:--:| 
| *Standard Digital Fabrication Workflow*|

Digital fabrication is a manufacturing process where computer-controlled machines create physical objects. 3D printers use an additive process to create physical objects, constructing a print layer by layer using melted plastic, metal or clay.

Most digital fabrication workflows follow four steps:
1) Users design 3D models using Computer-Aided Design (CAD) software (Rhino, Fusion360, Blender, TinkerCAD, etc.) After they are satisfied with their design, users export their 3D model as an .stl, .obj or .3mf file.
2) Users pass this file through Computer-Aided Manufacturing (CAM) software (Cura, 3DPrinterOS, Slic3r, etc.), which slices the model into several layers. This aptly-named "slicer" software converts each layer into a machine-readable toolpath that can be interpreted by a 3D printer. 
3) The 3D printer receives a set of commands which tell it how to print the model. These commands are (often) written in a programming language called G-Code. A basic G-Code command tells the machine which coordinates to move towards, how much material to extrude, and how quickly to move to the new set of coordinates. Additional G-Code commands can tell the printer to pause, stop printing, or retract material: a full list of commands can be found [here](https://marlinfw.org/meta/gcode/).
4) The .gcode file is sent to a 3D printer, which creates the final model.

| ![cam-fab](../../images/about/cam-coilcam.png) | 
|:--:| 
| *CoilCAM Workflow*|

CoilCAM bypasses the first step of this process, directly manipulating the CAM toolpath to create models. Instead of designing a model and passing that model through a slicer, CoilCAM lets users *modify the CAM toolpath* to shape their model. This design method provides a greater level of control that is analogous to clay coiling, a traditional craft workflow.

## How do I build forms using CoilCAM?
The simplest CoilCAM workflow follows three steps:
1) Use the **Toolpath Unit Generator** function to create a basic toolpath. This function controls the position, radius, layer height, number of points per layer and number of layers in the final model. The Toolpath Unit Generator function will output an array of points, storing the x, y, z coordinate and print speed of every point along the toolpath.
2) Use the **GCode Generator** function to convert the outut from step 1 to a machine-readable toolpath.
3) Use the **Download GCode** function to save the output from step 2 as a .gcode file. G-Code can be read directly by 3D printers, including the PotterBot 10 Micro and PotterBot 10 Super, which were used to print examples in this tutorial. 
<div style="display: flex; align-items: flex-start;">
  <img src="../../images/about-toolpath-1.jpg" alt="Description" style="width: 20%; margin-right: 20px;">
  <pre style="flex: 1; margin: 0; padding: 0; font-family: monospace; white-space: pre-wrap;">
// Step 1: Create a basic toolpath 
var toolpath = toolpathUnitGenerator([0, 0, 0], 40, 6, 12, 35, [], [], [], [], [], []);
updatePath(toolpath); // (Optional) Display toolpath

// Step 2: Generate GCode
var gcode = generateGCode(toolpath, 6, 10);

// Step 3: Download GCode file
downloadGCode(gcode, "simple-vessel.gcode");
  </pre>
</div>

### Functions
Once this vessel is created, users can offset points along the toolpath using several functions. A full list of functions can be found at the [reference]({{< ref "/docs/documentation/_index.md" >}}) page. In this example, we
offset the radius of each layer of the model using a sine wave.
<div style="display: flex; align-items: flex-start;">
  <img src="../../images/about-toolpath-2.jpg" alt="Description" style="width: 20%; margin-right: 20px;">
  <pre style="flex: 1; margin: 0; padding: 0; font-family: monospace; white-space: pre-wrap;">
// Step 0: Modify toolpath using a function, then add that function to another
var sineWave = sinusoidal(8, 14, 0, 12, [], "");

// Step 1: Create a basic toolpath 
var toolpath = toolpathUnitGenerator([0, 0, 0], 40, 6, 12, 35, [], [], [], [], [], []);
updatePath(toolpath); // (Optional) Display toolpath

// Step 2: Generate GCode
var gcode = generateGCode(toolpath, 6, 10);

// Step 3: Download GCode file
downloadGCode(gcode, "simple-vessel.gcode"); 
  </pre>
</div>

### Chaining Functions
Most importantly, functions can be added and multiplied to one another to form complex shapes. In this example, two sine waves are added together to modify the profile of the model.
<div style="display: flex; align-items: flex-start;">
  <img src="../../images/about-toolpath-3.jpg" alt="Description" style="width: 20%; margin-right: 20px;">
  <pre style="flex: 1; margin: 0; padding: 0; font-family: monospace; white-space: pre-wrap;">
// Step 0: Modify toolpath using a function, then add that function to another
var smallSineWave = sinusoidal(2, 4, 2, 12, [], "");
var sineWave = sinusoidal(8, 14, 0, 12, smallSineWave, "");

// Step 1: Create a basic toolpath 
var toolpath = toolpathUnitGenerator([0, 0, 0], 40, 6, 12, 35, [], [], [], [], [], []);
updatePath(toolpath); // (Optional) Display toolpath

// Step 2: Generate GCode
var gcode = generateGCode(toolpath, 6, 10);

// Step 3: Download GCode file
downloadGCode(gcode, "simple-vessel.gcode"); 
  </pre>
</div>

By chaining multiple functions together, and joining shapes using union or difference functions, CoilCAM can create complex and precise clay forms. 

### Next Steps
The [tutorial]({{< ref "/docs/tutorial/_index.md" >}}) page provides a step-by-step tutorial for using the Toolpath Unit Generator function.

The [reference]({{< ref "/docs/documentation/_index.md" >}}) page provides a list of CoilCAM functions, with in-browser visualizations for each one.






