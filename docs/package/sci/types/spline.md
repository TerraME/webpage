# Spline

Build a Catmull-Roll spline from a set of points and returns interpolated value.  
  

### Arguments

- **points**: the set of x-ordered points in format { { x = x0, y = y0 }, { x = x1, y = y1 }, ....}.
- **steps**: how many points to interpolate btw two data points. Default is 10.

### Usage

```
import("sci")

waterSurface = Spline{
    points = DataFrame{
        x = {0, 1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000},
        y = {0, 24.7, 35.3, 48.6, 54.3, 57.2, 61.6, 66.0, 69.9}
    }
}
```

## Functions

|   |   |
|---|---|
|[value](#value)|Returns the value of the spline for a given value.|

## **value** 

Returns the value of the spline for a given value.  
  

### Arguments

- **#1**: A number value.

### Usage

```
import("sci")

waterSurface = Spline{
    points = DataFrame{
        x = {0, 1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000},
        y = {0, 24.7, 35.3, 48.6, 54.3, 57.2, 61.6, 66.0, 69.9}
    }
}

print(waterSurface:value(1500))
```