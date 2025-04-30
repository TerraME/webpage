# Projects

## [cells.tview](../data/cells.tview)

Automatically created TerraView project file from [cells.lua](../data/cells.lua).

|   |   |   |
|---|---|---|
|**Layer**|**File**|**Description**|
|"cells"|[cells.shp](#cells.shp)|2254 cells (polygons) with resolution 200 built from layer "farms".|

# Data

|   |   |
|---|---|
|[area.gpm](#area.gpm)|GPM file created by example area.|
|[border.gal](#border.gal)|GAL file created by example border.|
|[border.gpm](#border.gpm)|GPM file created by example border.|
|[border.gwt](#border.gwt)|GWT file created by example border.|
|[cells.shp](#cells.shp)|Automatically created file in project "cells.tview".|
|[communities.shp](#communities.shp)|A shapefile describing some communities in Santarem, Para, Brazil.|
|[farms.shp](#farms.shp)|A shapefile describing the farms.|
|[partofbrazil.shp](#partofbrazil.shp)|A shapefile describing the some Brazilian states.|
|[roads.shp](#roads.shp)|Some roads of Santarem, Para state, Brazil.|

# Directory

|   |   |
|---|---|
|[error](#error)|Some corrupted files for internal tests.|
|[test](#test)|Some files for internal tests.|

## area.gpm

GPM file created by example area.lua.

- **File:** [area.gpm](../data/area.gpm)
- **Connected files/layers:** cells.shp and farms.shp
- **Number of origins:** 2254
- **Number of connections:** 4877
- **Source:** TerraME team

## border.gal

GAL file created by example border.lua.

- **File:** [border.gal](../data/border.gal)
- **Connected file/layer:** partofbrazil.shp
- **Number of origins:** 5
- **Number of connections:** 12
- **Source:** TerraME team

## border.gpm

GPM file created by example border.lua.

- **File:** [border.gpm](../data/border.gpm)
- **Connected file/layer:** partofbrazil.shp
- **Number of origins:** 5
- **Number of connections:** 12
- **Source:** TerraME team

## border.gwt

GWT file created by example border.lua.

- **File:** [border.gwt](../data/border.gwt)
- **Connected file/layer:** partofbrazil.shp
- **Number of origins:** 5
- **Number of connections:** 12
- **Source:** TerraME team

## cells.shp

Automatically created file with 2254 cells (polygons) with resolution 200 built from layer "farms", in project [cells.tview](#cells.tview).

- **Files:** [cells.dbf](../data/cells.dbf), [cells.prj](../data/cells.prj), [cells.shp](../data/cells.shp), [cells.shx](../data/cells.shx)
- **Representation:** polygon
- **Quantity:** 2254
- **Projection:** ['WGS 84', with EPSG: 4326 (PROJ4: '+proj=longlat +datum=WGS84 +no_defs ')](https://epsg.io/4326)

|Attribute|Type|Description|
|---|---|---|
|col|number|Cell's column.|
|id|string|Unique identifier (internal value).|
|row|number|Cell's row.|

## communities.shp

A shapefile describing some communities in Santarem, Para, Brazil.

- **Files:** [communities.dbf](../data/communities.dbf), [communities.prj](../data/communities.prj), [communities.shp](../data/communities.shp), [communities.shx](../data/communities.shx)
- **Representation:** point
- **Quantity:** 4
- **Projection:** ['WGS 84', with EPSG: 4326 (PROJ4: '+proj=longlat +datum=WGS84 +no_defs ')](https://epsg.io/4326)
- **Source:** TerraME team

|Attribute|Type|Description|
|---|---|---|
|LOCALIDADE|string|Name of the community.|
|MUNICIPIO|string|Municipality the community belongs.|

## farms.shp

A shapefile describing the farms.

- **Files:** [farms.dbf](../data/farms.dbf), [farms.prj](../data/farms.prj), [farms.shp](../data/farms.shp), [farms.shx](../data/farms.shx)
- **Representation:** polygon
- **Quantity:** 343
- **Projection:** ['WGS 84', with EPSG: 4326 (PROJ4: '+proj=longlat +datum=WGS84 +no_defs ')](https://epsg.io/4326)
- **Source:** TerraME team

|Attribute|Type|Description|
|---|---|---|
|id|string|Unique identifier.|

## partofbrazil.shp

A shapefile describing the some Brazilian states.

- **Files:** [partofbrazil.dbf](../data/partofbrazil.dbf), [partofbrazil.shp](../data/partofbrazil.shp), [partofbrazil.shx](../data/partofbrazil.shx)
- **Representation:** polygon
- **Quantity:** 5
- **Projection:** Undefined, with EPSG: 0 (PROJ4: Undefined)
- **Source:** TerraME team

|Attribute|Type|Description|
|---|---|---|
|name|string|Name of the state.|

## roads.shp

Some roads of Santarem, Para state, Brazil.

- **Files:** [roads.dbf](../data/roads.dbf), [roads.prj](../data/roads.prj), [roads.shp](../data/roads.shp), [roads.shx](../data/roads.shx)
- **Representation:** line
- **Quantity:** 38
- **Projection:** ['WGS 84', with EPSG: 4326 (PROJ4: '+proj=longlat +datum=WGS84 +no_defs ')](https://epsg.io/4326)
- **Source:** TerraME team

|Attribute|Type|Description|
|---|---|---|
|STATUS|string|Status of the road: 'paved' or 'nonpaved'.|

## error

Some corrupted files for internal tests.

- **Files:** 11
- **Extensions:** dbf, prj, qix, qpj, shp, shx
- **Source:** TerraME team

## test

Some files for internal tests.

- **Files:** 109
- **Extensions:** dbf, lua, prj, qix, qpj, shp, shx, tview, xml
- **Source:** TerraME team