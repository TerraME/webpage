# Calibration metrics and algorithms

  
**Version:** 0.5.5  
**License:** LGPL-3  
**Release:** 02/08/2018  
**Authors:** Antonio Oliveira Jr, Pedro R. Andrade, Claus Aranha  
**URL:** [https://github.com/pedro-andrade-inpe/calibration](https://github.com/pedro-andrade-inpe/calibration)  
**Contact:** [junior092006@hotmail.com](mailto:junior092006@hotmail.com), [pedro.andrade@inpe.br](mailto:pedro.andrade@inpe.br), [caranha@cs.tsukuba.jp](mailto:caranha@cs.tsukuba.jp)  
  

A package with functions for calibrating spatial models. It contains goodness-of-fit metrics as well as an automatic calibration feature using a genetic algorithm called SaMDE (Self-Adaptive Mutation in the Differential Evolution).  

## Types

|Type|Description|
|---|---|
|[MultipleRuns](./types/multipleRuins.md)|The Multiple Runs type has various model execution strategies, that can be used by the modeler to compare the results of a model and analyze it's behavior in different scenarios.|
|[SAMDE](./types/samde.md)|Type to calibrate a model using genetic algorithm.|

## Functions
|Function|Description|
|---|---|
|[GoodnessOfFit](./functions/goodnessOfFit.md)|Goodness-of-fit metrics.|
|[Utils](./functions/utils.md)|Useful functions that are used by [MultipleRuns](./types/multipleRuins.md) and [SAMDE](./types/samde.md).|

## [Examples](./functions/examples.md)
|Example|Description|
|---|---|
|[**broeke**](./functions/examples.md#broeke)|An implementation of the model described in ten Broeke, Guus, George van Voorn, and Arend Ligtenberg.|
|[**costanza**](./functions/examples.md#costanza)|Basic example for testing goodness-of-fit.|
|[**daisy**](./functions/examples.md#daisy)|Daisyworld example using multiple Runs factorial strategy.|
|[**fire-average**](./functions/examples.md#fire-average)|Fire in the forest example using multiple runs repeateated strategy.|
|[**moving-agents**](./functions/examples.md#moving-agents)|Example that uses [MultipleRuns](./types/multipleRuins.md) to compute wow many cells agents moving randomly can reach.|
|[**sir-mr-campaign**](./functions/examples.md#sir-mr-campaign)|Multiple simulations of a Susceptible-Infected-Recovered (SIR) model with a public campaign.|
|[**sir-mr-probability**](./functions/examples.md#sir-mr-probability)|Investigating the probability of infection in a Susceptible-Infected-Recovered (SIR) model.|
|[**sir-samde-fit**](./functions/examples.md#sir-samde-fit)|Infection example using SaMDE, simulates an infection spreading inside a school.|
|[**sir-samde-max-infected**](./functions/examples.md#sir-samde-max-infected)|An example of a bad calibration.|
|[**sir-samde-point**](./functions/examples.md#sir-samde-point)|Calibration of a SIR model using a single point.|
|[**yeast-mr**](./functions/examples.md#yeast-mr)|Basic example for testing [MultipleRuns](./types/multipleRuins.md) using Yeast model.|
|[**yeast-samde**](./functions/examples.md#yeast-samde)|Basic example for [SAMDE](./types/samde.md) using Yeast model.|

## [Data](./functions/data.md)
|Data|Description|
|---|---| 
|[**costanza.pgm**](./functions/data.md#costanza.pgm)|Example of a CellularSpaces for multi resolution goodness-of-fit metric.|