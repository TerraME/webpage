# GPM

Type to create a Generalized Proximity Matrix (GPM). GPM is a concept used to establish relations between origins and destinations, represented as geographical objects. It has several strategies to define how two objects are connected, from basic geographical relations such as intersection area and border to connectivity networks. The relations created by GPM are not stored in external sources nor in attributes of the CellularSpaces it connects. It is necessary to use some functions of this type in order to create attributes or neighborhoods and to save the output.  
  

### Arguments

- **destination**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) or a [Network](../types/network.md), containing the destination points. When the destination is a Network, the real destinations are the targets of the network. It is possible to use the origin as destination as well.
- **distance**: Maximum distance allowed to connect an origin to a destination.
- **entrance**: Optional string that can used when the destination is a Network. Its values can be "points" or "lines" which indicates how the distances will be calculated. The default is "points". See the table below.
- **origin**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) representing the objects to be connected.
- **progress**: Optional boolean value indicating whether GPM will print messages while processing values. The default value is true.
- **strategy**: An optional string with the strategy to create a GPM.

|Strategy|Description|Compulsory Arguments|Optional Arguments|
|---|---|---|---|
|"area"|Create relations between objects that have intersection areas. This strategy can only be used with objects represented as polygons. The weight of each relation is the intersection area.|destination, origin|progress|
|"border"|Create relations between polygons that share borders. The weight of each relation is the length of the intersection border divided by the perimeter of the origin, which is a value between zero and one.|origin, strategy|progress|
|"contains"|Connect a destination to an origin that contains it. It requires that both origin and destination are represented as polygons. The weight of each relation will be one.|destination, origin, strategy|progress|
|"distance"|Connects all objects from the origin to the destination according to their distances. If the argument distance is used, then only the objects that have distance less than this value are connected. The weight of the relation will be the distance between the two objects.|destination, origin|distance, entrance, progress|
|"length"|Create relations between polygons that share borders. The weight of each relation is the length of the intersection border.|destination, origin, strategy|progress|

### Usage

```
import("gpm")

roads = CellularSpace{file = filePath("roads.shp", "gpm")}
communities = CellularSpace{file = filePath("communities.shp", "gpm")}
cells = CellularSpace{file = filePath("cells.shp", "gpm")}

network = Network{
    lines = roads,
    target = communities,
    progress = false,
    inside = function(distance, cell)
        if cell.STATUS == "paved" then
            return distance / 5
        else
            return distance / 2
        end
    end,
    outside = function(distance)
        return distance * 2
    end
}

gpm = GPM{
    destination = network,
    origin = cells,
    progress = false,
    output = {
        id = "id1",
        distance = "distance"
    }
}
```

## Functions

|   |   |
|---|---|
|[fill](#fill)|Create attributes in the origin according to the relations established by GPM.|
|[save](#save)|Save the GPM into a neighborhood file.|

## **fill** 

Create attributes in the origin according to the relations established by GPM. The values of each created attribute is always related to the weights of the connections in the GPM. These attributes are created in memory, and must be saved manually afterwards if needed.  
  

### Arguments

- **attribute**: Name of the attribute to be created.
- **copy**: An attribute (or a set of attributes) to be copied from the destination to the origin, given the selected neighbor. It can be a string, a vector of strings with the attribute names, or a named table, where the values represent the attribute names from the destination and the indexes are the attribute names to be created in the origin.
- **max**: An optional number with the maximum output value. If it is greater than max, then it will be max. The default is math.huge, meaning that there is no limitation on the maximum value.
- **missing**: Value of the output used when there is no input value available. The default value is math.huge for strategy "minimum" and -math.huge for strategy "maximum".
- **strategy**: The strategy used to create attributes. See the table below.

|Strategy|Description|Mandatory Arguments|Optional Arguments|
|---|---|---|---|
|"all"|Create one attribute for each available destination. The selected attribute name to be created will be the prefix for the attributes to be created. For each connection with unique identifier x, one attribute with the selected attribute name followed by _x will be created. If an origin is not connected to a given destination, the output for the attribute for the origin will be the value of missing.|attribute|missing|
|"average"|Average of all connection weights into one single attribute. Missing values are set to zero.|attribute||
|"count"|Count the number of neighbors.|attribute|max|
|"maximum"|Create an attribute using the maximum value among the weights of the connections.|attribute|copy, missing|
|"minimum"|Create an attribute using the minimum value among the weights of the connections.|attribute|copy, missing|
|"sum"|Sum all the weights into one single attribute. Missing values are set to zero.|attribute||

### Usage

```

import("gpm")

cells = CellularSpace{file = filePath("cells.shp", "gpm")}
farms = CellularSpace{file = filePath("farms.shp", "gpm")}

gpm = GPM{
    origin = cells,
    strategy = "area",
    destination = farms,
    progress = false
}

gpm:fill{
    strategy = "count",
    attribute = "quantity",
    max = 5
}

map = Map{
    target = gpm.origin,
    select = "quantity",
    min = 0,
    max = 5,
    slices = 6,
    color = "Reds"
}
```

## **save** 

Save the GPM into a neighborhood file.  
  

### Arguments

- **#1**: A string or a [File (base package)](../../../base/types/file.md) with the name of the file to be saved. Three extensions are allowed: '.gal', '.gwt', or '.gpm'.

### Usage

```
import("gpm")

roads = CellularSpace{file = filePath("roads.shp", "gpm")}
communities = CellularSpace{file = filePath("communities.shp", "gpm")}
cells = CellularSpace{file = filePath("cells.shp", "gpm")}

network = Network{
    lines = roads,
    target = communities,
    progress = false,
    inside = function(distance, cell)
        if cell.STATUS == "paved" then
            return distance / 5
        else
            return distance / 2
        end
    end,
    outside = function(distance)
        return distance * 2
    end
}

gpm = GPM{
    destination = network,
    origin = cells,
    progress = false,
}

gpm:save("cells.gpm")
```