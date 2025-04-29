# LifePatterns

## Functions

|   |   |
|---|---|
|[getLife](#getLife)|Return a CellularSpace from a data file available in the ca package.|
|[insertPattern](#insertPattern)|Insert a given pattern in a CellularSpace.|

## **getLife** 

Return a CellularSpace from a data file available in the ca package. It works with .life files, where the CellularSpace is stored as spaces (dead) or Xs (alive).  
  

### Arguments

- **#1**: A string with a file name without .file.

### Usage

```
import("ca")

glider = getLife("glider")
```

## **insertPattern** 

Insert a given pattern in a CellularSpace.  
  

### Arguments

- **#1**: A CellularSpace to receive the pattern.
- **#2**: A CellularSpace with the pattern.
- **#3**: The x position where the pattern will be copied on the CellularSpace.
- **#4**: The y position where the pattern will be copied on the CellularSpace.

### Usage

```
import("ca")

cs = CellularSpace{xdim = 10}
insertPattern(cs, getLife("glider"), 0, 0)
```