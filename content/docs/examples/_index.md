+++
title = 'examples'
date = 2024-04-13T15:43:45-06:00
draft = true
+++

# examples

This example shows how to create the toolpath for a simple vessel with sinusoidal functions used as shaping parameter for the radius and scale shaping parameters.

```javascript
//POTTERBOT CONFIG
var potterbot_printSpeed = 30;
var potterbot_nozzleDiameter = 5.0;
var potterbot_layerHeight = 1.8;
var potterbot_extrusionMultiplier = 1.0;
var potterbot_bedSize = [280, 265, 305];

//--Main Vessel
var nbLayers = 60;
var nbPointsInLayer = 30;
var rsp = sinusoidal(5, 5, 0, nbPointsInLayer, 0, "");
var ssp = sinusoidal(10, 15, 0, nbLayers, 0, "");
var toolpath_main = toolpathUnitGenerator([0.0, 0.0, 4.5], 42.00, potterbot_layerHeight, nbLayers, nbPointsInLayer, rsp, ssp, [], [], []);

updatePath(toolpath_main);
```