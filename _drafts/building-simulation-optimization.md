# Building Simulation Optimization

Building Simulation Optimization is the process by which the design of a building is optimized by running many computer simulations.

## GenOpt and EnergyPlus

**GenOpt** or *Generic Optimization Program* is an optimization program for the minimization of a cost function that is evaluated by an external simulation program like [EnergyPlus](https://energyplus.net/) [[1](1)].

**EnergyPlus** is a whole building energy simulation program that engineers, architects, and researchers use to model both energy consumption--for heating cooling, ventilation, lighting and plug and process loads--and water use in buildings [[2](2)].

Together these programs can optimize the design of a building through running many simulations.

1. Install the latest compatible version of EnergyPlus

2. Install GenOpt
* `git clone https://github.com/lbl-srg/GenOpt.git`
* `cd GenOpt`
* Follow README instructions for your particular OS
  * `java -jar genopt.jar example/quad/GPSHookeJeeves/optLinux.ini`

[1]: http://simulationresearch.lbl.gov/GO/
[2]: https://energyplus.net/