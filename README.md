 <div align="center">
  <img
    width="200"
    alt="FoamGraph"
    src="https://raw.githubusercontent.com/nikholt1/FoamGraph/refs/heads/main/foamGraph.png"
  />

  <h1>FoamGraph</h1>
</div>

**Lightweight, reusable JavaScript libraries for interactive graph and data visualization.**

This repository contains two standalone JavaScript libraries: **FoamGraph**, for visualizing connected data as an interactive graph, and **XYGraph**, for plotting data on a two-dimensional X–Y coordinate system.

Both libraries are designed to be easy to integrate into existing web projects, with minimal setup and no need to build visualization functionality from scratch.

## Libraries

### FoamGraph

FoamGraph makes it easy to integrate an interactive, Obsidian-style graph into any web project. It visualizes entities as nodes and their relationships as connections, making it useful for exploring complex structures and interconnected data.

<img width="604" alt="image" src="https://github.com/user-attachments/assets/18d213ca-de7f-4627-87aa-91b519603688" />

**Features**
- **Simple integration:** Mount the graph inside a designated HTML element.
- **Reusable:** Integrate it into existing or new web projects.
- **Flexible data:** Represent notes, files, components, or other entities as connected nodes.
- **Relationship mapping:** Define hierarchical relationships and additional connections.
- **Interactive visualization:** Explore, select, drag, and navigate nodes.
- **Local or online usage:** Import the library from a local file or a hosted CDN.

**Documentation:** [FoamGraph README](https://github.com/nikholt1/FoamGraph/blob/main/FoamGraph.md)

### XYGraph

XYGraph is a lightweight JavaScript plotting library for visualizing numerical data on a two-dimensional X–Y coordinate system. It supports multiple plot types and configurable axes, colors, and interactions.

<img width="604" alt="image" src="https://github.com/user-attachments/assets/d92f6611-283b-46f1-9468-8ca2e5b575f3" />


**Features**
- **Simple plotting API:** Add data points using `XYGraph.plot(x, y)`.
- **Multiple plot types:** Line, scatter, pillar, bar, area, step, stem, and smooth plots.
- **Configurable axes:** Set axis labels and minimum or maximum values.
- **Interactive navigation:** Support for dragging and zooming.
- **Custom styling:** Configure plot colors, grid lines, axes, and point appearance.
- **Local or online usage:** Import the library from a local file or a hosted CDN.

**Documentation:** [XYGraph README](https://github.com/nikholt1/FoamGraph/blob/main/XYGraph.md)

## Getting Started

Both libraries can be integrated independently. Use only the library that fits your application's visualization needs.

### 1. FoamGraph Integration

Add a container to your HTML:

```html
<div id="foam-graph" style="width: 100%; height: 600px;"></div>
```

Import FoamGraph from jsDelivr and populate it through its API:

```html
<script type="module">
  import "https://cdn.jsdelivr.net/gh/nikholt1/FoamGraph@main/FoamGraph.js";

  window.FoamGraph.pushNode({
    id: "project",
    title: "My Project"
  });

  window.FoamGraph.pushNode({
    id: "frontend",
    title: "Frontend",
    parentId: "project"
  });

  window.FoamGraph.pushNode({
    id: "backend",
    title: "Backend",
    parentId: "project"
  });
</script>
```

FoamGraph handles the graph rendering and interaction, while your application provides the data.

### 2. XYGraph Integration

Add a container to your HTML:

```html
<div id="xy-graph" style="width: 100%; height: 400px;"></div>
```

Import XYGraph and plot data points:

```html
<script type="module">
  import XYGraph from "https://cdn.jsdelivr.net/gh/nikholt1/FoamGraph@main/XYGraph.js";

  XYGraph.setType = "line";
  XYGraph.setX = "X";
  XYGraph.setY = "Y";

  XYGraph.plot(0, 0);
  XYGraph.plot(1, 4);
  XYGraph.plot(2, 7);
  XYGraph.plot(3, 5);
  XYGraph.plot(4, 10);
</script>
```

XYGraph handles the coordinate system, plotting, and configured interactions. Your application supplies the numerical data.

## How They Work

Both libraries are built with JavaScript, HTML, and CSS, but serve different visualization purposes.

| Library | Visualization | Typical data |
| --- | --- | --- |
| **FoamGraph** | Interactive node-and-link graph | Entities, relationships, dependencies |
| **XYGraph** | Two-dimensional X–Y plot | Numerical points, measurements, trends |

The libraries separate visualization logic from application logic. Your application determines what the data represents, while the selected library renders it in a visual format.

## Use Cases

**FoamGraph**
- Knowledge graphs and interconnected notes.
- Software architecture and module dependencies.
- Repository structures and file relationships.
- Project data and related entities.
- Exploring relationships within complex systems.

**XYGraph**
- Plotting mathematical functions and datasets.
- Visualizing measurements and experimental results.
- Comparing numerical values and trends.
- Displaying time-series or other ordered data.
- Embedding charts in dashboards and web applications.

## Portfolio Integration

FoamGraph is used in my [Portfolio Website](https://nikholt1.github.io/#github) to visualize the structure of the website and show how its components and files relate to each other.

This demonstrates how the library can be integrated into a real project to explore and visualize relationships within an existing system.

## Documentation

| Resource | Description |
| --- | --- |
| [FoamGraph.md](https://github.com/nikholt1/FoamGraph/blob/main/FoamGraph.md) | FoamGraph setup, API, configuration, and graph functionality. |
| [XYGraph.md](https://github.com/nikholt1/FoamGraph/blob/main/XYGraph.md) | XYGraph setup, plotting methods, plot types, and configuration. |

## Project Goal

The goal of these libraries is to make interactive visualization accessible through reusable, easy-to-integrate JavaScript components.

FoamGraph focuses on **relationships and connected structures**, while XYGraph focuses on **numerical data and coordinate-based plotting**. Together, they provide two distinct visualization approaches that can be integrated into a wide range of web projects.
