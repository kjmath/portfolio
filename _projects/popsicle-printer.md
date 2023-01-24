---
title: "Popsicle 3D Printer"
excerpt: "A 3D printer for frozen popsicles. My friends and I built this by adapting a bed-XY printer with a custom chilled build platform and a slush extruder mechanism."
header:
  teaser: /assets/images/popsicle-printer/popsicle-printer-composite.png
order: 3.1
share: false
toc: true
toc_sticky: true
---
{% include video id="x69az8HE6NU" provider="youtube" caption="Popsicle printer." %}

*Designed and built in collaboration with Juju Wang and Prashanth Prakash.*

## Description

My friends and I built a printer to make edible, frozen popsicles. We started with a [Velleman K8200 printer](https://www.velleman.eu/products/view/?id=412554), which uses a bed-XY design. With this printer design, the print head only moves in the Z direction, and is rigidly attached to a piece of aluminum framing. This made it easier for us to change out the filament extruder for our custom slush extruder. 

### Slush extruder

A screw drive mechanism was used to extrude a partially frozen slush feedstock, as shown in the figure below.

![screw-dirve]({{ site.baseurl }}/assets/images/popsicle-printer/screw-drive.png){:width="75%"}{: .align-center}
<figcaption>A screw drive mechanism with a reservoir was used to extrude slush feedstock.</figcaption>{: .text-center}

### Chilled build plate

In order to freeze the slush feedstock into a solid popsicle, a chilled build plate was used. This was done by submerging a tray in a bath of dry ice and ethanol. We chose this method over other possible methods (refrigeration unit or LN2 injection in slush) because it was mechanically simple, and allowed us to use the printer in ambient, open air. This chilled build plate concept is shown below.

![build-plate]({{ site.baseurl }}/assets/images/popsicle-printer/build-plate.png){:width="100%"}{: .align-center}
<figcaption>Slush feedstock was printed and frozen onto a build plate chilled with a dry ice bath.</figcaption>{: .text-center}

### Integration with printer

The chilled build plate was attached to the printer using simple sheet metal brackets:

![plate-attach]({{ site.baseurl }}/assets/images/popsicle-printer/plate-bracket.png){:width="100%"}{: .align-center}

The end of the screw drive mechanism was designed to key directly with the filament extruder motor that came with the base printer kit:

![motor-screw-mate]({{ site.baseurl }}/assets/images/popsicle-printer/motor-screw-mate.png){:width="100%"}{: .align-center}

### Calibration and tuning

The relationship between the screw drive extruder mass flow rate and motor speed was measured. This measurement then let us characterize the first layer freezing time vs extrude mass flow rate:

![first-layer-freeze]({{ site.baseurl }}/assets/images/popsicle-printer/first-layer-freeze.png){:width="100%"}{: .align-center}

We selected a mass flow rate of 1.2 g/s, and with that flow rate we characterized the layer freezing time vs layer number:

![layer-num-freeze]({{ site.baseurl }}/assets/images/popsicle-printer/layer-num-freeze.png){:width="100%"}{: .align-center}

Once we'd characterized these printer parameters, we could write custom gcode for (attempted) printing of various popsicle shapes.

## Gallery of Popsicle Attempts

![popsicle-gallery]({{ site.baseurl }}/assets/images/popsicle-printer/popsicle-gallery.png){:width="100%"}{: .align-center}


