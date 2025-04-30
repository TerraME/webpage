# Generalized Proximity Matrix

  
**Version:** 0.7  
**License:** LGPL-3  
**Release:** 04/16/2018  
**Authors:** Pedro R. Andrade, Rodrigo Avancini  
**URL:** [https://github.com/pedro-andrade-inpe/gpm](https://github.com/pedro-andrade-inpe/gpm)  
  

A package to create neighborhood relations or fill attributes using the idea of GPM.  

## Types

|Type|Description|
|---|---|
|[GPM](./types/gpm.md)|Type to create a Generalized Proximity Matrix ([GPM](./types/gpm.md)).|
|[Network](./types/network.md)|Type that represents a network.|

## [Examples](./types/examples.md)

su|Example|Description|
|---|---|
|[**area**](./types/examples.md#area)|[GPM](./types/gpm.md) Implementation strategy 'area' and creating map.|
|[**border**](./types/examples.md#border)|Compute the neighbors of some Brazilian states.|
|[**contains**](./types/examples.md#contains)|Example that connects cells to the communities located within them.|
|[**distance-all**](./types/examples.md#distance-all)|Computes neighborhoods based on Euclidean distances from cells to all communities.|
|[**distance-limit**](./types/examples.md#distance-limit)|Computes neighborhoods based on Euclidean distances from cells to communities within 4km of distance.|
|[**length**](./types/examples.md#length)|Compute a [GPM](./types/gpm.md) based on the intersection between cells and lines.|
|[**network**](./types/examples.md#network)|[GPM](./types/gpm.md) Implementation creating maps.|

## [Data](./types/data.md)

|Data|Description|
|---|---|
|[**area.gpm**](./types/data.md#area.gpm)|GPM file created by example area.|
|[**border.gal**](./types/data.md#border.gal)|GAL file created by example border.|
|[**border.gpm**](./types/data.md#border.gpm)|GPM file created by example border.|
|[**border.gwt**](./types/data.md#border.gwt)|GWT file created by example border.|
|[**cells.dbf**](./types/data.md#cells.dbf)|Automatically created file in project "cells.tview".|
|[**cells.tview**](./types/data.md#cells.tview)|Automatically created TerraView project file.|
|[**communities.dbf**](./types/data.md#communities.dbf)|A shapefile describing some communities in Santarem, Para, Brazil.|
|[**farms.dbf**](./types/data.md#farms.dbf)|A shapefile describing the farms.|
|[**partofbrazil.dbf**](./types/data.md#partofbrazil.dbf)|A shapefile describing the some Brazilian states.|
|[**roads.dbf**](./types/data.md#roads.dbf)|Some roads of Santarem, Para state, Brazil.|