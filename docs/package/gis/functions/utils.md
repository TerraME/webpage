# Utils

Some basic and useful functions to handle file names.

## Functions

|   |   |
|---|---|
|[forEachLayer](#forEachLayer)|Second order function to traverse all the [Layers](../types/layer.md) of a given [Project](../types/project.md), applying a given function to each of its Layer.|

## **forEachLayer** 

Second order function to traverse all the [Layers](../types/layer.md) of a given [Project](../types/project.md), applying a given function to each of its Layer. If any of the function calls returns false, forEachLayer() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: A Project.
- **#2**: A user-defined function that takes a Layer as argument. It can optionally have a second argument with a positive number representing the position of the Layer in the vector of Cells. If it returns false when processing a given Layer, forEachLayer() stops and does not process any other Cell.

### Usage

```
import("gis")

filename = "emas-count.tview"

project = Project{
    file = filename,
    clean = true,
    author = "Almeida, R.",
    title = "Emas database",
    firebreak = filePath("emas-firebreak.shp", "gis"),
    river = filePath("emas-river.shp", "gis"),
    limit = filePath("emas-limit.shp", "gis")
}

forEachLayer(project, function(layer, index)
    print(index.."\t"..layer.rep)
end)

File(filename):deleteIfExists()
```