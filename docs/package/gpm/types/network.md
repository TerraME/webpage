# Network

Type that represents a network. It uses a set of lines and a set of destinations that will be the end points of the network. This type requires that the network is fully connected, meaning that it is possible to reach any line from any other line of the network. Distances within and without the network are computed in different ways. In this sense, the distances inside the network should be proportionally shorter then the distances outside the network in order to allow the shortest paths to be within the network. Typically, using the Network changes the representation from space to time, meaning that traveling within the network is faster than outside. A Network can then be used to create a [GPM](../types/gpm.md), using a set of origins.  
  

### Arguments

- **error**: As default, two lines are connected in the Network only if they share exactly the same point. This argument allows two lines to be connected when there is a maximum error in the distance up to the its value. The maximum error must be just a insignificant value, otherwise, the Network might connect lines that are parallels or so close or another collateral effect. Therefore, the ideal solution for it is to correct the data. The default value for this argument is zero.
- **inside**: User defined function that converts the distance based on an Euclidean distance to a distance in the geographical space. This function is applied to every path within the network. If not set a function, will return the distance itself. Note that, if the user does not use this argument neither outside function, the paths will never use the network, as the distance within the network will always be greater than the distance outside the network. This function gets two arguments, the distance in Euclidean space and the line, and must return the distance in the geographical space. This means that it is possible to use properties from the lines such as paved or non-paved roads.
- **lines**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) with lines to create network. It can be for example a set of roads.
- **outside**: User-defined function that converts the distance based on an Euclidean distance to a distance in the geographical space. This function is applied to enter and to leave the network, as well as to try to see whether the distance without using the network is shorter than using the network. If not set a function, will return the distance itself. This function gets one argument with the distance in Euclidean space and must return the distance in the geographical space.
- **progress**: Optional boolean value indicating whether Network will print messages while processing values. The default value is true.
- **target**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) with the destinations of the network.
- **validate**: A boolean value that check if the lines is valid to build the Network. It is recommended that the lines be validated once at least. The default value is true.

### Usage

```
import("gpm")

roads = CellularSpace{file = filePath("roads.shp", "gpm")}
communities = CellularSpace{file = filePath("communities.shp", "gpm")}

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
```

## Functions

|   |   |
|---|---|
|[distances](#distances)|Returns a table with the minimal distances from a cell to all targets.|

## **distances** 

Returns a table with the minimal distances from a cell to all targets. The keys are the target ids and the values are the minimal distances to the targets through the Network.  
  

### Arguments

- **#1**: A cell with a geometry.
- **#2**: A name which indicates if the distances will be calculated using point-to-point or by the lines. Point-to-point means that the function is going to calculate the distances from the cell centroid to all points of the Network to find the minimal ones. Lines find the minimal distances using their lines. Although "points" can be more accurate, the performance using "lines" is faster than "points".

### Usage

```
distances = network:distances(cell, "lines")
cell.distance = distances[0].distance
cell.target = distances.targetId
```