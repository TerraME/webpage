# Utils

## Functions

|   |   |
|---|---|
|[countNeighbors](#countNeighbors)|Return the number of neighbors of a given cell that have a given value in their attribute "state".|

## **countNeighbors** 

Return the number of neighbors of a given cell that have a given value in their attribute "state".  
  

### Arguments

- **#1**: A Cell.
- **#2**: A Value. If missing, this function will return the number of neighbors of the Cell.

### Usage

```
import("ca")

Anneal = Model{
    finalTime = 100,
    dim = 80,
    init = function(model)
        model.cell = Cell{
            init = function(cell)
                if Random():number() > 0.5 then
                    cell.state = "L"
                else
                    cell.state = "R"
                end
            end,
            execute = function(cell)
                local alive = countNeighbors(cell, "L")

                if cell.state == "L" then alive = alive + 1 end

                if alive <= 3 then
                    cell.state = "R"
                elseif alive >= 6 then
                    cell.state = "L"
                elseif alive == 4 then
                    cell.state = "L"
                elseif alive == 5 then
                    cell.state = "R"
                end
            end
        }

        model.cs = CellularSpace{
            xdim = model.dim,
            instance = model.cell
        }

        model.cs:createNeighborhood()

        model.timer = Timer{
            Event{action = model.cs},
            Event{action = model.map}
        }
    end
}
```