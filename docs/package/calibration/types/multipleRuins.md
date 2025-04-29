# MultipleRuns

The Multiple Runs type has various model execution strategies, that can be used by the modeler to compare the results of a model and analyze it's behavior in different scenarios. It returns a [MultipleRuns](./multipleRuins.md) table with the results.  
  

### Arguments

- **folderName**: Name or file path of the folder where the simulations output will be saved. Whenever the Model saves one or more files along its simulation, it is necessary to use this argument to guarantee that the files of each simulation will be saved in a different directory.
- **free**: If true, then the memory used by Model instances will be removed after each simulation. Only the observed properties of the model will be stored within MultipleRuns. Default is false.
- **hideGraphics**: If true (default), then sessionInfo().graphics will disable all charts and observers during models execution.
- **init**: An optional user-defined function that gets a model instance and executes before running the model.
- **model**: The Model to be instantiated and executed several times.
- **parameters**: A table with the parameters to be tested. These parameters must be a subset of the parameters of the Model with a subset of the available values. They may have any name the modeler chooses.
- **quantity**: number of samples to be created in sample strategy execution.
- **repetition**: repetition of runs that must be executed with the same parameters. The default value is 1.
- **showProgress**: If true, a message is printed on screen to show the models executions progress on repeated strategy, (Default is false).
- **strategy**: Strategy to be used when testing the model. See the table below:

|Strategy|Description|Mandatory arguments|Optional arguments|
|---|---|---|---|
|"factorial"|Simulate the Model with all combinations of the argument parameters.|model, parameters|folderName, free, hideGraphics, init, quantity, repetition, showProgress, summary, ...|
|"sample"|Run the model with a random combination of the possible parameters|model, parameters, repetition|folderName, free, hideGraphics, init, quantity, showProgress, summary, ...|
|"selected"|This should test the Model with a given set of parameters values. In this case, the argument parameters must be a named table, where each position is another table describing the parameters to be used in such simulation.|model, parameters|folderName, free, hideGraphics, init, quantity, repetition, showProgress, summary, ...|

- **summary**: A function can be defined by the user to summarize results after executing all repetitions of a set of parameters. This function gets as a parameter a table containing the values of each variable, the results of each simulation and results of each user-defined functions.
- **...**: Additional functions can be defined by the user. Such functions are executed each time a simulation of a Model ends and get as parameter the model instance itself. MultipleRuns will get the returning value of these function calls and put it into a vector of results available in the returning value of MultpleRuns.

### Attributes

Some attributes of MultipleRuns have internal semantics. They can be used as **read-only** by the modeler.

- **output**: A DataFrame with the final values in each model execution. The additional functions used as arguments for MultipleRuns will also generate attributes whose name will be the function's name, and whose values will be the returning value of such function given the final state of the model as argument.
- **parameters**: A table with parameters used to instantiate the model in this simulation. Also indexed by execution order.
- **simulations**: A table with directory names. A directory is created for each model instance to save the output functions result. It is indexed by execution order.

### Usage

```

-- Complete Example:
import("calibration")
local MyModel = Model{
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

local RainModel = Model{
    water = Choice{min = 0, max = 100},
    rain = Choice{min = 0, max = 20},
    finalTime = 2,
    init = function(self)
        self.timer = Timer{
            Event{action = function()
                self.water = self.water + (self.rain - 150)
            end}
        }
    end
}

c = MultipleRuns{
    model = MyModel,
    strategy = "sample",
    showProgress = false,
    quantity = 5,
    parameters = {
        x = Choice{-100, -1, 0, 1, 2, 100},
        y = Choice{min = 1, max = 10, step = 1},
        finalTime = 1
    },
    additionalOutputfunction = function(model)
        return model.value
    end,
    additionalFunction = function(model)
        return model.value/2
    end
}

-- Selected Example:
m = MultipleRuns{
	model = MyModel,
 showProgress = false,
	parameters = {
		scenario1 = {x = 2, y = 5},
		scenario2 = {x = 1, y = 3}
	 },
	additionalF = function(model)
		return "test"
	end
}

-- This should run the model 10 times with the same parameters:
r = MultipleRuns{
    model = RainModel,
    showProgress = false,
    parameters = {repeatScenario = {water = 10, rain = 20, finalTime = 1}},
    repetition = 10
}

-- Factorial Example. It will run the model 2*66 times to test all the possibilities
-- for the parameters repetition times.
MultipleRuns{
    model = RainModel,
    showProgress = false,
    strategy = "factorial",
    parameters = {
        water = Choice{min = 10, max = 20, step = 1},
        rain = Choice{min = 10, max = 20, step = 2},
        finalTime = 1
    },
    repetition = 2
}

-- Sample Example:
MultipleRuns{
    model = RainModel,
    strategy = "sample",
    showProgress = false,
    parameters = {
        water = Choice{min = 10, max = 20, step = 1},
        rain = Choice{min = 10, max = 20, step = 2},
        finalTime = 10,
    },
    quantity = 5
}

-- This should run the model 5 times selecting random values from the defined parameters
-- (if they are choice, otherwise use the only available value).
-- This should run the model two times with the same parameters defined in the vector of parameters.
```