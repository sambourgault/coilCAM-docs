+++
title = 'web editor'
date = 2024-04-13T15:42:11-06:00
draft = false
weight = 10
[params]
  math = true
+++

# Web Editor
This tutorial demonstrates how to navigate the [CoilCAM-js web editor](https://sambourgault.github.io/coilCAM-js/).

## Layout
*picture placeholder*

The web editor is divided into three sections: a file upload area, a code editor and a toolpath visualizer. At the top is a menu bar containing the following options:

*picture placeholder*

- run: Runs the code in the code editor.
- save: Saves the code in the code editor as a .txt file.
- upload: Uploads .txt files to the code editor.
- examples: Provides a list of example vessels to experiment with.
- printer dimensions: Changes the printer dimensions in the toolpath visualizer.
- documentation: Links to the documentation site.
- github: Links to the CoilCAM-js source code.



Try selecting the "demo vase" example from the dropdown. Then, make changes to the scalingParameter, layerRotation and thicknessParameter and press the "run" button to see those changes reflected in the toolpath visualizer.

*gif placeholder*

When you are satisfied with your changes, uncomment the generateGCode and downloadGCode lines (## and ##) and press "run" to download your toolpath as a gcode file.

## Additional Resources
Additional examples are available through the [examples]({{< ref "/docs/examples/_index.md" >}}) tab, and code from these examples can be pasted into the web editor. Similarly, each step of the [tutorial]({{< ref "/docs/tutorial/_index.md" >}}) can be pasted into the web editor.

