# GoodnessOfFit

Goodness-of-fit metrics.

## Functions

|   |   |
|---|---|
|[multiLevel](#multiLevel)|Compares two CelluarSpace according to the calibration method described in Costanza's paper.|
|[pixelByPixel](#pixelByPixel)|Compares two CelluarSpaces using a pixel by pixel strategy.|
|[sumOfSquares](#sumOfSquares)|Calculates the sum of the difference of squares between two tables of a table.|

## **multiLevel** 

Compares two CelluarSpace according to the calibration method described in Costanza's paper. It returns a number with the average precision between the values of both CelluarSpaces. Source: Costanza R. Model goodness of fit: a multiple resolution procedure. Ecological modelling. 1989 Sep 15;47(3-4):199-215.  
  

### Arguments

- **discrete**: A boolean value indicating whether the values are discrete. The default value is false, meaning that the atributes are continuous.
- **k**: Value that determines the weigth for each square calibration. The default value is 0.1.
- **log**: Value indicating whether the levels should be computed using log scale: 1, 2, 4, ... until the maximum length in both directions. The default value (fales) means that all levels will be computed: 1, 2, 3, ... until the maximum length in both directions.
- **select**: A vector of strings with the names of the attributes to be compared. They must follow the same order of data.target: the first attribute is related to the first CellularSpace and so for the second one. When the target is a single CellularSpace, the two attributes must belong to it. It can also be a single string, when comparing the same attribute name in both CellularSpaces.
- **target**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) or a table with two CellularSpaces.

### Usage

```
import("calibration")

cs1 = CellularSpace{
    file = filePath("costanza.pgm", "calibration"),
    attrname = "costanza"
}

cs2 = CellularSpace{
    file = filePath("costanza2.pgm", "calibration"),
    attrname = "costanza"
}

multiLevel{
    target = {cs1, cs2},
    select = "costanza",
    discrete = true
}
```

## **pixelByPixel** 

Compares two CelluarSpaces using a pixel by pixel strategy. It returns a number with the average difference of the values in each cell of both CelluarSpaces. When the attributes are discrete, the difference between two cells will be zero when they have the same value or one if not. If all the values are equal, the output will be one. If they are completely different, it will be zero. When the attributes are continuous, the difference between the two values will be used. In this case, the returned value is the average of all differences.  
  

### Arguments

- **discrete**: A boolean value indicating whether the values are discrete. The default value is false, meaning that the atributes are continuous.
- **select**: A vector of strings with the names of the attributes to be compared. They must follow the same order of data.target: the first attribute is related to the first CellularSpace and so for the second one. When the target is a single CellularSpace, the two attributes must belong to it. It can also be a single string, when comparing the same attribute name in both CellularSpaces.
- **target**: A [CellularSpace (base package)](../../../base/types/cellularSpace.md) or a table with two CellularSpaces.

### Usage

```
import("calibration")

cell = Cell{a = 0.8, b = 0.7}
cs = CellularSpace{xdim = 10, instance = cell}

result = pixelByPixel{
    target = cs,
    select = {"a", "b"}
}

print(result)
```

## **sumOfSquares** 

Calculates the sum of the difference of squares between two tables of a table.  
  

### Arguments

- **#1**: A named table formed by other tables.
- **#2**: The attribute corresponding to the first table in table data.
- **#3**: The attribute corresponding to the second table in table data.

### Usage

```
import("calibration")
data = {a = {1, 2, 3, 4, 5}, b = {5, 4, 3, 2, 1}}
sumOfSquares(data, "a", "b")
```