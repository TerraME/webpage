# Layer

A Layer representing a geospatial dataset stored in a given data source. Each Layer belongs to a [Project](./project.md). It is possible to use data stored in different data sources to create a Layer, or to create a cellular Layer from scratch. Cellular Layers homogenize the spatial representation of a given model, making the model simpler and requiring less computational resources. Layer gets different arguments, depending on the task one needs to execute. See the table below.  
  

|Task|Mandatory Arguments|Optional arguments|
|---|---|---|
|Open a Layer that already belongs to a [Project](./project.md).|name, project||
|Create a Layer using an existent file, database, or service.|name, project, [arguments related to the source]|[arguments related to the source]|
|Create a cellular Layer from scratch. It has a set of squared polygons that cover its input. It can be stored in "postgis" or "shp" sources.|input, name, project, resolution, [arguments related to the source]|box, clean, [arguments related to the source]|

### Arguments

- **box**: A boolean value indicating whether the cellular Layer will fill the box from the input layer (true) or only the minimal set of cells that cover all the input data (false, default).
- **clean**: A boolean value indicating whether the argument file should be cleaned if it needs to create the file. The default value is false.
- **encoding**: A string value to set the character encoding. Supported encodings are "utf8", "cp1250", "cp1251", "cp1252", "cp1253", "cp1254", "cp1257", and "latin1". The default value is "latin1".
- **epsg**: A number from the EPSG Geodetic Parameter Dataset describing a projection. It is a unique value used to unambiguously identify projected, unprojected, and local spatial coordinate system definitions. When the projection of the data does not have this information, it is necessary to set it manually to allow combining the Layer with other Layer to execute any algorithm. If the prj file of a given data exists but there is no EPSG number, please visit [http://www.prj2epsg.org](http://www.prj2epsg.org) to search for it. A list with the supported epsg numbers is available at [http://www.terrame.org/projections.html](http://www.terrame.org/projections.html) .
- **feature**: A string with the name of the feature to be read from a WFS.
- **file**: A string with the location of the file to be loaded or created, or a [File (base package)](../../../base/types/file.md).
- **format**: A string with the image format available in a WMS ("png", default). You can use another format if available in the WMS ("jpeg", "tiff", "geotiff", etc).
- **host**: String with the host where the database is stored. The default value is "localhost".
- **index**: A boolean value indicating whether a spatial index file must be created for a shapefile. The default value is true.
- **input**: Name of the input layer whose coverage area will be used to create a cellular layer.
- **map**: A string with the name of the map to be read from a WMS. The map will be saved in the current directory within wms subdirectory automatically created.
- **name**: A string with the layer name to be used. If the layer already exists and no additional argument is used besides project, then it opens such layer.
- **password**: A string with the password.
- **port**: Number with the port of the connection. The default value is the standard port of the DBMS. For example, MySQL uses 3306 as standard port.
- **progress**: A boolean value indicating whether progress will be shown while creating the cellular space. The default value is true.
- **project**: A file name with the TerraView project to be used, or a [Project](./project.md).
- **resolution**: A number with the x and y resolution. It will need to be measured in the same projection of the input layer.
- **service**: A string with the description of a WFS or WMS location. When the string contains wms or wfs in its content, the argument source can be avoided.
- **source**: A string with the data source. See table below with the supported data sources:

|Source|Description|Mandatory|Optional|
|---|---|---|---|
|"postgis"|PostGIS database.|password|host, port, epsg, user|
|"shp"|ESRI shapefile.|file|index, epsg|
|"wfs"|Web Feature Service (WFS).|feature, service||
|"wms"|Web Map Service (WMS).|map, service|format, user, password, port|
|"tif"|Geotiff file.|file|epsg|
|"asc"|ASC format.|file|epsg|
|"nc"|NetCDF file.|file|epsg|
|"geojson"|GeoJSON file.|file|epsg|

- **user**: String with the username. The default value is "".

### Attributes

Some attributes of Layer have internal semantics. They can be used as **read-only** by the modeler.

- **epsg**: A number with its projection identifier.

### Usage

```
import("gis")

proj = Project{
    file = "myproject.tview"
}

-- Creating a layer from a shapefile.
Layer{
    project = proj,
    file = filePath("TI_AMZ.shp", "gis"),
    name = "ti"
}

-- Creating a layer from a PostGIS database.
Layer{
    project = proj,
    name = "roads",
    user = "root",
    password = "abc123",
    table = "roads"
}

-- Opening a layer called "cells".
cl = Layer{
    project = filePath("rondonia.tview", "gis"),
    name = "cells"
}

-- Creating a cellular layer.
cl2 = Layer{
    project = proj,
    input = "amazonia-states",
    name = "cells",
    file = "cells.shp",
    resolution = 5e4 -- 50x50km
}

-- Opening a WFS.
Layer{
    project = proj,
    name = "protected",
    service = "http://terrabrasilis.info/redd-pac/wfs/wfs_biomes",
    feature = "ProtectedAreas2000",
}
```

## Functions

|   |   |
|---|---|
|[attributes](#attributes)|The attribute names of the Layer.|
|[bands](#bands)|Return the number of bands of a raster layer.|
|[box](#box)|Returns the bounding box as a table with the keys xMin, yMin, xMax and yMax.|
|[check](#check)|Checks if data layer geometries are valid.|
|[delete](#delete)|Delete the data source of the Layer.|
|[drop](#drop)|Drop the database of the Layer.|
|[dummy](#dummy)|Returns the dummy value of a raster layer.|
|[export](#export)|Exports the data of a Layer to another data source.|
|[fill](#fill)|Create a new attribute for each object of a Layer.|
|[merge](#merge)|Merges every temporal layer from the layer's project into a single layer with all temporal attribute.|
|[polygonize](#polygonize)|Creates a vector data from a raster layer using polygons covering contiguous pixels that share the same value.|
|[projection](#projection)|Return the Layer's projection.|
|[representation](#representation)|Return a string with the representation of the layer.|
|[simplify](#simplify)|Create a new data simplifying its geometry.|
|[split](#split)|Splits a temporal layer into multiple layers.|
|[#](##)|Return the number of objects (points, polygons, lines, or pixels) within the Layer.|

## **attributes** 

The attribute names of the Layer. It returns a vector of strings, whose size is the number of attributes.  
  

### Usage

```
import("gis")

print(vardump(layer:attributes()))
```

## **bands** 

Return the number of bands of a raster layer. If the layer does not have a raster representation then it will stop with an error. The bands of the raster layer are named from zero to the number of bands minus one.  
  

### Usage

```
print(layer:bands())
```

## **box** 

Returns the bounding box as a table with the keys xMin, yMin, xMax and yMax.  
  

### Usage

```
bbox = alayer:box()
print(bbox.xMin, bbox.yMin, bbox.xMax, bbox.yMax)
```

## **check** 

Checks if data layer geometries are valid. If some invalid geometry are found, a warning is show about the problem. Return true if no problem is found.  
  

### Arguments

- **#1**: A boolean value which if true tries to fix the geometry problems found. If not set, its value will be false. If it is not possible fix the geometries an error will be shown.
- **#2**: A boolean value indicating whether progress will be shown while fixing the geometries.

### Usage

```
local layer = Layer{
    project = proj,
    name = "DefectBio",
    file = "biomassa.shp"
}

if not layer:check() then
    layer:check(true)
end
```

## **delete** 

Delete the data source of the Layer. If it is a file or a set of files, remove them. If it is a database table, remove it.  
  

### Usage

```
layer:delete()
```

## **drop** 

Drop the database of the Layer. This function only works when the layer is stored in a PostGIS table. Note that it removes all tables within the database.  
  

### Usage

```
layer:drop()
```

## **dummy** 

Returns the dummy value of a raster layer. If the layer does not have a raster representation then it returns nil . The bands of the raster layer are named from zero to the number of bands minus one. If the band is greater than that, it returns an error.  
  

### Arguments

- **#1**: The band number. The default value is zero.

### Usage

```
print(layer:dummy())
```

## **export** 

Exports the data of a Layer to another data source. The data can be either a file data or postgis. The SRID and overwrite are common arguments.  
  

### Arguments

- **epsg**: A number from the EPSG Geodetic Parameter Dataset describing a projection. It can be used to reproject the data. A list with the supported epsg numbers is available at [http://www.terrame.org/projections.html](http://www.terrame.org/projections.html) .
- **overwrite**: Indicates if the exported data will be overwritten, the default is false.
- **progress**: A boolean value indicating whether progress will be shown while exporting the layer. The default value is true.
- **select**: A vector with the names of the attributes to be saved. When saving a single attribute, you can use a string "attribute" instead of a table {"attribute"}.
- **...**: Additional arguments related to where the output will be saved. These arguments are the same for describing the data source when one creates a layer from a file or database.

### Usage

```
layer:export{file = "myfile.shp"}
layer:export{file = "myfile.geojson"}
layer:export{file = "myfile.geojson", epsg = 4326}
layer:export{file = "myfile.geojson", epsg = 4326, select = {"uf", "population"}}
```

## **fill** 

Create a new attribute for each object of a Layer. This attribute can be stored as a new column of a table or a new file, according to where the Layer is stored. There are several strategies for filling cells according to the geometry of the input layer.  
  

### Arguments

- **area**: Whether the calculation will be based on the intersection area (true), or the weights are equal for each object with some overlap (false, missing value).
- **attribute**: The name of the new attribute to be created.
- **band**: An integer value representing the band of the raster to be used. The default value is one.
- **dummy**: A number related to the input raster data that represents no information in a pixel value. This value will be ignored by all operations as if it did not exist. For example, in averages, dummy values will not be used in the sum nor to count the number of pixels. Its default value is the result of [Layer:dummy()](../files/Layer.html#dummy).
- **layer**: An input Layer belonging to the same [Project](../files/Project.html). It can also be a string with the Layer's name. There are several strategies available, depending on the geometry of the Layer. See below:

|Geometry|Using only geometry|Using attribute of objects with some overlap|Using geometry and attribute|
|---|---|---|---|
|Points|"count", "distance", "presence"|"average", "mode", "maximum", "minimum", "stdev", "sum", "median"|(none)|
|Lines|"count", "distance", "presence"|"average", "mode", "maximum", "minimum", "stdev", "sum", "median"|(none)|
|Polygons|"area", "count", "distance", "presence"|"average", "mode", "maximum", "minimum", "stdev", "sum", "median"|"average", "mode", "coverage", "sum"|
|Raster|(none)|"average", "mode", "maximum", "minimum", "coverage", "stdev", "sum", "count", "median"|(none)|

- **missing**: A value that will be used to fill a cell whose attribute cannot be computed (for example, when there is no intersection area). Note that this argument is related to the output. Its default value is zero.
- **operation**: The way to compute the attribute of each cell. When using raster data, a pixel is considered within a given geometry if there is some intersection between the pixel and the geometry. This means that the same pixel might belong to two or more geometries of the layer. See the table below with the available operations:

|Operation|Description|Mandatory arguments|Optional arguments|
|---|---|---|---|
|"area"|Percentage of area with some overlay with a layer of polygons. The created values will range from zero (no intersection) to one (area fully covered by polygons). This algorithm supposes that there is no intersection area between each pair of polygons from the reference layer. It sums the intersection areas of the object with all the polygons of the reference layer. Because of that, if there is some overlay between the polygons of the reference layer, it might create attribute values greater than one.|attribute, layer|progress, split|
|"average"|Average of quantitative values from the objects that have some intersection with the cell, without taking into account their geometric properties. When using argument area, it computes the average weighted by the proportions of the respective intersection areas. Useful to distribute atributes that represent averages, such as per capita income.|attribute, layer, select|area, band, dummy, missing, pixel, progress, split|
|"count"|Number of objects that have some overlay with the cell.|attribute, layer|dummy, pixel, progress, split|
|"coverage"|Percentage or total area of each qualitative value covering the cell, using polygons or raster data. It creates one new attribute for each available value, in the form attribute.."_"..value, where attribute is the value passed as argument to fill and value represent the different values in the input data. The sum of the created attribute values for a given cell will range from zero to one indicating the percentage of the cell covered by pixels of each class (default), or the total area covered by each class, according to the area of a pixel in the raster data (when using area = true). Note that this operation does not use dummy value, therefore one attribute will also be created for the dummy values. When using shapefiles, keep in mind the total limit of ten characters, as it removes the characters after the tenth in the name. This function will stop with an error if two attribute names in the output are the same.|attribute, layer, select|area, band, missing, pixel, progress, split|
|"distance"|Distance to the nearest object. The distance is computed from the centroid of the cell to the closest point, line, or border of a polygon.|attribute, layer|progress, split|
|"maximum"|Maximum quantitative value among the objects that have some intersection with the cell, without taking into account their geometric properties.|attribute, layer, select|band, dummy, missing, pixel, progress, split|
|"minimum"|Minimum quantitative value among the objects that have some intersection with the cell, without taking into account their geometric properties.|attribute, layer, select|band, dummy, missing, pixel, progress, split|
|"mode"|More common qualitative value from the objects that have some intersection with the cell, without taking into account their geometric properties. This operation creates an attribute with string values. Whenever there are two or more values with the same count, the resulting value will contain all them separated by comma. When using argument area, it uses the value of the object that has larger coverage.|attribute, layer, select|band, dummy, missing, pixel, progress, split|
|"presence"|Boolean value pointing out whether some object has an overlay with the cell.|attribute, layer|progress, split|
|"stdev"|Standard deviation of quantitative values from objects that have some intersection with the cell, without taking into account their geometric properties.|attribute, layer, select|band, dummy, missing, pixel, progress, split|
|"sum"|Sum of quantitative values from objects that have some intersection with the cell, without taking into account their geometric properties. When using argument area, it computes the sum based on the proportions of intersection area. Useful to preserve the total sum in both layers, such as population size.|attribute, layer, select|area, band, dummy, missing, pixel, progress, split|
|"median"|Median is the midpoint of a frequency distribution of observed values.|attribute, layer, select|band, dummy, missing, pixel, progress, split|

- **pixel**: A string value indicating when a pixel is within a polygon. See the table below.

|Pixel|Description|
|---|---|
|"centroid" (default)|A pixel is within a polygon if its centroid is within the polygon. It is recommended to use this strategy when one wants to keep the sum of the amount of pixels in the created output, and when the resolution of the polygons is greater than the resolution of the pixels. If the resolution of polygons is smaller than the resolution of pixels, there might exist polygons that do not contain any pixel. For cellular representations, when the cells were created using the raster and the resolution of polygons is considerably smaller than the resolution of pixels, a pixel might belong to two polygons as its centroid might be located in the limit of both polygons.|
|"overlap"|A pixel is considered within a polygon if they have some overlap. This way, a pixel might belong to two or more polygons at the same time. This strategy is usually recommended when the resolution of the polygons is smaller than the resolution of the pixels. This strategy takes more time to run.|

- **progress**: A boolean value indicating whether progress will be shown while computing the operation. The default value is true.
- **select**: Name of an attribute from the input data. It is only required when the selected operation needs a value associated to the geometry (average, sum, mode). When using a raster data as input, use argument band instead.
- **split**: A boolean to determine if the fill will split the temporal data into different layers with each new layer's name formed by the own Layer's name and the respective times as sufix. The default value is false and, in this case, the temporal data will be filled in the own Layer into different attributes though.

### Usage

```
import("gis")

cl = Layer{
    project = file("rondonia.tview"),
    layer = "cells"
}

cl:fill{
    attribute = "distRoads",
    operation = "distance",
    layer = "roads"
}

cl:fill{
    attribute = "population",
    layer = "population",
    operation = "sum",
    area = true
}

cl:fill{
    attribute = "area2010_",
    operation = "coverage",
    layer = "cover",
    select = "cover2010"
}

cl:fill{
    attribute = "area",
    operation = "coverage",
    layer = "cover*", -- temporal representation
}
```

## **merge** 

Merges every temporal layer from the layer's project into a single layer with all temporal attribute. Atributes from temporal layers are created with the attribute name followed by the time from its layer. Every temporal layer must have the same geometry.  
  

### Usage

```
layer:merge()
```

## **polygonize** 

Creates a vector data from a raster layer using polygons covering contiguous pixels that share the same value. The output data can be either a file data or postgis.  
  

### Arguments

- **band**: The band number (0, default). The output data created will have an attribute named 'value' with the value of the pixel according to the band selected.
- **overwrite**: Optional argument that indicates if the output data will be overwritten, the default is false.
- **...**: Additional arguments related to where the output will be saved. These arguments are the same for describing the data source when one creates a layer from a file or database.

### Usage

```
layer:polygonize{file = "polygonized.shp", overwrite = true}
layer:polygonize{
	source = "postgis",
	password = "postgres",
	database = "postgis_22_sample",
	table = "polygonized",
	overwrite = true
}
```

## **projection** 

Return the Layer's projection. It contains the name of the projection, its Geodetic Identifier (EPSG), and its Proj4 description ([www.proj4.org/parameters.html](www.proj4.org/parameters.html)).  
  

### Usage

```
print(layer:projection())
```

## **representation** 

Return a string with the representation of the layer. It can be "point", "polygon", "line", or "raster".  
  

### Usage

```
print(layer:representation())
```

## **simplify** 

Create a new data simplifying its geometry. The data will be created using the same data source layer. This function uses Douclas-Peucker algorithm and currently works only for line data.  
  

### Arguments

- **output**: The data name that will be created.
- **tolerance**: The maximum distance between the original curve and the simplified curve. A given point is removed when the distances in a curve without it is less than the maximum distance. The tolerance uses the same unit of the input geometry's projection.

### Usage

```
layer:simplify{output = "layer_simplified", tolerance = 500}
```

## **split** 

Splits a temporal layer into multiple layers. It creates a 'layer_time' for each time available as attribute values 'attribute_time'.  
  

### Usage

```
layer:split()
```

## **#** 

Return the number of objects (points, polygons, lines, or pixels) within the Layer.  
  

### Usage

```
print(#layer)
```