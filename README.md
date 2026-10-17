# FoamGraph

Example Usage:
```code

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FoamGraph Demo</title>
    <script type="module" src="./FoamGraph.js"></script>
</head>
<body>
    <div id="foam-graph" style="height: 500px; width: 500px;"></div>

    <script type="module">
        FoamGraph.pushNode({
            id: "parser",
            title: "Parser",
            parentId: "inspector",
            color: "#b9b9b9",
            size: 6,
            links: ["files", "metadata", "syntax", "validation", "formats"]
        });

        FoamGraph.pushNode({
            id: "files",
            title: "File Parser",
            parentId: "parser",
            color: "#34d399",
            size: 4
        });

        FoamGraph.pushNode({
            id: "metadata",
            title: "Metadata",
            parentId: "parser",
            color: "#34d399",
            size: 4
        });

        FoamGraph.pushNode({
            id: "syntax",
            title: "Syntax",
            parentId: "parser",
            color: "#34d399",
            size: 4
        });

        FoamGraph.pushNode({
            id: "validation",
            title: "Validation",
            parentId: "parser",
            color: "#34d399",
            size: 4
        });

        FoamGraph.pushNode({
            id: "formats",
            title: "Formats",
            parentId: "parser",
            color: "#34d399",
            size: 4
        });
    </script>
</body>
</html>

```