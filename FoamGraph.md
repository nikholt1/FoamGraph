# FoamGraph

FoamGraph is a lightweight, embeddable JavaScript graph visualization library. It renders interactive, interconnected nodes on an animated HTML Canvas using a circular branching layout.

It is designed for visualizing relationships between data, software components, files, metadata, projects, and other connected information.

## Features

- Circular branching node layout
- Parent-child relationships and custom graph links
- Automatically generated placeholder nodes
- Custom node titles, colors, and sizes
- Custom connection colors and widths
- Animated physics with spring forces, repulsion, and gentle movement
- Interactive node selection and dragging
- Canvas panning and zooming
- Selected-only or always-visible labels
- Automatic graph statistics showing node and link counts
- JavaScript API for adding, retrieving, and updating nodes and links
- No external libraries or API keys required

## 1. Installation

Download `FoamGraph.js` and place it in your project.

For example:

```text
my-project/
├── index.html
└── FoamGraph.js
```

Create a container with the ID `foam-graph`:

```html
<div id="foam-graph"></div>
```

Give the container a defined height so the graph has space to render:

```html
<style>
    #foam-graph {
        width: 100%;
        height: 600px;
    }
</style>
```

Import the library using an ES module:

```html
<script type="module">
    import "./FoamGraph.js";

    FoamGraph.pushNode({
        id: "root",
        title: "My Project"
    });
</script>
```

Alternatively, import the JavaScript file through a module script:

```html
<script type="module" src="./FoamGraph.js"></script>
```

The library automatically initializes when it detects the `#foam-graph` element. It also exposes its API globally through `window.FoamGraph`.

**Important:** Load the library after the graph container exists, or allow the library's automatic initialization to run when the DOM is ready. Use a local development server for local testing.

## 2. Basic Usage

The simplest graph consists of a root node and several children.

```javascript
FoamGraph.pushNode({
    id: "project",
    title: "My Project"
});

FoamGraph.pushNode({
    id: "frontend",
    title: "Frontend",
    parentId: "project"
});

FoamGraph.pushNode({
    id: "backend",
    title: "Backend",
    parentId: "project"
});

FoamGraph.pushNode({
    id: "database",
    title: "Database",
    parentId: "backend"
});
```

This creates the following hierarchy:

```text
My Project
├── Frontend
└── Backend
    └── Database
```

FoamGraph calculates a circular branching layout from the hierarchy. The first root node is placed near the center of the graph, and its descendants are distributed around it.

You do not need to manually calculate the node coordinates.

## 3. Understanding Nodes

A node represents an individual item in the graph.

```javascript
FoamGraph.pushNode({
    id: "parser",
    title: "Parser",
    parentId: "inspector",
    color: "#34d399",
    size: 6
});
```

### Node properties

| Property | Description |
|---|---|
| `id` | Unique identifier used to find and connect nodes |
| `title` | Text displayed beside the node |
| `label` | Alternative to `title` when `title` is not provided |
| `parentId` | ID of the parent node in the branching layout |
| `color` | Node color in hexadecimal or another Canvas-compatible color format |
| `size` | Node radius in pixels before zoom scaling |
| `links` | Array of additional connections to other nodes |

The `id` is required. The other properties are optional.

If neither `title` nor `label` is provided, the node ID is used as its title.

### Node colors and sizes

```javascript
FoamGraph.pushNode({
    id: "frontend",
    title: "Frontend",
    color: "#60a5fa",
    size: 5
});

FoamGraph.pushNode({
    id: "backend",
    title: "Backend",
    color: "#34d399",
    size: 8
});
```

Larger nodes also influence the preferred spacing between connected nodes.

## 4. Parent-Child Relationships vs. Graph Links

FoamGraph supports two ways of defining relationships.

### Parent-child relationships

Use `parentId` to define the hierarchy used by the circular branching layout.

```javascript
FoamGraph.pushNode({
    id: "root",
    title: "Root"
});

FoamGraph.pushNode({
    id: "child",
    title: "Child",
    parentId: "root"
});
```

This creates a connection from `root` to `child` and places the child in the root's branch.

### Explicit graph links

Use `links` or `pushLink()` to create additional connections between nodes.

```javascript
FoamGraph.pushLink({
    source: "frontend",
    target: "backend"
});
```

An explicit link connects the nodes without changing their parent-child hierarchy.

This is useful when two components depend on each other even though they belong to different branches.

**Note:** A link is directional in the data (`source` to `target`), but the visualization draws it as a line without an arrowhead.

## 5. Creating Links

### Link using a node ID

You can define links directly inside a node.

```javascript
FoamGraph.pushNode({
    id: "parser",
    title: "Parser",
    parentId: "inspector",
    links: ["metadata", "validation", "formats"]
});
```

This creates connections from `parser` to each listed node.

If a target node does not exist yet, FoamGraph automatically creates a placeholder for it.

### Link using an object

Use an object when you want to customize a connection.

```javascript
FoamGraph.pushNode({
    id: "parser",
    title: "Parser",
    links: [
        {
            target: "metadata",
            color: "#60a5fa",
            width: 2
        }
    ]
});
```

The source defaults to the current node ID unless `source` is explicitly supplied.

### Link styling

```javascript
FoamGraph.pushLink({
    source: "frontend",
    target: "backend",
    color: "#c084fc",
    width: 2
});
```

| Property | Description |
|---|---|
| `source` | ID of the source node |
| `target` | ID of the target node |
| `color` | Optional custom line color |
| `width` | Optional line width |

Links must have both a source and a target. Self-links are rejected, and duplicate links with the same source and target are updated instead of duplicated.

## 6. Placeholder Nodes

One useful feature is that nodes can be referenced before they are fully defined.

```javascript
FoamGraph.pushLink({
    source: "frontend",
    target: "api"
});
```

If `frontend` and `api` do not exist, FoamGraph creates placeholder nodes for them.

A placeholder has the following initial properties:

```javascript
{
    id: "api",
    title: "api",
    parentId: null,
    placeholder: true
}
```

You can later define the actual node:

```javascript
FoamGraph.pushNode({
    id: "api",
    title: "REST API",
    color: "#fbbf24",
    size: 7
});
```

The existing node is updated instead of creating a second node with the same ID.

This is particularly useful when building a graph from data sources where relationships are discovered before every entity's details are available.

## 7. Updating Nodes and Links

Calling `pushNode()` with an existing ID updates that node's supplied properties.

```javascript
FoamGraph.pushNode({
    id: "api",
    title: "REST API",
    color: "#34d399",
    size: 8
});
```

Calling `pushLink()` with an existing source-target pair updates the properties of that link.

```javascript
FoamGraph.pushLink({
    source: "frontend",
    target: "backend",
    color: "#ff5252",
    width: 2
});
```

After adding or updating graph data, FoamGraph refreshes the layout and redraws the visualization.

**Important:** `pushNode()` updates the node properties supplied to it, but it does not remove old links merely because they are omitted from a later call. The current public API does not provide dedicated node or link deletion methods.

## 8. Retrieving Graph Data

FoamGraph exposes methods for retrieving individual nodes and graph data.

### Get a node

```javascript
const node = FoamGraph.getNode("parser");

console.log(node);
```

Returns the node object if found, otherwise `undefined`.

### Get all nodes

```javascript
const nodes = FoamGraph.getNodes();

console.log(nodes);
```

Returns a new array containing the graph's node objects.

### Get all explicit links

```javascript
const links = FoamGraph.getGraphLinks();

console.log(links);
```

Returns a new array containing copies of the explicit link objects.

**Note:** `getGraphLinks()` returns links created through the explicit link API. Parent-child connections are derived separately when the graph is rendered.

## 9. Interactive Controls

FoamGraph includes its own toolbar and interaction handlers.

### Zoom

Use the `+` and `−` buttons or scroll the mouse wheel.

- Minimum zoom: `20%`
- Maximum zoom: `300%`
- Mouse-wheel zoom is centered around the pointer position.
- Toolbar zoom is centered around the canvas.

### Pan

Click and drag empty canvas space to move around the graph.

You can also hold **Space** and drag over a node to pan rather than move that node. The canvas must have keyboard focus to receive the Space key.

### Move nodes

Click and drag a node to reposition it.

The node is temporarily held in place while dragged. After release, the physics simulation can move it toward its target position again.

### Select nodes

Click a node to select it.

When a node is selected:

- Its appearance is highlighted in purple.
- Its label becomes visible.
- Directly connected nodes are highlighted through their labels.
- Unrelated connections remain subdued.
- The footer displays the selected node's title and number of linked neighbors.

### Labels

Use the label selector in the toolbar.

| Mode | Behavior |
|---|---|
| `selected` | Show labels only for the selected node |
| `always` | Show labels for every node |

The default mode is `selected`.

### Reset

The toolbar's **Reset** button restores the zoom to `100%`, clears the current selection, and recenters the visible graph around its current node positions.

Reset does not delete nodes or links.

## 10. Circular Layout and Physics

FoamGraph combines a branching layout with a continuous physics simulation.

### Circular branching

The initial layout uses `parentId` to organize nodes into branches. Branches are allocated angular space based on the number of descendant leaves, helping larger branches receive more room.

The first root node is the main root. Additional root nodes are positioned relative to it.

### Automatic spacing

The preferred distance between connected nodes depends on their sizes.

```javascript
const combinedRadius = source.size + target.size;
```

Conceptually, the layout uses the combined node radii and a spacing factor to determine the desired link distance. The implementation also introduces small random variations to avoid a perfectly rigid arrangement.

### Physics simulation

The animation loop applies several forces:

- **Spring force:** pulls nodes toward their layout targets.
- **Edge force:** adjusts the distance between connected nodes.
- **Repulsion:** discourages nodes from clustering too closely.
- **Water movement:** adds subtle continuous motion.
- **Damping:** reduces velocity and stabilizes the graph.

The result is a graph that remains structured but feels dynamic.

These physics constants are currently internal implementation details, not public configuration properties.

## 11. Styling

FoamGraph injects its own CSS when initialized. Its default appearance uses a dark background, subtle borders, muted labels, and purple selection highlights.

The main CSS variables are:

```css
.obsidian-graph {
    --graph-bg: #050505;
    --graph-panel: #050505;
    --graph-border: #30363d;
    --graph-text: #dcddde;
    --graph-muted: #999;
    --graph-blue: #7f6df2;
    --graph-surface: #18232d;
}
```

You can override these variables in your own stylesheet:

```css
.obsidian-graph {
    --graph-bg: #0d1117;
    --graph-panel: #161b22;
    --graph-border: #30363d;
    --graph-text: #e6edf3;
    --graph-muted: #8b949e;
    --graph-blue: #58a6ff;
    --graph-surface: #21262d;
}
```

Node and link colors can also be configured individually through their data properties.

The graph resizes automatically using `ResizeObserver`, so its parent container should have a meaningful height.

## 12. Complete Example

The following example creates a small software architecture graph with hierarchical branches and additional cross-links.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>FoamGraph Example</title>

    <style>
        body {
            margin: 0;
            padding: 24px;
            background: #050505;
            color: #dcddde;
            font-family: Arial, sans-serif;
        }

        #foam-graph {
            width: 100%;
            height: 600px;
        }
    </style>

    <script type="module" src="./FoamGraph.js"></script>
</head>
<body>
    <h1>Software Architecture</h1>

    <div id="foam-graph"></div>

    <script type="module">
        // FoamGraph initializes automatically.
        // Add data after the module has loaded.

        FoamGraph.pushNode({
            id: "project",
            title: "Project",
            color: "#b9b9b9",
            size: 8
        });

        FoamGraph.pushNode({
            id: "frontend",
            title: "Frontend",
            parentId: "project",
            color: "#60a5fa",
            size: 6,
            links: ["api"]
        });

        FoamGraph.pushNode({
            id: "backend",
            title: "Backend",
            parentId: "project",
            color: "#34d399",
            size: 6,
            links: ["database"]
        });

        FoamGraph.pushNode({
            id: "api",
            title: "REST API",
            parentId: "backend",
            color: "#fbbf24",
            size: 5
        });

        FoamGraph.pushNode({
            id: "database",
            title: "Database",
            parentId: "backend",
            color: "#c084fc",
            size: 5
        });

        FoamGraph.pushLink({
            source: "frontend",
            target: "database",
            color: "#ff5252",
            width: 1.5
        });

        console.log(FoamGraph.getNodes());
        console.log(FoamGraph.getGraphLinks());
    </script>
</body>
</html>
```

In this example, `project` is the root node. `frontend` and `backend` are its children, while `api` and `database` belong to the backend branch.

The additional links represent relationships beyond the hierarchy. FoamGraph automatically creates the visualization and keeps the graph updated as nodes and links are added.

## 13. Public API Reference

| Method | Purpose |
|---|---|
| `FoamGraph.init()` | Initializes or reinitializes the graph UI |
| `FoamGraph.pushNode(node)` | Adds a node or updates an existing node |
| `FoamGraph.pushLink(link)` | Adds or updates an explicit connection |
| `FoamGraph.getNode(id)` | Retrieves a node by ID |
| `FoamGraph.getNodes()` | Retrieves the node array |
| `FoamGraph.getGraphLinks()` | Retrieves explicit graph links |

The module also exports the named functions `initializeInspector`, `pushNode`, `pushLink`, `getNode`, `getNodes`, and `getGraphLinks`.

The current public API does not expose methods for deleting nodes, deleting links, setting zoom programmatically, or configuring the internal physics constants.

## License

Add your chosen open-source license here. If you intend to distribute FoamGraph publicly, include the corresponding license file in the repository.