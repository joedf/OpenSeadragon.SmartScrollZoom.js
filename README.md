# OpenSeadragon.SmartScrollZoom.js
This is a small, simple plugin for OpenSeadragon, which detects how fast the user is scrolling the mouse wheel and increases the zoom speed accordingly.

## Fork Differences
- `viewer.smartScrollZoom()` can be used to instantiate or modify the current smartScrollZoom instance. Before you had to call `.toggleEnable()` or `.setOptions()` on `viewer.smartScrollZoomInstance`.
  - now you do `smartScrollZoom('toggleEnable')` and `smartScrollZoom({ ... option ... })` instead.
  - this also works to set options: `smartScrollZoom('setOptions', { ... option ... })` 
- Tweaked the default values to be less extreme
- Starts off enabled unless specified in options
- Scroll direction change is interpreted as a different scroll acceleration event. Otherwise, quickly scrolling in and out would also trigger the acceleration.
- added `smartScrollZoom('getOptions')`
- preserves and restores the original `zoomPerScroll` (before plugin init.) setting on disable.

## Quick Start

Download and include `openseadragon-smartScrollZoom.js` after OpenSeadragon on your website.

To use this plugin, include this after declaring a viewer instance:
`````javascript
viewer.smartScrollZoom({
  //Define your properties here
  minScrolls: ...,
  ...
});
`````
It would look something like this:
`````javascript
//Create Viewer object
var viewer = new OpenSeadragon(...);

//Define smartScrollZoom for this viewer
viewer.smartScrollZoom({
  minScrolls: ...,
  timeThreshold: ...,
  zoomIncrement: ...,
  ...
});
`````

## Properties
Here's a list of the properties that can be defined, taken directly from the source code:
1. timeThreshold {Number} - Amount of time, in milliseconds, that the minimum number of scrolls must occur within before logic begins.

2. minScrolls {Number} - Required number of consecutive scrolls that must take place within the specified time threshold of each other before logic begins.

3. minZoomPerScroll {Number} - Minimum factor to zoom by with a single scroll. Setting this to 1 will affectively result in no zoom while logic is not being executing.

4. maxZoomPerScroll {Number} - Maximum zoom factor that can be reached.

5. zoomIncrement {Number} - Amount to increment zoom factor by with every scroll after minScrolls

6. enabled {Boolean} - Whether or not the scroll zoom logic is currently active

To change a property, call the SmartScrollZoom object with the changed property. For example, if you wanted to change the minScrolls property to 4 scrolls:
`````javascript
viewer.smartScrollZoom({
  minScrolls: 4,
  ...
});
`````
To toggle on and off the enabled property, call toggleEnable():

`````javascript
viewer.smartScrollZoom('toggleEnable');
`````
