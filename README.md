<div align="center">
  <img
    width="345"
    height="449"
    alt="FoamGraph"
    src="https://raw.githubusercontent.com/nikholt1/FoamGraph/refs/heads/main/foamGraph.png"
  />

  <h1>FoamGraph</h1>
</div>
**A lightweight, reusable JavaScript library for interactive graph visualizations.**

FoamGraph makes it easy to integrate an interactive, Obsidian-style graph into any web project. It is designed to be simple to embed, easy to configure, and flexible enough to visualize different types of connected data.

Instead of building a graph visualization from scratch, you can import FoamGraph, provide a designated HTML element, and populate the graph with your own nodes and relationships.

## Features

- **Simple integration:** Place a `<div id="form-graph"></div>` wherever you want the graph to appear.
- **Reusable:** Integrate the library into existing or new web projects.
- **Flexible data:** Represent notes, files, components, or other entities as connected nodes.
- **Relationship mapping:** Define connections between nodes to visualize how your data relates.
- **Interactive visualization:** Explore and interact with the graph through its visualization interface.
- **Local or online usage:** Import the library from a local file or reference a hosted version.
<img width="604" height="541" alt="image" src="https://github.com/user-attachments/assets/18d213ca-de7f-4627-87aa-91b519603688" />

## How It Works

FoamGraph is built with JavaScript, HTML, and CSS. JavaScript handles the graph's data, relationships, rendering, and interaction logic, while HTML provides the mounting point and CSS controls its presentation.

The library separates the visualization engine from the application using it. Your application supplies the data, while FoamGraph handles displaying that data as a graph.

The graph is mounted inside a specific HTML element identified by `form-graph`. This means you can position it anywhere in your existing page layout without restructuring the rest of your application.

```html
<div id="form-graph"></div>
```

The element can be placed inside a section, a dashboard, a sidebar, or any other container in your application. FoamGraph uses that element as its rendering target.

## Getting Started

FoamGraph supports two integration approaches, depending on how you want to use the library.

### 1. Local Integration

Download or copy the FoamGraph.js file and place it in your repository. Reference it in your HTML or JavaScript.

See [`local.html`](./local.html) for a ready-to-use example of local integration.

### 2. Online Integration

### 2. Online Integration

Import FoamGraph directly from this repository using jsDelivr. This allows you to integrate the library into your project without downloading or copying the source files.

```javascript
import "https://cdn.jsdelivr.net/gh/nikholt1/FoamGraph@main/FoamGraph.js";
```

Add the required graph container to your HTML:

```html
<div id="form-graph"></div>
```

FoamGraph can then be integrated into your existing application using its API.


See [`online.html`](./online.html) for a ready-to-use example of online integration.

Both examples demonstrate how to get the graph running quickly. Use them as starting points when integrating FoamGraph into your own system.

## Providing Data

FoamGraph represents information as nodes and relationships. Each node can contain identifying information, a display title, and optional configuration such as its size, color, parent, or connections, depending on the supported API.

For example, a graph representing a software project could contain nodes for the entry point, JavaScript modules, HTML pages, and external services. Connections between these nodes can represent imports, dependencies, or navigation paths.

Your application remains responsible for deciding what the data represents. FoamGraph provides the visualization layer that turns that data into a connected graph.

Refer to the source code and integration examples for the exact data structure and available methods.

## Integration Concept

The basic integration follows three steps:

1. Add `<div id="form-graph"></div>` wherever the graph should appear.
2. Import or reference the FoamGraph library and its required resources.
3. Initialize the graph and supply your nodes and relationships using its API.

Once integrated, the graph becomes part of your existing application rather than a separate page or application of its own.

## Use Cases

FoamGraph can be used to visualize:

- Knowledge graphs and interconnected notes.
- Software architecture and module dependencies.
- Repository structures and file relationships.
- Project data and related entities.
- Any dataset that can be represented as nodes and connections.

### Example: Portfolio Website

FoamGraph is used in my [Portfolio Website](https://nikholt1.github.io/#github) to visualize the structure of the website and show how its different components and files relate to each other.

This demonstrates how FoamGraph can be integrated into a real project to explore and visualize the relationships within an existing system.
## Examples

| Example | Description |
| --- | --- |
| [`local.html`](./local.html) | Integrate FoamGraph using local files. |
| [`online.html`](./online.html) | Integrate FoamGraph using an online-hosted version. |

## Project Goal

FoamGraph aims to make interactive graph visualization accessible through a reusable, easy-to-integrate JavaScript library. By keeping the graph engine separate from the application data, it can be adapted to different projects without requiring each application to implement its own visualization system.
