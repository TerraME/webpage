# TerraLib

Type to access TerraLib. It contains very basic and low level functions that are used by the other types of the package. If needed, these functions should be used with care. Such functions mught stop with very strange errors because they do not check any errors in their arguments. All functions must be called by '.'.  
  

### Usage

```
TerraLib().getVersion()
```

## Functions

|   |   |
|---|---|
|[addGdalLayer](#addGdalLayer)|Add a new GDAL layer to a given project.|
|[addGeoJSONCellSpaceLayer](#addGeoJSONCellSpaceLayer)|Create a new cellular layer into a shapefile.|
|[addGeoJSONLayer](#addGeoJSONLayer)|Add a GeoJSON layer to a given project.|
|[addPgCellSpaceLayer](#addPgCellSpaceLayer)|Add a new cellular layer to a PostgreSQL connection.|
|[addPgLayer](#addPgLayer)|Add a new PostgreSQL layer to a given project.|
|[addShpCellSpaceLayer](#addShpCellSpaceLayer)|Create a new cellular layer into a shapefile.|
|[addShpLayer](#addShpLayer)|Add a shapefile layer to a given project.|
|[addWfsLayer](#addWfsLayer)|Add a WFS layer to a given project.|
|[addWmsLayer](#addWmsLayer)|Add a WMS layer to a given project.|
|[attributeFill](#attributeFill)|Fill a given attribute in a layer.|
|[castGeomToSubtype](#castGeomToSubtype)|Returns a subtype of Geometry object.|
|[checkLayerGeometries](#checkLayerGeometries)|Checks if data layer geometries are valid.|
|[checkName](#checkName)|Check if a name is valid.|
|[createProject](#createProject)|Create a new [Project](../types/project.md).|
|[douglasPeucker](#douglasPeucker)|Create a new dataset applying Douglas Peucker algorithm.|
|[dropPgDatabase](#dropPgDatabase)|Remove a PostreSQL database.|
|[dropPgTable](#dropPgTable)|Remove a PostreSQL table.|
|[geometry](#geometry)|Return a handle to TerraLib Geometry Objects.|
|[getArea](#getArea)|Returns the area of this envelope as measured in the spatial reference system of it.|
|[getBoundingBox](#getBoundingBox)|Return the bounding box of a [Layer](../types/layer.md).|
|[getDataSet](#getDataSet)|Returns a given dataset from a layer.|
|[getDataSetSize](#getDataSetSize)|Return the size of a dataset.|
|[getDistance](#getDistance)|Returns the shortest distance between any two points in the two geometries.|
|[getDummyValue](#getDummyValue)|Returns the dummy value of a raster data.|
|[getGeometryInfo](#getGeometryInfo)|Get information about the geometry attribute.|
|[getLayerInfo](#getLayerInfo)|Return the information of a given layer.|
|[getLayerSize](#getLayerSize)|Returns the size of a layer.|
|[getNumOfBands](#getNumOfBands)|Returns the number of bands of some Raster.|
|[getProjection](#getProjection)|Returns a coordinate system name given an identification.|
|[getPropertyInfos](#getPropertyInfos)|Returns the property informations of a layer.|
|[getPropertyNames](#getPropertyNames)|Returns the property names of the dataset.|
|[getRasterInfo](#getRasterInfo)|Return the information of a raster.|
|[getVersion](#getVersion)|Return the current TerraLib version.|
|[isValidWfsUrl](#isValidWfsUrl)|Validates if the URL is a valid WFS server.|
|[openProject](#openProject)|Open a new project.|
|[polygonize](#polygonize)|Creates a polygonized data using GDALPolygonize().|
|[random](#random)|Return pseudo-random number generations exported from Boost.|
|[removeLayer](#removeLayer)|Remove a given layer from a given project.|
|[saveDataAs](#saveDataAs)|Save some data of a layer to another data type.|
|[saveDataSet](#saveDataSet)|Save a given dataset.|
|[saveRasterFromTable](#saveRasterFromTable)|Save a raster on file.|
|[setProgressVisible](#setProgressVisible)|Set progress viewer.|

## **addGdalLayer** 

Add a new GDAL layer to a given project.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The file to the layer.
- **#4**: A number value that represents the Spatial Reference System Identifier.

### Usage

```
proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

layerName = "TifLayer"
layerFile = filePath("cbers_rgb342_crop1.tif", "gis")
TerraLib().addGdalLayer(proj, layerName, layerFile)
```

## **addGeoJSONCellSpaceLayer** 

Create a new cellular layer into a shapefile.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The name of the layer.
- **#4**: The size of a cell.
- **#5**: The file to the cellular layer.
- **#6**: A boolean value indicating whether the cells should cover only the input data (true) or its bounding box (false).

### Usage

```
proj = {
    file = "mygeojsonproject.tview",
    title = "TerraLib Tests",
    author = "Carneiro Heitor"
}

TerraLib().createProject(proj, {})

layerName1 = "Setores_Layer"
layerFile1 = filePath("Setores_Censitarios_2000_pol.geojson", "gis")
TerraLib().addGeoJSONLayer(proj, layerName1, layerFile1)

TerraLib().addGeoJSONCellSpaceLayer(proj, layerName1, "Setores_Cells", 10000, currentDir())
```

## **addGeoJSONLayer** 

Add a GeoJSON layer to a given project.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The file to the layer.
- **#4**: A number value that represents the Spatial Reference System Identifier.
- **#5**: A string value used to set the character encoding.

### Usage

```
tl = TerraLib()
TerraLib().createProject("project.tview", {})
TerraLib().addGeoJSONLayer(proj, "GeoJSONLayer", filePath("Setores_Censitarios_2000_pol.geojson", "gis"))
```

## **addPgCellSpaceLayer** 

Add a new cellular layer to a PostgreSQL connection.  
  

### Arguments

- **#1**: The name of the project.
- **#2**: Name of the input layer.
- **#3**: The name of the layer.
- **#4**: The size of a cell.
- **#5**: The connection data, such as host, port, and user.
- **#6**: A boolean value indicating whether the cells should cover only the input data (true) or its bounding box (false).

### Usage

```
local proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

local layerName1 = "SampaShp"
local layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

local pgData = {
    type = "POSTGIS",
    host = "localhost",
    port = "5432",
    user = "postgres",
    password = "postgres",
    database = "terralib_save_test",
    table = "sampa_cells"
}

local clName1 = "SampaPgCells"
local resolution = 0.7
TerraLib().addPgCellSpaceLayer(proj, layerName1, clName1, resolution, pgData)
```

## **addPgLayer** 

Add a new PostgreSQL layer to a given project.  
  

### Arguments

- **database**: The database name.
- **encoding**: A string value used to set the character encoding.
- **host**: Name of the host.
- **name**: The name of the layer.
- **password**: The password.
- **port**: Port number.
- **project**: A table that represents a project.
- **srid**: A number value that represents the Spatial Reference System Identifier.
- **user**: The user name.

### Usage

```

proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

local layerName1 = "SampaShp"
local layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

pgData = {
    type = "POSTGIS",
    host = "localhost",
    port = "5432",
    user = "postgres",
    password = "postgres",
    database = "terralib_save_test",
    table = "sampa_cells",
}

TerraLib().addPgLayer(proj, "SampaPg", pgData)
```

## **addShpCellSpaceLayer** 

Create a new cellular layer into a shapefile.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The name of the layer.
- **#4**: The size of a cell.
- **#5**: The file to the layer.
- **#6**: A boolean value indicating whether the cells should cover only the input data (true) or its bounding box (false).
- **#7**: A boolean value indicating whether a spatial index file should be created.

### Usage

```
proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

layerName1 = "SampaShp"
layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

TerraLib().addShpCellSpaceLayer(proj, layerName1, "Sampa_Cells", 0.7, currentDir())
```

## **addShpLayer** 

Add a shapefile layer to a given project.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The file to the layer.
- **#4**: A boolean value indicating whether a spatial index file should be created.
- **#5**: A number value that represents the Spatial Reference System Identifier.
- **#6**: A string value used to set the character encoding.

### Usage

```
tl = TerraLib()
proj = TerraLib().createProject("project.tview", {})
TerraLib().addShpLayer(proj, "ShapeLayer", filePath("sampa.shp", "gis"))
```

## **addWfsLayer** 

Add a WFS layer to a given project.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: The URL of the WFS server.
- **#4**: The data set in WFS server.
- **#5**: A number value that represents the Spatial Reference System Identifier.
- **#6**: A string value used to set the character encoding.

### Usage

```
local layerName = "WFS-Layer"
local url = "http://terrabrasilis.info/redd-pac/wfs/wfs_biomes"
local dataset = "reddpac:BAU"
TerraLib().addWfsLayer(project, name, url, dataset)
```

## **addWmsLayer** 

Add a WMS layer to a given project.  
  

### Arguments

- **#1**: A table that represents a project.
- **#2**: The name of the layer.
- **#3**: A table with the WMS connection parameters.
- **#4**: The data set in WMS server.
- **#5**: A number value that represents the Spatial Reference System Identifier.

### Usage

```
local layerName = "WMS-Layer"
local url = "http://terrabrasilis.info/terraamazon/ows"
local dataset = "IMG_02082016_321077D"
local directory = currentDir()
local conn = {
url = url,
directory = directory,
format = "jpeg"
}
TerraLib().addWmsLayer(project, layerName, conn, dataset)
```

## **attributeFill** 

Fill a given attribute in a layer.  
  

### Arguments

- **area**: A boolean value indicating whether the area should be considered.
- **attribute**: Name of the attribute to be created.
- **default**: The default value.
- **from**: Name of the input layer with the data where the operations will take place.
- **nodata**: A number used in raster data that represents no information in a pixel value.
- **operation**: Name of the operation.
- **out**: Name of the layer to be created with the output.
- **pixel**: A boolean value. If true, a pixel is considered within a polygon if they have some overlap. If false, a pixel is within a polygon if its centroid is within the polygon.
- **project**: The name of the project.
- **repr**: A string with the spatial representation of data ("raster", "polygon", "point", or "line").
- **select**: The attribute to be used in the operation.
- **to**: Name of the reference layer with the elements to be copied to the output.

### Usage

```
proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

layerName1 = "Para"
layerFile1 = filePath("limitePA_polyc_pol.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

resolution = 60e3
TerraLib().addShpCellSpaceLayer(proj, layerName1, clName, resolution, filePath1)

clSet = TerraLib().getDataSet{project = proj, layer = clName}

layerName2 = "Protection_Unit"
layerFile2 = filePath("BCIM_Unidade_Protecao_IntegralPolygon_PA_polyc_pol.shp", "gis")
TerraLib().addShpLayer(proj, layerName2, layerFile2)

TerraLib().attributeFill{
    project = proj,
    from = layerName2,
   to = clName,
   out = presLayerName,
   attribute = "presence",
   operation = "presence",
   select = "FID"
}
```

## **castGeomToSubtype** 

Returns a subtype of Geometry object.  
  

### Arguments

- **#1**: A Geometry object.

### Usage

```
shpPath = filePath("RODOVIAS_AMZ_lin.shp", "gis")
dSet = TerraLib().getDataSet{file = shpPath}
geom = dSet[1].OGR_GEOMETRY
geom = TerraLib().castGeomToSubtype(geom)
```

## **checkLayerGeometries** 

Checks if data layer geometries are valid. If invalid geometries are found, it returns a list of the problems.  
  

### Arguments

- **#1**: A project.
- **#2**: The name of the layer.
- **#3**: A boolean value which if true tries to fix the geometry problems founded.

### Usage

```
local problems = TerraLib().checkLayerGeometries(self.project, self.name)
print(problems[1].error, problems[1].coord.x, problems[1].coord.y)
```

## **checkName** 

Check if a name is valid. Return an error message if the name is invalid, otherwise it returns a empty string.  
  

### Arguments

- **#1**: A string name.

### Usage

```
TerraLib().checkName("aname")
```

## **createProject** 

Create a new [Project](../types/project.md).  
  

### Arguments

- **#1**: The name of the project.
- **#2**: A table where the layers will be stored.

### Usage

```
import("gis")

proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})
```

## **douglasPeucker** 

Create a new dataset applying Douglas Peucker algorithm.  
  

### Arguments

- **#1**: The project.
- **#2**: The layer name used as reference to create a new dataset.
- **#3**: The new dataset name.
- **#4**: The tolerance is a distance that defines the threshold for vertices to be considered "insignificant" for the general structure of the geometry. The tolerance must be expressed in the same units as the projection of the input geometry.

### Usage

```
lnName = "ES_Rails"
lnFile = filePath("test/rails.shp", "gis")
TerraLib().addShpLayer(proj, lnName, lnFile)
TerraLib().douglasPeucker(proj, lnName, "spl"..lnName, 500)
```

## **dropPgDatabase** 

Remove a PostreSQL database.  
  

### Arguments

- **database**: The database name.
- **host**: Name of the host.
- **password**: The password.
- **port**: Port number.
- **user**: The user name.

### Usage

```

proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

local layerName1 = "SampaShp"
local layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

pgData = {
    type = "POSTGIS",
    host = "localhost",
    port = "5432",
    user = "postgres",
    password = "postgres",
    database = "terralib_save_test",
    table = "sampa_cells",
    encoding = "CP1252"
}

TerraLib().addPgLayer(proj, "SampaPg", pgData)

TerraLib().dropPgDatabase(pgData)
```

## **dropPgTable** 

Remove a PostreSQL table.  
  

### Arguments

- **database**: The database name.
- **encoding**: The encoding of the table.
- **host**: Name of the host.
- **password**: The password.
- **port**: Port number.
- **user**: The user name.

### Usage

```

proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

local layerName1 = "SampaShp"
local layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

pgData = {
    type = "POSTGIS",
    host = "localhost",
    port = "5432",
    user = "postgres",
    password = "postgres",
    database = "terralib_save_test",
    table = "sampa_cells",
    encoding = "CP1252"
}

TerraLib().addPgLayer(proj, "SampaPg", pgData)

TerraLib().dropPgTable(pgData)
```

## **geometry** 

Return a handle to TerraLib Geometry Objects.  
  

### Usage

```
TerraLib().geometry().Point(0, 0)
```

## **getArea** 

Returns the area of this envelope as measured in the spatial reference system of it.  
  

### Arguments

- **#1**: The geometry of the project.

### Usage

```
local dSet = TerraLib().getDataSet{project = proj, layer = clName1}
local area = TerraLib().getArea(dSet[0].OGR_GEOMETRY)
```

## **getBoundingBox** 

Return the bounding box of a [Layer](../types/layer.md).  
  

### Arguments

- **#1**: A Layer.

### Usage

```
TerraLib().getBoundingBox(proj.layers["layerName"])
```

## **getDataSet** 

Returns a given dataset from a layer.  
  

### Arguments

- **file**: A file path.
- **layer**: A layer name.
- **missing**: A value to replace null values.
- **project**: A project.

### Usage

```
dset = TerraLib().getDataSet{project = "myproject.tview", layer = "mylayer"}
```

## **getDataSetSize** 

Return the size of a dataset.  
  

### Arguments

- **#1**: A file.

### Usage

```
tifFile = filePath("prodes_polyc_10k.tif", "gis")
tifSize = TerraLib().getDataSetSize(tifFile)
```

## **getDistance** 

Returns the shortest distance between any two points in the two geometries.  
  

### Arguments

- **#1**: The geometry.
- **#2**: The other geometry.

### Usage

```
local dSet = TerraLib().getDataSet{project = proj, layer = clName1}
local dist = TerraLib().getDistance(dSet[0].OGR_GEOMETRY, dSet[getn(dSet) - 1].OGR_GEOMETRY)
```

## **getDummyValue** 

Returns the dummy value of a raster data.  
  

### Arguments

- **#1**: The project.
- **#2**: The layer name which is in the project.
- **#3**: The band number.

### Usage

```
local layerName = "TifLayer"
local layerFile = filePath("cbers_rgb342_crop1.tif", "gis")
TerraLib().addGdalLayer(proj, layerName, layerFile)
local dummy = TerraLib().getDummyValue(proj, layerName, 0)
```

## **getGeometryInfo** 

Get information about the geometry attribute.  
  

### Arguments

- **file**: A file. If a project is set, file is ignored.
- **layer**: Name of a layer.
- **project**: A project.

### Usage

```

local shpFile = filePath("amazonia-roads.shp", "gis")
local geomInfo = TerraLib().getGeometryInfo{file = shpFile}
print(geomInfo.fid, geomInfo.name, geomInfo.geometry)
```

## **getLayerInfo** 

Return the information of a given layer.  
  

### Arguments

- **#1**: The name of the project.
- **#2**: The name of a layer.

### Usage

```
proj = {
    file = "myproject.tview",
    title = "TerraLib Tests",
    author = "Avancini Rodrigo"
}

TerraLib().createProject(proj, {})

local layerName1 = "SampaShp"
local layerFile1 = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName1, layerFile1)

pgData = {
    type = "POSTGIS",
    host = "localhost",
    port = "5432",
    user = "postgres",
    password = "postgres",
    database = "terralib_save_test",
    table = "sampa_cells"
}

TerraLib().addPgLayer(proj, "SampaPg", pgData)

layerInfo = TerraLib().getLayerInfo(proj, "SampaPg")
```

## **getLayerSize** 

Returns the size of a layer. When it stores vector data, it returns the number of elements. If it stores raster data, return the number of pixels.  
  

### Arguments

- **#1**: The project.
- **#2**: The layer name which is in the project.

### Usage

```
local layerName = "SampaShp"
local layerFile = filePath("sampa.shp", "gis")
TerraLib().addShpLayer(proj, layerName, layerFile)
local size = TerraLib().getLayerSize(proj, layerName)
```

## **getNumOfBands** 

Returns the number of bands of some Raster.  
  

### Arguments

- **#1**: The project.
- **#2**: The input layer name.

### Usage

```
TerraLib().addGdalLayer(proj, layerName, layerFile)
local numBands = TerraLib().getNumOfBands(proj, layerName)
```

## **getProjection** 

Returns a coordinate system name given an identification.  
  

### Arguments

- **#1**: A layer.

### Usage

```
local prj = TerraLib().getProjection(proj.layers[layerName])
print(prj.NAME..". SRID: "..prj.SRID..". PROJ4: "..prj.PROJ4)
```

## **getPropertyInfos** 

Returns the property informations of a layer.  
  

### Arguments

- **#1**: A [Project](./project.md).
- **#2**: A [Layer](./layer.md) name.

### Usage

```
local propInfos = TerraLib().getPropertyInfos(proj, "layerName")
unitTest:assertEquals(propInfos[1].name, "ID")
unitTest:assertEquals(propInfos[1].type, "integer 64")
unitTest:assertEquals(propInfos[2].name, "NM_MICRO")
unitTest:assertEquals(propInfos[2].type, "string")
```

## **getPropertyNames** 

Returns the property names of the dataset.  
  

### Arguments

- **#1**: A [Project](./project.md).
- **#2**: A [Layer](./layer.md) name.

### Usage

```
local propNames = TerraLib().getPropertyNames(proj, proj.layers[layerName])
for i = 0, #propNames do
	unitTest:assert((propNames[i] == "FID") or (propNames[i] == "ID") or
					(propNames[i] == "NM_MICRO") or (propNames[i] == "CD_GEOCODU"))
end
```

## **getRasterInfo** 

Return the information of a raster.  
  

### Arguments

- **#1**: A raster file.

### Usage

```
tifFile = filePath("prodes_polyc_10k.tif", "gis")
tifInfo = info = gis.TerraLib().getRasterInfo(file)
```

## **getVersion** 

Return the current TerraLib version.  
  

### Usage

```
import("gis")
print(TerraLib().getVersion())
```

## **isValidWfsUrl** 

Validates if the URL is a valid WFS server.  
  

### Arguments

- **#1**: The URL of the WFS server.

### Usage

```
local layerName = "WFS-Layer"
local url = "http://terrabrasilis.info/redd-pac/wfs/wfs_biomes"
local dataset = "reddpac:BAU"
TerraLib().isValidWfsUrl(url)
```

## **openProject** 

Open a new project.  
  

### Arguments

- **#1**: The name of the project.
- **#2**: The path for the project.

### Usage

```
import("gis")
proj = {}
TerraLib().openProject(proj2, "myproject.tview")
```

## **polygonize** 

Creates a polygonized data using GDALPolygonize().  
  

### Arguments

- **band**: The band which will be created the values.
- **layer**: The layer name.
- **outInfo**: A table with output information according to data source with the same arguments when creates a layer from a file or database.
- **project**: The project which contains the layer.

### Usage

```
local rasterInfo = {
	project = aProject,
	layer = aLayerName,
	band = 0,
}

local outInfo = {
	source = "postgis",
	host = "localhost",
	port = "5432",
	user = "postgres",
	password = "postgres",
	database = "postgis_22_sample",
	table = "aTableName",
	encoding = "LATIN1"
}

TerraLib().polygonize(rasterInfo, outInfo)
```

## **random** 

Return pseudo-random number generations exported from Boost.  
  

### Usage

```
mt = TerraLib().random().MersenneTwister(1)
nd = TerraLib().random().NormalDistribution(mt, 1, 6)
print(nd())
```

## **removeLayer** 

Remove a given layer from a given project.  
  

### Arguments

- **#1**: The name of the project.
- **#2**: The name of the layer to be removed.

### Usage

```
removeLayer(project, layerName)
```

## **saveDataAs** 

Save some data of a layer to another data type.  
  

### Arguments

- **#1**: The reference information data.
- **#2**: The data that will be saved.
- **#3**: Indicates if the saved data will be overwritten.
- **#4**: The attribute(s) that will be saved.
- **#5**: A table with a data's subset of the [Layer](./layer.md). If this parameter is set with a subset of from data, the saved data will have only its values. And, if values is set and attrs is nil, all attributes will be saved.

### Usage

```
local fromData = {
    project = aProject,
    layer = "aLayerName"
}
local toData = {
    file = "shp2geojson.geojson",
    type = "geojson",
    srid = 4326
}
TerraLib().saveDataAs(fromData, toData, true, {"population", "ages"})
```

## **saveDataSet** 

Save a given dataset.  
  

### Arguments

- **#1**: The name of the project.
- **#2**: The input layer name.
- **#3**: A table mapping the names of the attributes from the input to the output.
- **#4**: The output layer name.
- **#5**: A table with the attributes to be saved.
- **#6**: The name of the output data set.

### Usage

```
saveDataSet(project, fromLayerName, toSet, toName, attrs)
```

## **saveRasterFromTable** 

Save a raster on file.  
  

### Arguments

- **#1**: A table built from raster dataset.
- **#2**: The raster file that was used for build the raster table.
- **#3**: A file to save the raster.
- **#4**: A attribute from the table that its values will be saved on raster band 0.

### Usage

```
tifFile = filePath("prodes_polyc_10k.tif", "gis")
local outFile = File("newraster.tif"):deleteIfExists()
TerraLib().saveRasterFromTable(cs.cells, tifFile, outFile, "b0")
```

## **setProgressVisible** 

Set progress viewer.  
  

### Arguments

- **#1**: A boolean that if true show the percetage progress of some functions.

### Usage

```
TerraLib().setProgressVisible(true)
TerraLib().attributeFill(...)
```