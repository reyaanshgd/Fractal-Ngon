# 3D Polygon Fractal

An interactive, zoomable 3D fractal built with Three.js. A regular polygon is extruded into a thin prism. At each vertex, a smaller copy of the prism (scaled by about 0.382) is placed and raised along the Z axis. The pattern repeats. Only the parts of the fractal you can currently see are generated, so you can keep zooming in and new detail appears.

## Features
- Adjustable polygon: 3 to 20 sides.
- Adjustable 3D height: controls how far each generation is lifted along Z (0 to 300). At 0 the fractal is flat.
- Detail on demand: each frame, the fractal is subdivided only where a prism is large enough on screen (about 28 px) and inside the camera view. Everything else is skipped.
- Prisms are drawn as one InstancedMesh, and their edges are merged into a single line buffer.
- Live zoom readout and prism count in the control panel.
- Draggable control panel you can move out of the way.
## Controls
- Left-drag to rotate the view
- Right-drag to pan
- Scroll to zoom in or out
- Double-click, or the reset view button to return to the starting view
- Sides input to change the polygon (3 to 20)
- 3D height input to change the vertical offset between generations
## Running it

The page loads Three.js (v0.160.0) from the unpkg CDN through an import map, so you need an internet connection and a browser with WebGL.

## How it works
The base shape is a regular N-gon with radius 250, extruded into a prism 40 units thick. Each prism spawns one child per vertex. A child sits at 0.618 × vertex from its parent, is raised by height, and is scaled by 1 − 0.618 ≈ 0.382. Every time the camera changes, the tree is rebuilt breadth-first:
Nodes outside the camera frustum are dropped. Nodes whose projected radius is under 28 px become leaves and are drawn. Larger nodes are subdivided, up to a cap of 24000 / sides prisms (minimum 400) and 60 levels deep. The visible prisms are written into an instanced mesh with a merged wireframe, and the ratio of the starting camera distance to the current one gives the zoom readout.

## Settings in the code

These constants and numbers near the top of the script are easy to adjust:

R: base polygon radius.
RATIO: scale factor per generation. The child offset also uses 0.618.
maxVisiblePrisms: prism budget. Raise it for more detail at the cost of speed.
pixelRadius < 28: the screen-size threshold at which subdivision stops.
Colors: the solidMaterial, edgeMaterial and light definitions.
Known limitations
Float32 precision: at very deep zoom levels, positions lose precision and the geometry will jitter or break up. Re-centering the scene on the zoom target would push this limit much further.
Full rebuild on every camera change: the mesh and edge buffer are regenerated each time. This is fine at the current prism cap but gets heavy if you raise it a lot.
Dependencies
Three.js 0.160.0 and its OrbitControls add-on, both loaded from unpkg.

# Cresent Fractal n-gon V.1

Give user the ability to add, toggle, and create infinite shapes, to their liking!

## DEMO

https://reyaanshgd.github.io/Cresent-Fractal-pentagon/

## Controls

- Adjust the number of sides, using the dragable box.
- use the reset view button, to return to original.
- zoom in by scrolling, and explore the canvas infinitly!
