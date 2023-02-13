---
title: "3D Printed Titanium Rocket Motor Closure"
header:
  teaser: /assets/images/printed-closure/printed-closure-composite.png
excerpt: I designed a 3D printed Ti-6Al-4V rocket motor closure in collaboration with Renishaw PLC. I successfully used the closure in a static fire for a small solid rocket motor.
order: 2
share: false
toc: true
toc_sticky: true
---

I designed a 3D printed Ti-6Al-4V rocket motor closure in collaboration with Renishaw PLC. 
The closure was used for a small, end-burning solid rocket motor, which posed unique design requirements. These requirements led to the design of a thin, light-weight, tapered closure that was best suited to manufacturing via additive methods. I successfully used the closure in a static fire for a small solid rocket motor.

## Design

This after closure is a part of a rocket motor I use for research of small, low-thrust solid rocket motors that will ultimately be used in small aircraft applications. As shown in the CAD below, the aft closure serves as an adapter between the aft end of the motor and the miniature nozzle. The closure has a tapered geometry, which mimics the shape of the aft end of the aircraft that this motor would be used in.

![aft-section-CAD]({{ site.baseurl }}/assets/images/printed-closure/aft-section-CAD-annotated.jpg)
<figcaption>CAD section view of aft closure installed in motor.</figcaption>

Ti-6Al-4V metal is used for this part, given its relatively high maximum service temperature and (strength / density) ratio. The thickness of the closure should be as thin as possible to minimize the mass of the part. This thin, tapered part would be time-consuming to manufacture via subtractive methods, and would waste a significant amount of material in the process. Additive manufacturing was chosen for fabricating this part, and the part was designed with the constraints of additive manufacturing in mind. 

This closure was designed in collaboration with engineers at Renishaw PLC, who ultimately manufactured the part. The printed closure, after secondary machining operations, is shown below.

![closure]({{ site.baseurl }}/assets/images/printed-closure/closure-annotated.png)
<figcaption>3D printed titanium rocket closure.</figcaption>

The wall thickness of the aft closure is limited by the minimum thickness that can reliably be achieved with their metal powder bed fusion process, about 1.3 mm. The part was oriented during the print with the larger diameter end of the part at the bottom. This is the best orientation for printing, since the part is generally self supporting in this orientation. The threaded through-holes on the tapered portion of the part are instrument ports. Support tabs were added on the bottom sides of these threaded ports to support them during the print. The part was printed with additional material at the base where the o-ring glands and motor case interface holes are located, so that the outer diameter and o-ring gland dimensions could be turned precisely after printing.  

## Analysis

Before designing the parts, I did some brief hand calculations to verify the hoop stress due to pressure loads and the bearing stress at the motor case interface holes would not yield the part during use. Hand calculations were completed for material properties at room temperature and at 800 K, using the MMPDS handbook to determine material properties of Ti-6Al-4V at elevated temperature. After designing the part, I subsequently used the SolidWorks Simulation FEA tool to do a more rigorous analysis of the stresses in the part to ensure the material would not yield during use in a static fire.

## Manufacturing

The part was printed using a powder bed fusion process at Renishaw PLC. After completing the design, I created two STEP files for the manufactuer: one with the as-printed geometry, and one with the final machined geometry. I also created an engineering drawing with GD&T to communicate the final required dimensions and tolerances. This drawing can be seen below, or a PDF of this drawing can also be viewed [here]({{ site.baseurl }}/assets/images/printed-closure/aft-section-drawing.pdf).

![aft-section-drawing]({{ site.baseurl }}/assets/images/printed-closure/aft-section-drawing.jpg)
<figcaption>Drawing of the aft closure.</figcaption>

## Test

This aft closure was used in a static fire of a small experimental rocket motor testing a new propellant and nozzle design. The aft closure performed as expected, and showed no damage upon inspection after the motor test.

![closure-burn]({{ site.baseurl }}/assets/images/printed-closure/motor-burn.png)
<figcaption>3D printed titanium rocket motor closure in use during a static fire of a small rocket motor.</figcaption>