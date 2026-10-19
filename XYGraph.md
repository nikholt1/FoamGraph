# XYGraph.js

A lightweight, dependency-free JavaScript library for rendering interactive 2D charts using HTML Canvas.

## Features

- Multiple chart types
- Simple `(x, y)` plotting
- Optional per-point colors
- Automatic axis scaling
- Custom axis labels and bounds
- Mouse dragging and zooming
- Configurable colors, grid, markers, and line widths
- Responsive canvas rendering

## Installation

Place `XYGraph.js` in your project and import it as an ES module.

```html
<div id="xy-graph"></div>

<script type="module">
    import XYGraph from "./XYGraph.js";
</script>
```

The library automatically finds the `#xy-graph` element and creates its canvas.

**Important:** Run the HTML through a local development server rather than opening it directly using `file://`. For example, use VS Code Live Server.

## Basic Usage

```javascript
import XYGraph from "./XYGraph.js";

XYGraph.setType = "line";

XYGraph.setX = "Time";
XYGraph.setY = "Value";

XYGraph.plot(0, 0);
XYGraph.plot(1, 10);
XYGraph.plot(2, 15);
XYGraph.plot(3, 12);
```

The first argument is the X coordinate, and the second is the Y coordinate.

The graph automatically adjusts its bounds to fit the data, including the origin `(0, 0)`.

## Chart Types

Set the chart type before plotting data.

```javascript
XYGraph.setType = "line";
```

Available chart types:

| Type | Description |
|---|---|
| `line` | Connects points with straight lines |
| `scatter` | Displays individual points |
| `pillar` | Vertical pillars from the X-axis |
| `bar` | Horizontal bars |
| `area` | Fills the area beneath the plotted line |
| `step` | Connects points using step-shaped lines |
| `stem` | Displays vertical stems with point markers |
| `smooth` | Connects points with a smooth curve |

## Plotting Data

### Plot a single point

```javascript
XYGraph.plot(5, 20);
```

### Plot multiple points

```javascript
const points = [
    [0, 0],
    [1, 4],
    [2, 7],
    [3, 5],
    [4, 10]
];

for (const [x, y] of points) {
    XYGraph.plot(x, y);
}
```

### Custom colors per point

Pass an optional third argument to set a point's color.

```javascript
XYGraph.plot(0, 0);
XYGraph.plot(1, 10, "#ff5252");
XYGraph.plot(2, 15, "#4ade80");
XYGraph.plot(3, 12, "#c084fc");
```

When no color is provided, the default chart colors are used.

For line-based charts, the segment leading to a colored point uses that point's color. Point colors also apply to markers and supported individual bar, pillar, stem, and scatter elements.

Area fill uses the configured area color.

## Chart Adjustments

All adjustments are made directly through `XYGraph` properties.

### Axis labels

```javascript
XYGraph.setX = "Time (seconds)";
XYGraph.setY = "Temperature (°C)";
```

### Axis bounds

Set minimum and maximum values for each axis.

```javascript
XYGraph.setXMin = 0;
XYGraph.setXMax = 100;

XYGraph.setYMin = 0;
XYGraph.setYMax = 50;
```

To let the maximum follow the plotted data automatically, use `"plotMax"`:

```javascript
XYGraph.setXMax = "plotMax";
XYGraph.setYMax = "plotMax";
```

For a graph that starts at zero, set the minimum bounds to `0`:

```javascript
XYGraph.setXMin = 0;
XYGraph.setYMin = 0;
```

### Mouse interaction

```javascript
XYGraph.setDrag = true;
XYGraph.setZoom = true;
```

| Property | Description |
|---|---|
| `setDrag` | Enables dragging to move around the graph |
| `setZoom` | Enables mouse-wheel zooming |

Reset the view to the automatic data bounds:

```javascript
XYGraph.resetView();
```

Manual pan and zoom are preserved until the view is reset.

### Area fill

```javascript
XYGraph.setFill = true;
```

Enables the configured fill behavior where supported.

For an area chart:

```javascript
XYGraph.setType = "area";
XYGraph.setFill = true;
```

### Line and point styling

```javascript
XYGraph.setLineColor = "#58a6ff";
XYGraph.setLineWidth = 2.5;

XYGraph.setPointColor = "#58a6ff";
XYGraph.setPointRadius = 4;
```

### Chart-type colors

```javascript
XYGraph.setPillarColor = "#58a6ff";
XYGraph.setBarColor = "#58a6ff";
XYGraph.setAreaColor = "#58a6ff";
XYGraph.setStepColor = "#58a6ff";
XYGraph.setSmoothColor = "#58a6ff";
XYGraph.setStemColor = "#58a6ff";
```

### Pillar and bar sizing

```javascript
XYGraph.setPillarWidth = 12;
XYGraph.setPillarGap = 4;

XYGraph.setBarHeight = 12;
XYGraph.setBarGap = 4;
```

These settings control the dimensions and spacing of the respective chart elements.

### Background and colors

```javascript
XYGraph.setBackground = "#050505";
XYGraph.setGridColor = "#242a31";
XYGraph.setAxisColor = "#8b949e";
XYGraph.setTextColor = "#a1a1aa";
```

### Grid, ticks, and zero line

```javascript
XYGraph.setShowGrid = true;
XYGraph.setShowTicks = true;
XYGraph.setShowZeroLine = true;
```

### Maximum number of points

```javascript
XYGraph.setMaxPoints = 1000;
```

Use this setting to limit how many data points the graph retains, which can be useful for live data streams.

## Reading and Managing Data

### Get all plotted data

```javascript
const data = XYGraph.getData();

console.log(data);
```

The returned data contains the plotted points, including their coordinates and any assigned colors.

### Clear the graph

```javascript
XYGraph.clear();
```

Removes the plotted data.

### Refresh the graph

```javascript
XYGraph.refresh();
```

Requests a redraw of the graph.

### Destroy the graph

```javascript
XYGraph.destroy();
```

Destroys the current graph instance and its associated rendering resources.

## Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>XYGraph Example</title>

    <style>
        body {
            margin: 0;
            padding: 24px;
            background: #050505;
            color: #dcddde;
            font-family: Arial, sans-serif;
        }

        #xy-graph {
            width: 100%;
            height: 400px;
        }
    </style>
</head>
<body>
    <h1>XYGraph Example</h1>

    <div id="xy-graph"></div>

    <script type="module">
        import XYGraph from "./XYGraph.js";

        XYGraph.setType = "area";

        XYGraph.setX = "Time";
        XYGraph.setY = "Value";

        XYGraph.setXMin = 0;
        XYGraph.setYMin = 0;

        XYGraph.setXMax = "plotMax";
        XYGraph.setYMax = "plotMax";

        XYGraph.setDrag = true;
        XYGraph.setZoom = true;
        XYGraph.setFill = true;

        const points = [
            [0, 0],
            [1, 4],
            [2, 7],
            [3, 5],
            [4, 10],
            [5, 8],
            [6, 13],
            [7, 11],
            [8, 16],
            [9, 14]
        ];

        for (const [x, y] of points) {
            XYGraph.plot(x, y);
        }
    </script>
</body>
</html>
```

## License

Specify your chosen open-source license here, such as the MIT License.
