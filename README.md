## The terrain viewer accepts a duffle of data, and maps it to a three-dimensional terrain. The component features various options for binning data, coloring the terrain, lighting the terrain, configuring camera type and position, and more.

# Purpose
* Produces a three-dimensional terrain based on a duffle of data.
* Set options for the camera, scene, and terrain.
* Dynamically updates scene when options change.
* Outputs raw terrain data on command.

# Inputs
  * ** data **
    * ** x ** Duffle value selector for the x-axis.
    * ** y ** Duffle value selector for the y-axis.
    * ** z ** Duffle value selector for the z-axis.

  Example data:
  ```
  [
    {
      "disp": 160.0,
      "mpg": 21.0,
      "hp": 110,
      "model": "Mazda RX4"
    },
    {
      "disp": 400.0,
      "mpg": 19.2,
      "hp": 175,
      "model": "Pontiac Firebird"
    },
    ...
  ]
  ```

  * ** options **
    * _camera_ String that sets the camera type. Options are ```perspective``` and ```orthographic```.
    * _cameraSpeed_ An integer that sets the speed of the camera, in milliseconds, when it is snapping to a view.

  * ** getScene ** A dynamic input to output the current object that is creating the scene. Can be decoded to obtain information about the scene, or sent to an appropriate THREE.js component to render the scene.

  * ** sceneOptions **
    * _drawAxes_ A boolean value to draw or remove the axes helper (axes lines). Red indicates the positive x axis, green indicates the positive y axis, and blue indicates the positive z axis.
    * _controlType_ A string that sets the type of Three.js control system to use. Valid strings include `TrackballControls` and `OrbitControls`.

  * ** terrainOptions **
    * _resolution_ An integer to set the resolution at which the data is binned. A higher resolution generally results in more pronounced peaks in the terrain, and wider spaces of level terrain between the peaks.
    * _smooth_ An integer to set the smoothing radius of the data. The larger the smoothing radius, the more even the terrain will become. Experiment with small values (0-10) first, if using this feature.
    * _bestFitSmooth_ A boolean value that determines how the terrain is smoothed. A true value will average the height of the neighboring vertices around a peak and will attempt to fit those vertices to a sine wave. A false value will not average the values of the neighboring vertices before they are fit to a sine wave. A true value here will hold greater fidelity to the original data, while a false value will emphasize peaks and valleys.
    * _wireframe_ A boolean value that draws the terrain as a wireframe when set true. When false, the terrain has a colorized face.
    * _hexColor_ A color string that corresponds to the hex code that the terrain is to be colored by. Accepts color strings which do not begin with a hash. E.g., `ff00ff` is an acceptable color string.
    * _colorByZ_ A boolean value that if set true will increase the lighten the colors around vertices which are elevated above 0. In other words, the higher the Z value of a vertex, the lighter in color it will appear compared to flat terrain.
    * _colorByZScale_ A string value that, if _colorByZ_ is set true, will use one of d3.js' 34 built-in color interpolation scales to color the terrain by height. Some examples of acceptable strings include ```interpolateRainbow```, ```interpolateMagma```, and ```interpolateRdYlGn```. For a complete list of scales, [consult d3's documentation.](https://github.com/d3/d3-scale-chromatic)
    * _scaleZ_ A boolean value that if set true will scale the data to fill the vertical space of the terrain up a defied maximum.
    * _maxZ_ An integer value that sets the maximum z height possible for the terrain. The scaleZ terrain option must be set true for this option to work. For reference, the width and length of the terrain are always both 100 units.
    * _borderWidth_ An integer value that creates a flat border area at the edge of the terrain. The integer corresponds to the width of the border.
    * _alternatePinColors_ A boolean that, if set true, will have the terrain viewer generate different colors for each pin that is set by the user. There are 10 different colors for pinheads that the viewer will cycle through. If set false, the viewer will apply the default red color to all pinheads.
  Default options:
  ```
    {
      "resolution": 10,
      "smooth": 0,
      "bestFitSmooth": false,
      "wireframe": true,
      "hexColor": "dddddd",
      "colorByZ": true,
      "colorByZScale": "",
      "scaleZ": true,
      "logZ": false,
      "maxZ": 40,
      "borderWidth": 0,
      "alternatePinColors": false
    }
  ```

  * ** labelOptions ** Granular options to configure the appearance and position of axes labels.
    * _drawLabels_ A boolean value that determines whether labels are drawn.
    * _xLabel_ A string value that sets the text on the label for the X axis.
    * _yLabel_ A string value that sets the text on the label for the Y axis.
    * _zLabel_ A string value that sets the text on the label for the Z axis.
    * _xLabelPosition_ An array that determines the position of the X axis label, in [x,y,z] format.
    * _xLabelRotation_ An array that determines the rotation of the X axis label, in [α, β, γ] format.
    * _yLabelPosition_ An array that determines the position of the Y axis label, in [x,y,z] format.
    * _yLabelRotation_ An array that determines the rotation of the Y axis label, in [α, β, γ] format.
    * _zLabelPosition_ An array that determines the position of the Z axis label, in [x,y,z] format.
    * _zLabelRotation_ An array that determines the rotation of the Z axis label, in [α, β, γ] format.
    * _xValues_ An array containing any number of strings, to be placed on the x axis as value indicators. This text will be spaced in equal intervals along the axis.
    * _yValues_ An array containing any number of strings, to be placed on the x axis as value indicators. This text will be spaced in equal intervals along the axis.
    * _xValuesPosition_ An array that determines the position of the X axis values, in [x,y,z] format.
    * _xLabelRotation_ An array that determines the rotation of the X axis values, in [α, β, γ] format.
    * _yValuesPosition_ An array that determines the position of the Y axis values, in [x,y,z] format.
    * _yLabelRotation_ An array that determines the rotation of the Y axis values, in [α, β, γ] format.
    * _drawOutline_ A boolean value that, if set true, will place a black plane beneath the terrain.
    ```
      {
  			"drawLabels": true,
  			"xLabel": "X",
  			"yLabel": "Y",
  			"zLabel": "Z",
  			"xLabelPosition": [
  				-50,
  				-58,
  				0
  			],
  			"xLabelRotation": [
  				0,
  				0,
  				0
  			],
  			"yLabelPosition": [
  				-58,
  				-50,
  				0
  			],
  			"yLabelRotation": [
  				0,
  				0,
  				90
  			],
  			"zLabelPosition": [
  				-58,
  				58,
  				0
  			],
  			"zLabelRotation": [
  				90,
  				0,
  				90
  			],
  			"xValues": [],
  			"yValues": [],
  			"xValuesPosition": [
  				-50,
  				-58,
  				0
  			],
  			"xValuesRotation": [
  				0,
  				0,
  				0
  			],
  			"yValuesPosition": [
  				-58,
  				-50,
  				0
  			],
  			"yValuesRotation": [
  				0,
  				0,
  				90
  			],
  			"drawOutline": false
  		}
    ```
  * ** cameraOptions ** This is a granular port to set the positions for the position snaps for the camera. The camera can then be snapped to these preset positions by using the `snapToXZ`, `snapToYZ`, and `snapToXY` dynamic inputs.
    * _snapXZpos_ An array that determines the final position of the snapToXZ camera movement, in [x,y,z] format.
    * _snapYZpos_ An array that determines the final position of the snapToYZ camera movement, in [x,y,z] format.
    * _snapXYpos_ An array that determines the final position of the snapToXY camera movement, in [x,y,z] format.
    ```
      {
        "snapXZpos": [
          0,
          -125,
          0
        ],
        "snapYZpos": [
          125,
          0,
          0
        ],
        "snapXYpos": [
          0,
          0,
          175
        ]
      }
    ```

  * ** cameraPosition ** A granular input to change the camera's position. Write a new value to any of its inputs to automatically move the camera to the desired position.
    * _x_ Integer value for x position
    * _y_ Integer value for y position
    * _z_ Integer value for y position
    * _up_ An array of binary integer values (either 0 or 1), which determines the orientation of the camera.
    ```
      {
        "x": 0,
        "y": -100,
        "z": 100,
        "up": [
          0,
          1,
          0
        ]
      }
    ```

  * ** autoRotate ** A boolean value to activate or deactivate auto-rotation of the camera.

  * ** snapToXZ ** A dynamic input to snap the camera's view to the XZ plane.

  * ** snapToYZ ** A dynamic input to snap the camera's view to the YZ plane.

  * ** snapToXY ** A dynamic input to snap the camera's view to the XY plane.

  * ** pointList ** A port that configures a point of light to illuminate the landscape.
    * _light_ A boolean value to render or remove the point light source.
    * _xPos_ An integer value to set the x position of the light source.
    * _yPos_ An integer value to set the y position of the light source.
    * _zPos_ An integer value to set the z position of the light source.

  * ** pinOptions ** This is a port to configure the way the visualization handles interactive clicks and places pins in vertices.
    * _clickToPin_ A boolean value that, if set true, enables the user to set pins wherever they click on the terrain. Setting this value to false will retain the current pins, while preventing the user from adding more pins. The user must not click and drag their mouse across the terrain in order to drop a pin; only "hard clicks" will place a pin on the terrain.
    * _multiPins_ A boolean value, that if set true, will allow the user to add multiple mins to the terrain. If this is set to false, the previous pin or pins will be deleted when the user clicks to add a new pin.
    * _clearOnOutsideClick_ A boolean value, that if set true, will delete all pins on the terrain if the user clicks on somewhere other than the terrain.
    * _pinClosestVertex_ A boolean value, that if set true, will place new pins at the closest vertex to the user's mouse click. If set false, pins will be dropped directly at the user's mouse location.
    * _findClosestValues_ A boolean value, that if set true, will output the data closest to the user's pin. If set false, the component may output an empty array if the user does not directly click on a location where underlying data is present.
    ```
      {
        "clickToPin": false,
        "multiPins": false,
        "clearOnOutsideClick": false,
        "pinClosestVertex": false,
        "findClosestValues": false
      }
    ```

  * ** setPins ** This projection port accepts one or more entities from the original data duffle and places corresponding pins on the terrain.

  * ** deletePin ** This projection port accepts a single entity from the original data duffle and removes any corresponding pin, if any, from the terrain.

  * ** highlightPins ** This projection port accepts a single entity from the original data duffle and changes the color of the corresponding pin.

  * ** unHighlightPins ** A dynamic input that accepts any value to remove all highlights from pins on the terrain.

  * ** clearPins ** A dynamic input that accepts any value to clear all pins from the terrain.

  * ** clearScene ** A dynamic input that accepts any value to clear the entire scene.
