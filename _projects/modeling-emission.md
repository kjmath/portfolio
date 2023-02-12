---
title: "End-to-End Differentiable Models and Optimization for Solid Rocket Powered Aircraft with Plume Raidant Emission"
header:
  teaser: /assets/images/modeling-emission/banner.png
excerpt: TODO
order: 1.1
share: false
toc: true
toc_sticky: true
mathjax: true
---
For applications where vehicle visibility is a concern, exhaust plume radiant emission is an important aspect of solid rocket powered vehicle performance. 
However, it is often not considered during the design phase, despite significant physical couplings with motor propulsion and trajectory.
Typical modeling approaches are computationally expensive, and rely on CFD and complicated integration schemes that are not well-suited for fast, iterative vehicle design.
To address this gap, I developed simpler models for exhaust plume radiant emission, and implemented them in the fast, flexible [AeroSandbox](https://github.com/peterdsharpe/AeroSandbox#readme) design optimization framework.

During my graduate research at MIT, I worked on a broader research effort to design, build, and characterize propulsion systems for a class of small ( < 10 kg), fast (> 100 m s<sup>-1</sup>) aircraft.
A proposed design for this class of aircraft utilizes a small, end-burning solid rocket motor and a class of slow-burning propellants doped with the burn rate suppressant oxamide, similar to the motors developed, tested, and measured in the static fires described in the [exhaust plume radiant emission experiments]({{ site.baseurl }}/projects/experiments-emission/) I conducted.
This aircraft concept, illustrated below, will be used as a case study to explore the capabilities of the developed plume radiant emission model.

![vehicle-design]({{ site.baseurl }}/assets/images/modeling-emission/vehicle_design_with_plume.png)
<figcaption>A proposed design for a class of small ( < 10 kg), fast (> 100 m s<sup>-1</sup>) aircraft. Design choices such as propellant composition and nozzle throat area influence the downstream plume flow field and exhaust plume radiant intensity.</figcaption>

## Design Optimization with CasADi and AeroSandbox

The modeling and optimization work in this thesis leverages the [AeroSandbox](https://github.com/peterdsharpe/AeroSandbox#readme) framework, a flexible framework for implementing and solving high-dimensional engineering problems including fully- or under-constrained systems of nonlinear, implicit, and differential equations.
AeroSandbox solves design problems using the [CasADi](https://web.casadi.org/) framework, which in turn leverages automatic differentiation.
Automatic differentiation is a method for evaluating computational function derivatives by decomposing functions into elementary functions which have known derivatives, and then combining those derivatives using the chain rule.
It can be used to compute derivatives for gradient-based optimization schemes and provides a computationally efficient method to solve high-dimensional engineering problems.

I successfully developed and implemented a differentiable model for exhaust plume radiant emission in the AeroSandbox framework (discussed further [below](#general-model-description)).
A comparison of the model results to experimental data is shown in the following section.

## Model Comparison with Experimental Data

### Example 1: Comparison with Plume Radiant Emission Experiments for Small, End-burning Motors

In the figure below is a comparison of model results with the [exhaust plume radiant emission measurements]({{ site.baseurl }}/projects/experiments-emission/#results) collected during the experiments for my graduate research. 
For all four static fires, both the measured and modeled spectra show a distinct peak at 4.3 &#956;m corresponding to CO<sub>2</sub> emission.
Weaker emission peaks corresponding to a CO band at 4.7 &#956;m and a combined CO<sub>2</sub> and H<sub>2</sub>O band at 2.7 &#956;m.
The measured data and modeled results show reasonable agreement across the spectrum for all four static fires, although the measured experimental data is unfortunately noisy across the spectrum, especially away from the 4.3 &#956;m CO<sub>2</sub> peak where the measured signal is weak.
Unfortunately, the radiant emission of these small, slow-burning solid rocket motors required operating the radiometric instrumentation near its lower sensitivity limit.
<!-- Even at the maximum gain setting, the exhaust plume contrast measurements utilized, at most (at the 4.3 &#956;m CO<sub>2</sub> band where the signal was strongest), 7.7% of the dynamic range of the detector. -->

![plot-all-rad]({{ site.baseurl }}/assets/images/modeling-emission/plot_all_rad_uncorrected_annotated.png)
<figcaption>TODO</figcaption>

![plot-all-flow-field]({{ site.baseurl }}/assets/images/modeling-emission/flow_field_compare.png)
<figcaption>TODO</figcaption>

### Example 2: Comparison with Avital et al. Experiment

![avital-rad]({{ site.baseurl }}/assets/images/modeling-emission/avital_rad_annotated.png)
<figcaption>TODO</figcaption>


## General Model Description

![model-concept]({{ site.baseurl }}/assets/images/modeling-emission/model_concept-crop.png)
<figcaption>Six inter-dependent sub-models are used to couple solid rocket motor design with motor exhaust plume radiant emission.</figcaption>

Six diffentiable sub-models of different coupled physical phenomena were developed and implemented to predict exhaust plume radiant intensity.
Their dependencies and information flow are shown in the figure above.
These models will be discussed in greater detail in later sections, but are summarized here:

1. The *chamber thermodynamic equilibrium* sub-model predicts the motor combustion chamber temperature $$T_c$$ and species mass fractions $$y_{ic}$$ given the propellant composition and chamber pressure $$p_c$$. This sub-model uses equilibrium thermodynmics calculations.

2. The *motor internal ballistics* sub-model determines motor equilibrium mass flow, chamber pressure $$p_c$$, and nozzle throat diameter $$d_t$$ given chamber temperature $$T_c$$, propellant $$a$$ and $$n$$ values, and desired thrust $$F$$. These values are solved using a mass flow balance between the burning propellant and the nozzle exit.

3. The *isentropic nozzle flow* sub-model determines nozzle exit temperature $$T_e$$, pressure $$p_e$$, and diameter $$d_e$$ given chamber temperature $$T_c$$, chamber pressure $$p_c$$, and nozzle throat diameter $$d_t$$. For simplicity, these values are calculated using isentropic nozzle theory assuming frozen flow in the nozzle.

4. The *plume flow field* sub-model determines temperatures, densities, pressures, and species concentrations throughout the exhaust plume given nozzle exit properties and freestream conditions. A 1D simplified plume flow field model is implemented that captures the core effects of turbulent entrainment, jet expansion, and non-equilibrium chemistry. This 1D model is efficient and compatible with AeroSandbox, and does not rely black-box CFD codes used by many studies.

5. The *afterburning kinetics* sub-model determines the species production rates $$\dot{\omega}_i$$ throughout the plume given temperatures, densities, and species mass fractions throughout the plume. This sub-model uses a simple, single reaction mechanism with a global reaction rate equation fit to reaction rates predicted by a 28 reaction mechanism. This fitted global reaction rate equation is significantly less stiff than more complicated reaction mechanisms used in other studies.

6. The *radiative transfer* sub-model determines the plume radiant intensity $$J_{\lambda}$$ given temperatures, densities, and species mass fractions throughout the plume. This sub-model integrates the radiative transfer equation along lines-of-sight through the plume, and uses the Ludwig et al. single line group model[^1].

## Implementation in AeroSandbox

### Defining Design Problems

All design problems implemented in AeroSandbox are defined as an optimization problem, even if the problem is fully constrained.
Standard optimization problems are written using four elements:

1. *Variables* are quantities in the design problem that are not known; they are degrees of freedom and their values are solved for by the optimizer.

2. *Constraints* put bounds on variables or expressions that are functions of variables. They constrain the feasible design space. Constraints can be defined as equalities or inequalities.

3. The *objective* is the function in the design problem that is to be minimized by the optimizer. This is often a relevant performance metric.

4. *Parameters* are quantities in the design problem that have a pre-selected value that may be changed to update assumptions or perform design sweeps, but are otherwise treated as a constant by the optimizer during any particular optimization.

AeroSandbox provides straightforward syntax for implementing each of these optimization problem elements for a design problem.
Each of the sub-models are implemented in separate python classes as fully constrained systems of equations; that is, there are the same number of variables as there are constraints.
Fully constrained systems do not need an objective function since the feasible space for solutions is already a single point.
The developed models can be assembled into a larger optimization problem with additional variables, constraints, parameters, and an objective if desired. 

### Model Limitations

Despite its great flexibility, the AeroSandbox framework does create some limitations on the types of models that can be used.
The most important of these limitations are described below:

1. *Glass-box models*: AeroSandbox uses automatic differentiation, which evaluates computational function derivatives by decomposing functions into elementary functions which have known derivatives, and then combining those derivatives using the chain rule. In order to evaluate these derivatives, AeroSandbox needs direct access to the code for the model. Therefore models in AeroSandbox must be "glass-box", and coded directly in python; "black-box" codes cannot be used.
	
2. *C1-continuity*: AeroSandbox uses gradient descent with automatic differentiation to solve optimization problems, which requires that models be C1-continuous with respect to any problem variables. AeroSandbox has several tools for implementing surrogate models to meet the C1-continuity requirement.

3. *Non-stiff differential equations*: AeroSandbox uses a simple trapezoidal integrator for integrating differential equations. This integrator does not converge well for stiff systems of differential equations, and therefore stiff equations should be avoided.

## In Depth Sub-model Implementation Discussion: Chamber Thermodynamic Equilibrium Example



___
*Much of the discussion on this page was borrowed from my (not yet complete) PhD thesis.*

[^1]: C. B. Ludwig et al. *Handbook of Infrared Radiation from Combustion Gases.* NASA SP-3080. NASA Marshall Space Flight Center, 1973.