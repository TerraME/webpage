# Project

Project is a concept to describe all the data to be used by a given model. Data can be stored in different sources, with different formats and access. A project organises the data into a set of layers, storing all the information related to each data source internally. After that, the user can refer to the data sets only using the respective layer name. TerraME allows the modeler to create a Project from scratch or load one already created in another software of [TerraLib](./terralib.md) family.  
  

### Arguments

- **author**: An optional string with the name of the Project's author.
- **clean**: An optional boolean value indicating whether the argument file should be removed if it already exists. The default value is false.
- **directory**: An optional Directory where shapefile(s) and/or tiff file(s) are stored. When using this argument, all such files will be added to the project using the respective file names without extension as layer names. This argument can also be a string that will be converted to a Directory.
- **file**: A [File (base package)](../../../base/types/file.md) or a string with the file name to be used. If the file does not exist then it will be created. If it exists then it will be opened.
- **title**: An optional string with the title of the Project.
- **...**: Names of layers to be created from files. Each argument that has a string as value and does not belong to the arguments above will be converted into a layer. The name of the attribute will be used as layer name and its value as file name where data is stored. It can be a shapefile or a tiff.

### Usage

```
import("gis")

proj1 = Project{
    file = "myproject.tview"
}

proj2 = Project{
    file = "itaituba.tview",
    clean = true,
    deforestation = filePath("desmatamento_2000.tif", "gis"),
    altimetria = filePath("altimetria.tif", "gis"),
    localidades = filePath("Localidades_pt.shp", "gis"),
    roads = filePath("Rodovias_lin.shp", "gis"),
    setores = filePath("Setores_Censitarios_2000_pol.shp", "gis")
}
```