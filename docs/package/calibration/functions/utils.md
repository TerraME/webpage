# Utils

Useful functions that are used by [MultipleRuns](../types/multipleRuins.md) and [SAMDE](../types/samde.md). It contains basic functions to work with Models, such as checking parameters and creating random instances of a given Model.

## Functions

|   |   |
|---|---|
|[checkParameterSingle](#checkParameterSingle)|Verify if a given parameter for a Model value is a valid subset for a given Model parameter.|
|[checkParametersRange](#checkParametersRange)|Verify if a given parameter for a Model using min and max (and possibly range) values is a valid subset for a given Model parameter.|
|[checkParametersSet](#checkParametersSet)|Verify if a given parameter for a Model using a table of values is a valid subset for a given Model parameter.|
|[cloneValues](#cloneValues)|Function to create a copy of a given parameter, returns the copy.|
|[randomModel](#randomModel)|Function that returns a random model instance from a set of parameters.|
|[timeToString](#timeToString)|Function that returns the time in a higher-level representation.|

## **checkParameterSingle** 

Verify if a given parameter for a Model value is a valid subset for a given Model parameter.  
  

### Arguments

- **#1**: A model to be instantiated.
- **#2**: The name of the parameter to be checked in the parameters table.
- **#3**: The numerical index, of the parameter value to be checked, in the choosen parameter Choice table.
- **#4**: The value to be checked.
- **#5**: Optional parameter to be used if the paramater 'idx' is inside another table, it's the parameter's table name.

### Usage

```
import("calibration")

myModel = Model{
    x = Choice{-100, -1, 0, 1, 2, 100},
    finalTime = 1,
    init = function(self)
        self.timer = Timer{
            -- ...
        }
    end
}

local parameters = {x = Choice{-100, 5, 2}}
ok, err =  pcall(function()
    checkParameterSingle(myModel, "x", 2, 5)
end)

print(err) -- Error: Parameter 5 in #2 is out of the model x range.
```

## **checkParametersRange** 

Verify if a given parameter for a Model using min and max (and possibly range) values is a valid subset for a given Model parameter.  
  

### Arguments

- **#1**: A Model to be instantiated.
- **#2**: The name of the parameter to be verified in the Model.
- **#3**: A table with the values to be verified.
- **#4**: Optional parameter to be used if the paramater 'idx' is inside another table, it's the parameter's table name.

### Usage

```
import("calibration")

myModel = Model{
    y = Choice{min = 1, max = 100, step = 1},
    finalTime = 1,
    init = function(self)
        self.timer = Timer{
            -- ...
        }
    end
}

local parameters = {y = Choice{min = 20, max = 40}}
ok, err =  pcall(function()
    checkParametersRange(myModel, "y", parameters.y)
end)

print(err) -- Error: Argument 'y.step' is mandatory.
```

## **checkParametersSet** 

Verify if a given parameter for a Model using a table of values is a valid subset for a given Model parameter.  
  

### Arguments

- **#1**: A model to be instantiated.
- **#2**: The index of the parameter to be checked in the parameters table.
- **#3**: A table with the group of parameter values to be checked.
- **#4**: Optional parameter to be used if the paramater 'idx' is inside another table, it's the parameter's table name.

### Usage

```

import("calibration")

myModel = Model{
    x = Choice{-100, -1, 0, 1, 2, 100},
    finalTime = 1,
    init = function(self)
        self.timer = Timer{
            -- ...
        }
    end
}

local parameters = {x = Choice{-100, 1, 3}}
ok, err =  pcall(function()
   checkParametersSet(myModel, "x", parameters.x)
end)

print(err) -- Error: Parameter 3 in #3 is out of the model x range.
```

## **cloneValues** 

Function to create a copy of a given parameter, returns the copy.  
  

### Arguments

- **#1**: The parameter to be copied.

### Usage

```

import("calibration")
local original = {param = 42}
local copy = cloneValues(original)
```

## **randomModel** 

Function that returns a random model instance from a set of parameters. Each Choice argument will be instantiated with a random value from the available choices. The other arguments will be instantiated with their exact values. This function can be used by SaMDE as well as by [MultipleRuns](../types/multipleRuins.md).  
  

### Arguments

- **#1**: The Model to be instantiated.
- **#2**: A table of possible parameters for the model. Multiple Runs or Calibration instance.

### Usage

```

import("calibration")
local myModel = Model{
  x = Choice{-100, -1, 0, 1, 2, 100},
  y = Choice{min = 1, max = 10, step = 1},
  finalTime = 1,
  init = function(self)
    self.timer = Timer{
      Event{action = function()
        self.value = 2 * self.x ^2 - 3 * self.x + 4 + self.y
      end}
  }
  end
}
local parameters = {x = Choice{-100,- 1, 0, 1, 2, 100}, y = Choice{min = 1, max = 8, step = 1}}
randomModel(myModel, parameters)
```

## **timeToString** 

Function that returns the time in a higher-level representation.  
  

### Arguments

- **#1**: The time in seconds.

### Usage

```

import("calibration")
local t = 3670
print(timeToString(t)) -- 1 hour and 1 minute
```