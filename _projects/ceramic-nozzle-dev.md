---
title: "Small, Long Endurance Ceramic Rocket Nozzle Development"
header:
  teaser: /assets/images/ceramic-nozzle-dev/ceramic-nozzle-dev-composite.png
excerpt: I designed, manufactured, and tested ceramic nozzles suitable for small, long-endurance rocket motors with the novel use of 3D-printed silica and alumina-silicate materials. 
order: 4
share: false
toc: true
mathjax: true
---

## Overview

Typical solid rocket motors rely on transient methods -- such as ablation or heat-sinking -- for managing heat transfer through the nozzle and maintaining acceptable temperatures in the motor case. A large motor can use an ablative nozzle, which might erode by several millimeters during the motor burn; since these few millimeters represent only a small fraction of the nozzle throat diameter, the motor's thrust barely changes. A short-duration motor can rely on simple heat-sinking methods; the heat capacity of the motor case is often sufficient such that the heat transferred to it during the short motor burn does not unreasonably increase the temperature. However, these methods do not work for a small, long-endurance solid rocket motors. The nozzles for these motors require a steady-state insulation technique to ensure the temperature limits of the motor case material are not exceeded. 

## Nozzle material and design considerations

These nozzles are designed for a small, rocket-powered, low-thrust, long-endurance aircraft concept described [here](https://doi.org/10.2514/1.B38104). This aircraft concept utilizes a long-endurance solid rocket motor with a specially developed class of slow-burning solid rocket propellants.

The materials and design for these nozzles should be chosen to provide a high maximum service temperature (the operating temperature of the nozzle is 1500 - 2000 K), a low thermal conductivity (< 5 W m<sup>-1</sup> K<sup>-1</sup>), and good thermal shock properties with a critical fracture temperature change $$ \Delta T_f$$ > 1000 K. 

## Nozzle 1: Two-piece ceramic nozzle with 3D-printed cellular ceramic insulator

*This nozzle was designed in collaboration with Dr. Matthew Vernacchia, and more information can be found in our paper [here](https://doi.org/10.2514/1.B38104).* 

Dr. Vernacchia and I designed a two-piece nozzle configuration with a 3D-printed cellular ceramic nozzle insulator. The two-piece nozzle configuration, illustrated generally in the figure below, uses a nozzle insulator and contoured nozzle insert which are manufactured separately and then bonded together with a silica adhesive. The contoured nozzle insert is turned from boron nitride rod.

![two-piece-concept]({{ site.baseurl }}/assets/images/ceramic-nozzle-dev/two-piece-concept.png){:width="75%"}{: .align-center}
<figcaption>Two-piece nozzle concept with nozzle insert and insulator.</figcaption>{: .text-center}

The 3D-printed ceramic insulator is based on a hexagonal honeycomb that is wrapped around a cylinder, as shown below. This design concept has several advantages: the honeycomb structure reduces the stiffness of the nozzle, making it more resistant to thermal shock; thin wall reduce conductive heat transfer radially through the part; small cells reduce convection; and the multiple layers of cell walls create redundant gas seals.

![cellular-concept]({{ site.baseurl }}/assets/images/ceramic-nozzle-dev/cellular-concept.png){:width="75%"}{: .align-center}
<figcaption>Concept for a 3D-printed cellular ceramic nozzle insulator.</figcaption>{: .text-center}

The design is compatible with a stereolithography printing process, and was ultimately manufactured using a Form 2 stereolithography printer. The part is printed using the Formlabs Silica resin, which consists of a photosensitive polymer resin filled with silic particles. After printing, the part must be subsequently fired in a kiln to burn off the polymer and sinter the silica particles together. This results in part shrinkage, and so the part must be oversized when printing. An image of a printed insulator with a bonded contoured nozzle insert is shown below.

![bonded-nozzle]({{ site.baseurl }}/assets/images/ceramic-nozzle-dev/bonded-nozzle.JPG){:width="75%"}{: .align-center}
<figcaption>3D-printed silica nozzle insulator with bonded nozzle insert.</figcaption>{: .text-center}

The nozzles were manufactured and tested successfully in small, long-endurance test motors.
However, there are some manufacturing and performance drawbacks for this nozzle design.

Boron nitride is a relatively soft material, and consequently the tested nozzles using the boron nitride inserts showed nozzle erosion, which decreases the expansion ratio and specific impulse of the motor.

The 3D-printing process for the cellular ceramic insulation was also unreliable.
The thin cell walls were printed near the minimum resolution of the printer for this resin, which lead to inconsistent wall thicknesses.
The silica filled polymer used for the printing process was especially viscous, and often led to failed prints where the insulator broke off from its supports mid-print.
The insulators had inconsistent material shrinkage during the kiln firing process, which varied between 14 - 20 % in the $$r \theta$$ directions and 15 - 22 % in the $$z$$ direction for 29 different nozzle insulator iterations. Additionally, the use of a two-piece configuration inherently requires an additional machining step and a bonding step than would be required by a configuration where the nozzle insulator and insert was a single piece.

Following these manufacturing difficulties, I developed a new single-component nozzle design, which is discussed in the next section.

## Nozzle 2: Single-piece alumina-silicate nozzle