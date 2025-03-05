+++
title = 'examples'
date = 2024-04-13T15:43:45-06:00
draft = false
weight = 10
[params]
  math = true
+++

# Examples

Examples of complex forms made with CoilCAM-js are listed below.

### Micro Demo Vessel
Vase created by [Devon Frost](https://devnfrost.com/projects.html) for [CoilCAM](https://github.com/sambourgault/coilCAM/blob/main/Examples/CoilCAM_PBMicroDemoVessel.gh).

{{< tabs "Micro Demo Vessel">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=docs-examples&example=CoilCAM_MicroDemoVessel" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Micro Mug"></iframe>
{{% /tab %}}
{{% tab "Toolchains" %}}
*Toolchain coming soon*
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// Created by Devon Frost for CoilCAM (https://github.com/devonkay223)

// POTTERBOT CONFIG
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 5.0;
var potterbot_layerHeight = 2.5;
var potterbot_bedSize = [280, 265, 305];

//--Main Vessel
var nbLayers = 60;
var nbPointsInLayer = 42;
var main_position = [0.0, 0.0, potterbot_layerHeight*2];
var radius = 48;

// RADIUS SHAPING PARAMETER
var rsp = square(2.6, 7.0, 0.0, 3.0, nbPointsInLayer, [], "additive");

// SCALING SHAPING PARAMETER
var ssp1 = sinusoidal(0.4, 7.0, 0.3, nbLayers, [], "additive");
var ssp2 = linear(-0.033, 0.0, nbLayers, ssp1, "additive");
var ssp3 = sinusoidal(12.0, 63.0, 6.15, nbLayers, ssp2, "additive");

// SCALING RADIUS SHAPING PARAMETER
var srsp = linear(-0.03, 1.8, nbLayers, [], "additive");

// ROTATION PARAMETER
var rtsp = staircase(3.0, 30.0, 3.0, nbLayers, [], "");

//--Spout
// SCALING SHAPING PARAMETER
var spout_ssp = linear(0.63, 0.0, 60, [], "additive");
var spout_tsp = linear2D(0.712, 0.0, 0.0, 0.0, 60, [], [], "")

// TOOLPATH UNIT GENERATORS
var baseToolpath = toolpathUnitGenerator(main_position, radius, potterbot_layerHeight, nbLayers=60, nbPointsInLayer=42, rsp, ssp3, srsp, [], rtsp);
var spoutToolpath = toolpathUnitGenerator([-25.0, 0.0, potterbot_nozzleDiameter*2], 5, potterbot_layerHeight, nbLayers=58, nbPointsInLayer=3, [], spout_ssp, [], spout_tsp, []);
var toolpath = union(baseToolpath, spoutToolpath);
let lowerBase = baseFill([0, 0, 0], radius, nbPointsInLayer, potterbot_nozzleDiameter, baseToolpath);
let upperBase = baseSpiral([0, 0, potterbot_layerHeight], nbPointsInLayer, potterbot_nozzleDiameter, radius);
toolpath = lowerBase.concat(upperBase.concat(toolpath));
// toolpath = centerPrint(toolpath, main_position, potterbot_bedSize, potterbot_layerHeight);
updatePath(toolpath);

// GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter, potterbot_printSpeed);
//downloadGCode(gcode, "CC_microdemovessel.gcode");
```
{{% /tab %}}
{{% tab "CoilCAM" %}}
<a href="/data/CoilCAM_PBMicroDemoVessel.gh" download="checkerboard-bowl.json">Download Micro Demo Vessel Grasshopper File</a>
{{% /tab %}}
{{< /tabs >}}


### Micro Example Mug
Hourglass-shaped cup created by [Sam Bourgault](https://sambourgault.com) for [CoilCAM](https://github.com/sambourgault/coilCAM/blob/main/Examples/CoilCAM_PBMicroExampleMug.gh).

{{< tabs "Micro Example Mug">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=docs-examples&example=CoilCAM_MicroExampleMug" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Micro Mug"></iframe>
{{% /tab %}}
{{% tab "Toolchains" %}}
*Toolchain coming soon*
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// Created by Sam Bourgault for CoilCAM (https://github.com/sambourgault)

//POTTERBOT CONFIG
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 5.0;
var potterbot_layerHeight = 2;
var potterbot_extrusionMultiplier = 1.0;
var potterbot_bedSize = [280, 265, 305];

//--Main Vessel
var nbLayers = 60;
var ssp1 = linear(-0.09, 0.0, nbLayers, 0, "");
var ssp2 = sinusoidal(4.0, 50, 7.0, nbLayers, ssp1, "additive");
var toolpath_main = toolpathUnitGenerator([0.0, 0.0, 4.5], 42.00, potterbot_layerHeight, 60, 30, [], ssp2, [], [], [], []);

//--Subtracted vessel 1
var sub1_tsp1 = sinusoidal2D(9.399, 50, 0, 50, 12, 40, 0, 0, "");
var sub1_tsp2 = linear2D(-0.251, 48.0, 0.0, 0.0, 40.0, sub1_tsp1[0], sub1_tsp1[1], "additive");
var toolpath_subtracted1 = toolpathUnitGenerator([19.0, 0.0, 4.5], 24.18, potterbot_layerHeight, 40, 30, [], [], [], sub1_tsp2, []);
//--Subtracted vessel 2
var sub2_tsp1 = sinusoidal2D(9.399, 50, 0, 50, 15.8, 40, 0, 0, "");
var sub2_tsp2 = linear2D(0.388, 48, 0.0, 0.0, 40, sub2_tsp1[0], sub2_tsp1[1], "additive");
var toolpath_subtracted2 = toolpathUnitGenerator([-118.0, 0.0, 4.5], 24.18, potterbot_layerHeight, 40, 30, [], [], [], sub2_tsp2, [], []);

// TOOLPATH + GCODE
var toolpath = difference(difference(toolpath_main, toolpath_subtracted1), toolpath_subtracted2);
updatePath(toolpath);
var gcode = generateGCode(toolpath, layerHeight, potterbot_nozzleDiameter);
// Boolean Union Vase
// -- Complex example to demonstrate union between six smaller vessels and a main vase

// POTTERBOT CONFIGURATION
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 6.0;
var potterbot_layerHeight = 2.5;
var potterbot_bedSize = [280, 265, 305];

// -- Parameters for 6 smaller vessels
var nbLayers = 50;
var nbPointsInLayer = 24;
var radius = 18.0;
let position = [0, 0, potterbot_layerHeight*2];
var rsp = sinusoidal(4.0, 6.0, 30.0, nbPointsInLayer, [], "multiplicative");
var ssp1 = sinusoidal(1,12.0, 55.0, nbLayers, [], "additive");
var ssp2 = linear(0.35, 1, nbLayers, ssp1, "additive");
var ssp3 = linear(-0.45, 4, nbLayers, ssp2, "additive");

var ssp = sinusoidal(2,30.0, -9.0, nbLayers, ssp3, "additive");

// -- Union smaller vessels
let vessels = [];
let num_copies = 6;
var bool_vessels = [];
for (let i = 0; i < num_copies; i++){
  	var rotateSP = sinusoidal(3.0, 5.0, 0, 12, [], "multiplicative");
    vessels[i] = toolpathUnitGenerator([(32)*Math.sin(i*2*Math.PI/num_copies),(32)*Math.cos(i*2*Math.PI/num_copies), position[2]], radius, potterbot_layerHeight, nbLayers, nbPointsInLayer, rsp, ssp, [], [], (288*i)+240);
    if(i > 0){
        vessels[0] = union(vessels[i], vessels[0], true);
    }
}
bool_vessels = vessels[0];

// -- Build main cup
let vesselRadius = 45;
let main_vessel = toolpathUnitGenerator(position, vesselRadius, potterbot_layerHeight, nbLayers, nbPointsInLayer*1.5, [], [], [], [], [], []);
let toolpath = union(main_vessel, bool_vessels);

// -- Add base, spiralize, center
let lowerBase = baseFill([0, 0, 0], vesselRadius, nbPointsInLayer, potterbot_nozzleDiameter, toolpath);
let upperBase = baseFill([0, 0, potterbot_layerHeight], vesselRadius, nbPointsInLayer, potterbot_nozzleDiameter,toolpath, 0, 90);
toolpath = spiralize(toolpath, potterbot_layerHeight);
toolpath = lowerBase.concat(upperBase).concat(toolpath);
toolpath = centerPrint(toolpath, position, potterbot_bedSize, potterbot_layerHeight);
updatePath(toolpath);

// GENERATE GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter, potterbot_printSpeed);
//downloadGCode(gcode, "CC_microexamplemug.gcode");
```
{{% /tab %}}
{{% tab "CoilCAM" %}}
<a href="/data/CoilCAM_PBMicroExampleMug.gh" download="checkerboard-bowl.json">Download Micro Example Mug Grasshopper File</a>
{{% /tab %}}
{{< /tabs >}}

### Checkerboard Bowl
Bowl with checkerboard pattern created by thickness parameter.

{{< tabs "Checkerboard Bowl">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=web-editor&example=CheckerboardBowl" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Micro Mug"></iframe>
{{% /tab %}}
{{% tab "Toolchains" %}}
<a href="/data/checkerboard-bowl.json" download="checkerboard-bowl.json">Download Checkerboard Bowl Toolchain</a>
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// CHECKERBOARD BOWL
// -- Bowl with checkerboard pattern from thickness parameter.

// POTTERBOT CONFIGURATION
var potterbot_nozzleDiameter = 4.0;
var potterbot_layerHeight = potterbot_nozzleDiameter/2;

// BOWL PARAMETERS
var position = [150, 150, potterbot_layerHeight*2];
var radius = 40;
var nbLayers = 24;
var nbPointsInLayer = nbLayers*2;

// -- Shaping parameters
var scaleParameter = sinusoidal(18, 84, -6.25, nbLayers, 0, "");
var rotationParameter = staircase(4, 32, 0, nbLayers, 0, "");
var thicknessParameter = square(1, nbPointsInLayer/8, 0, 4, nbLayers*nbPointsInLayer, 0, "");

// BUILD VESSEL
var toolpath = toolpathUnitGenerator(position, radius, potterbot_layerHeight, nbLayers, nbPointsInLayer, [], scaleParameter, [], [], rotationParameter, thicknessParameter);
var toolpathBase = base(position, radius, potterbot_layerHeight, nbPointsInLayer, potterbot_nozzleDiameter, toolpath)
toolpath = toolpathBase.concat(toolpath);
updatePath(toolpath);

// GENERATE GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter);
//downloadGCode(gcode, "checkerboard_bowl_example.gcode");
```
{{% /tab %}}
{{< /tabs >}}


### Union Difference Mug
Mug that demonstrates union and difference functions.

{{< tabs "Union Difference Mug">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=docs-examples&example=UnionDifferenceMug" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Micro Mug"></iframe>
{{% /tab %}}
{{% tab "Toolchains" %}}
<a href="/data/union-diff-mug.json" download="checkerboard-bowl.json">Download Union Difference Mug Toolchain</a>
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// UNION DIFFERENCE MUG
// -- Mug with a handle made through a union function 
// -- and indentation made through a difference function.

// POTTERBOT CONFIGURATION
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 5;
var potterbot_layerHeight = potterbot_nozzleDiameter*.5;
var potterbot_extrusionMultiplier = 1.0;
var potterbot_bedSize = [280, 265, 305];

// MAIN VESSEL PARAMETERS
var position = [150, 150, potterbot_layerHeight*2];
var radius = 48;
var nbLayers = 40;
var nbPointsInLayer = 50;

// HANDLE PARAMETERS (UNION)
var handlePosition = [140, 150, 20];
var handleRadius = 20;
var handleNbLayers = 34;
var handleNbPointsInLayer = 30;

// INDENT PARAMETERS (DIFFERENCE)
var indentPosition = [-10, 150, 50];
var indentRadius = 60;
var indentNbLayers = 22;
var indentNbPointsInLayer = 30;

// -- Shaping parameters for union and difference
var radiusParameter = sinusoidal(5, 15, 1.5, handleNbPointsInLayer, [], "");
var translateParameter = sinusoidal2D(60, 120, 5.3, 0.5, 5, 1, handleNbLayers, [], "");

// BUILD VESSEL
var mugToolpath = toolpathUnitGenerator(position, radius, potterbot_layerHeight, nbLayers, nbPointsInLayer, [], [], [], [], [], []);
var handleToolpath = toolpathUnitGenerator(handlePosition, handleRadius, potterbot_layerHeight, handleNbLayers, handleNbPointsInLayer, radiusParameter, [], [], translateParameter, [], []);
var indentToolpath = toolpathUnitGenerator(indentPosition, indentRadius, potterbot_layerHeight, indentNbLayers, indentNbPointsInLayer, radiusParameter, [], [], translateParameter, [], []);
var toolpathBase = base(position, radius, potterbot_layerHeight, nbPointsInLayer, potterbot_nozzleDiameter, mugToolpath);
var toolpath = union(difference(mugToolpath, indentToolpath), handleToolpath);
toolpath = spiralize(toolpath, potterbot_layerHeight);
toolpath = toolpathBase.concat(toolpath);
updatePath(toolpath);

// GENERATE GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter);
// downloadGCode(gcode, "union_difference_mug.gcode"); 
```
{{% /tab %}}

{{< /tabs >}}

### Difference Candleholder
Candle holder with a groove made through a difference function.
{{< tabs "Candleholder">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=docs-examples&example=DifferenceCandleHolder" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Candleholder"></iframe>
{{% /tab %}}
{{% tab "Toolchains" %}}
<a href="/data/difference-candleholder.json" download="difference-candleholder.json">Download Difference Candleholder Toolchain</a>
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// DIFFERENCE CANDLE HOLDER
// -- Candle holder with a groove made through a difference function.

// POTTERBOT CONFIGURATION
var potterbot_nozzleDiameter = 5.0;
var potterbot_layerHeight = potterbot_nozzleDiameter/2;

// VESSEL PARAMETERS
var position = [0.0, 0.0, potterbot_layerHeight*2];
var radius = 38;
var nbLayers = 60;
var nbPointsInLayer = 50;

// -- Shaping parameters
var radiusParameter = square(3, nbPointsInLayer/6, -1, nbPointsInLayer/20, nbPointsInLayer, [], "");
var scaleParameter = linear(-0.35, 0, nbLayers, [], "");
var grooveScaleParameter = exponential(-1.1, 1.1, 0.3, 0, nbLayers, [], "");
var translateParameter = linear2D(.25, 0, .25, 0, nbLayers, [],[], "");
var grooveTranslateParameter = linear2D(.45, 0, .45, 0, nbLayers, [],[], "");

// BUILD VESSEL
var toolpath = toolpathUnitGenerator(position, radius, potterbot_layerHeight, nbLayers, nbPointsInLayer, radiusParameter, scaleParameter, [], translateParameter, [], []);
var toolpathBase = base(position, radius, potterbot_layerHeight, nbPointsInLayer, potterbot_nozzleDiameter, toolpath);
var differenceToolpath = toolpathUnitGenerator([-radius*3/5, -radius*3/5, potterbot_layerHeight*2], radius/3, potterbot_layerHeight, nbLayers, nbPointsInLayer, [], grooveScaleParameter, [], grooveTranslateParameter, [], []);
toolpath = difference(toolpath, differenceToolpath);
toolpath = toolpathBase.concat(spiralize(toolpath, potterbot_layerHeight));
updatePath(toolpath);

// GENERATE GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter);
//downloadGCode(gcode, "candle_holder_difference_example.gcode");
```
{{% /tab %}}
{{< /tabs >}}

### Boolean Union Vase
Complex example to demonstrate union between six smaller vessels and a main vase.
{{< tabs "Boolean Union Vase">}}
{{% tab "Web Editor" %}}
<iframe src="https://sambourgault.github.io/coilCAM-js/simple-editor-index?folder=docs-examples&example=BooleanUnionVase" width="100%" style="height: 40vh;" style="border: none;" 
allowfullscreen="" webkitallowfullscreen="" mozallowfullscreen=""
title="Union Vase"></iframe>
{{% /tab %}}
{{% tab "Code" %}}
```javascript
// BOOLEAN UNION VASE
// -- Complex example to demonstrate union between six smaller vessels and a main vase.

// POTTERBOT CONFIGURATION
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 6.0;
var potterbot_layerHeight = 2.5;
var potterbot_bedSize = [280, 265, 305];

// -- Parameters for 6 smaller vessels
var nbLayers = 50;
var nbPointsInLayer = 24;
var radius = 18.0;
let position = [0, 0, potterbot_layerHeight*2];
var rsp = sinusoidal(4.0, 6.0, 30.0, nbPointsInLayer, [], "multiplicative");
var ssp1 = sinusoidal(1,12.0, 55.0, nbLayers, [], "additive");
var ssp2 = linear(0.35, 1, nbLayers, ssp1, "additive");
var ssp3 = linear(-0.45, 4, nbLayers, ssp2, "additive");

var ssp = sinusoidal(2,30.0, -9.0, nbLayers, ssp3, "additive");

// -- Union smaller vessels
let vessels = [];
let num_copies = 6;
var bool_vessels = [];
for (let i = 0; i < num_copies; i++){
  	var rotateSP = sinusoidal(3.0, 5.0, 0, 12, [], "multiplicative");
    vessels[i] = toolpathUnitGenerator([(32)*Math.sin(i*2*Math.PI/num_copies),(32)*Math.cos(i*2*Math.PI/num_copies), position[2]], radius, potterbot_layerHeight, nbLayers, nbPointsInLayer, rsp, ssp, [], [], (288*i)+240);
    if(i > 0){
        vessels[0] = union(vessels[i], vessels[0], true);
    }
}
bool_vessels = vessels[0];

// -- Build main cup
let vesselRadius = 45;
let main_vessel = toolpathUnitGenerator(position, vesselRadius, potterbot_layerHeight, nbLayers, nbPointsInLayer*1.5, [], [], [], [], [], []);
let toolpath = union(main_vessel, bool_vessels);

// -- Add base, spiralize, center
let lowerBase = baseFill([0, 0, 0], vesselRadius, nbPointsInLayer, potterbot_nozzleDiameter, toolpath);
let upperBase = baseFill([0, 0, potterbot_layerHeight], vesselRadius, nbPointsInLayer, potterbot_nozzleDiameter,toolpath, 0, 90);
toolpath = spiralize(toolpath, potterbot_layerHeight);
toolpath = lowerBase.concat(upperBase).concat(toolpath);
toolpath = centerPrint(toolpath, position, potterbot_bedSize, potterbot_layerHeight);
updatePath(toolpath);

// GENERATE GCODE
var gcode = generateGCode(toolpath, potterbot_layerHeight, potterbot_nozzleDiameter, potterbot_printSpeed);
//downloadGCode(gcode, "union_vase_example.gcode");

```
{{% /tab %}}
{{< /tabs >}}