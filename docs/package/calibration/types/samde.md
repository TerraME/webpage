# SAMDE

Type to calibrate a model using genetic algorithm. It returns a SAMDE type with the fittest individual (a Model), its fit value, and the number of generations taken by the genetic algorithm to reach the result. SaMDE paper is available at: ( [https://onedrive.live.com/redir?resid=50A40B914086BD50!4054&authkey=!ACNH3WpLEBuIOME&ithint=file%2cpdf](https://onedrive.live.com/redir?resid=50A40B914086BD50!4054&authkey=!ACNH3WpLEBuIOME&ithint=file%2cpdf) ).  
  

### Arguments

- **fit**: A user-defined function that gets a model instance as argument and returns a numeric value of that particular model fitness, this value will be minimized or maximized by SAMDE according to the maximize parameter.
- **maxGen**: The maximum number of generations. If the simulation reaches this value, it stops and returns the Model that has the fittest result? TODO.
- **maximize**: An optional paramaters that determines if the fit will be maximized (true) or minimized (false, default value).
- **model**: A Model.
- **parameters**: A table with the possible parameter values. They can be values or Choices. All Choices will be calibrated.
- **size**: The maximum population size in each generation.
- **threshold**: If the fitness of a model reaches this value, SAMDE stops and returns such model.

### Attributes

Some attributes of SAMDE have internal semantics. They can be used as **read-only** by the modeler.

- **fit**: The best fitness result returned by the SAMDE Algorithm.
- **generation**: The number of generations created by the generit algorithm until it stopped.
- **instance**: The instance of the model with the best fitness.

### Usage

```

import("calibration")
local MyModel = Model{
  x = Choice{min = -100, max = 100},
  y = Choice{min = 1, max = 10},
  finalTime = 1,
  init = function(self)
    self.timer = Timer{
      Event{action = function()
        self.value = 2 * self.x ^2 - 3 * self.x + 4 + self.y
      end}
  }
  end
}
c = SAMDE{
    model = MyModel,
    parameters = {x = Choice{min = -100, max = 100}, y = Choice {min = 1, max = 10}, finalTime = 1},
    fit = function(model)
        return model.value
    end
}
```