---
title: "End-to-End Differentiable Models and Optimization for Solid Rocket Powered Aircraft with Plume Raidant Emission"
# header:
#   teaser: /assets/images/experiments-emission/composite.png
excerpt: TODO
order: 1.1
share: false
toc: true
toc_sticky: true
---

## Motivation

Exhaust plume radiant emission is coupled to a number of other vehicle disciplines for a solid rocket powered vehicle.
The solid rocket motor produces and accelerates the hot exhaust species that form the exhaust plume.
The vehicle trajectory affects the free stream conditions -- such as temperature, pressure and velocity -- which in turn affect the entrainment of air into the exhaust plume and subsequent chemical reactions in the plume.
For vehicles where exhaust plume radiant emission is relevant, considering it during the design phase is important for ensuring vehicle requirements and objectives can be met while accounting for the coupling of plume radiant emission with other disciplines.

Technology gaps exist, however, for integrating exhaust plume radiant emission in solid rocket powered vehicle design.
Typical modeling approaches are computationally expensive, and rely on CFD and complicated integration schemes that are not well-suited for fast, iterative vehicle design.
New, simpler models are needed that enable plume radiant emission to be practically considered during the design phase.
These models should ideally be implemented in a flexible design optimization framework such that radiant emission can be directly coupled to key design variables and other vehicle disciplines.

To address these gaps, I developed and implemented an end-to-end differentiable model for exhaust plume radiant emission coupled with solid rocket motor design parameters with [CasADi](https://web.casadi.org/) and the [AeroSandbox design optimization framework](https://github.com/peterdsharpe/AeroSandbox#readme).

## Model Overview

![model-concept]({{ site.baseurl }}/assets/images/modeling-emission/model_concept-crop.png)
<!-- <figcaption>A tip-to-tip fiberglass layup was applied to each fin pair to increase strength and stiffness of the fins.</figcaption> -->

Six sub-models of different coupled physical phenomena were developed and implemented in this thesis to predict exhaust plume radiant intensity:

1. 

___
*Much of the discussion on this page was borrowed from my (not yet complete) PhD thesis.*