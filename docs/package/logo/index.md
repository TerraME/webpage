# Simple spatial ABM

  
**Version:** 0.6.2  
**License:** GPL  
**Release:** 04/25/2018  
**Authors:** Pedro R. Andrade  
**Depends:** terrame (>= 2.0)  
  
  

Implements spatial agent-based models with at most one agent per cell.  

## [Models](models.md)

|  Models | Description  |
|---|---|
|[Ants](models.md#Ants)|A colony of ants bringing food to their nest.|
|[Disease](models.md#Disease)|A SIR model implemented with agents.|
|[GrowingSociety](models.md#GrowingSociety)|Model where a given Society grows, filling the whole space.|
|[Heatbugs](models.md#Heatbugs)|Heatbugs is an agent-based model inspired by the behavior of biological agents that seek to regulate the temperature of their surrounding environment around an optimum level.|
|[Labyrinth](models.md#Labyrinth)|A labyrynth, where agents move randomly from a given entrance until an exit point.|
|[LifeCycle](models.md#LifeCycle)|A model where agents reproduce and die by age.|
|[Overpopulation](models.md#Overpopulation)|Model where Agents die by overpopulation.|
|[PredatorPrey](models.md#PredatorPrey)|Predator-prey dynamics.|
|[Schelling](models.md#Schelling)|Schelling's segregation model.|
|[SingleAgent](models.md#SingleAgent)|A single agent moving around randomly.|
|[Sugarscape](models.md#Sugarscape)|Sex, Culture, and Conflict: The Emergence of History.|

## Functions
| Function | Description |
|---|---|
|[Utils](./functions/utils.md)||


## [Examples](./functions/examples.md)
| Example | Description |
|---|---|
|[**ants**](./functions/examples.md#ants)|A scenario for the Ants model.|
|[**disease**](./functions/examples.md#disease)|Running the disease model varying the probability of infecting a connection from 0.05 to 1.|
|[**road**](./functions/examples.md#road)|Implementation of a small model where agents move along a given road.|

## [Data](./functions/data.md)
| File | Description |
|---|---|
|[**crossRoom.labyrinth**](./functions/data.md#crossRoom.labyrinth)|A room with a cross in the middle.|
|[**default.pgm**](./functions/data.md#default.pgm)|The traditional sugarscape.|
|[**maze.labyrinth**](./functions/data.md#maze.labyrinth)|A small maze.|
|[**room.labyrinth**](./functions/data.md#room.labyrinth)|An empty room.|
|[**small.pgm**](./functions/data.md#small.pgm)|A small sugarscape.|