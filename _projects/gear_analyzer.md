---
name: Gear Analyzer
tools: [SolidWorks, Rapid Prototyping, CNC Machining, OpenCV]
image: /assets/gears/thumbnail.png
description: Automated gear analysis for production quality checking
---

## Overview
{% include elements/ext_link.html link="https://www.productiverobotics.com/" text="Productive Robotics "%} designs and fabricates many of parts and assemblies in house for their robots; these parts require quality and feature analysis before being deemed production ready. Gear analysis was a manual process; the most skilled employee analyzed a gear in two minutes, but even that employee occasionally made mistakes, especially when switching from one gear type to another. This machine was created to automate the gear analysis process.

Note that some parts of this machine and its purpose are proprietary and confidential. The descriptions will seem incomplete due to this.


<div class="row">
    <div class="two_column">
        {% include elements/figure.html image="assets/gears/labeled_full.png" caption="The automated gear analyzer"%}
    </div>
    <div class="two_column">
        {% include elements/figure.html image="assets/gears/full_cad.png" caption="CAD assembly (note that work was done in SolidWorks but is being viewed in Onshape)"%}
    </div>
</div>

## Mechanical Design
The gear analyzer is composed of two main sub-systems: the clamp-rotor and the imaging system. The parts that move up and down the column share a common elevator design.

### Elevator
A gear rack (1 module) and linear rail (HGH20) are attached to a 80/20 (36" 2040-S)column to allow the elevators to travel smoothly up and down. The commonized elevator is composed of an aluminum L-bracket and 3D printed platform. A motor (NEMA 17 with CAN control board) with a 16T gear is screwed directly to the L-bracket; the platform and L-bracket are screwed to a linear guide block (HGH20CA). The platform is modified for each specific use: a large hole with embedded magnets for holding the red LED disk, a hole and gear shroud for the upper clamp-rotor, and smaller holes for the camera and lens.

<div class="row">
    <div class="two_column">
        {% include elements/figure.html image="/assets/gears/elevator_front.png" caption="Front view of elevator" %}
    </div>
    <div class="two_column">
        {% include elements/figure.html image="/assets/gears/elevator_back.png" caption="Back view of elevator" %}
    </div>
</div>

### Clamp-Rotor

The clamp-rotor holds and aligns the gear perfectly vertical by closing the gear between a chamfer mill (1/4") on the bottom and center (1/8") on the top. The chamfer mill in the lower assembly is held in a ER16 collet chuck fit into a 3D printed gear. The center is embedded in a 1/8" thick clear acrylic disk clamped into a hollow gear in one of the column's elevators; the clear acrylic is necessary to allow the camera to see the gear. Two motors are also fit with 3D printed gears and mated to the lower and upper rotor gears.

Alignment of the centers is essential to successful operation of the fixture. The bottom assembly is adjusted using oversized screw holes to fasten it to the base. The upper assembly is adjusted  by sliding the acrylic plate between the gear and clamp plate before fully tightening its screws.

<div class="row">
    <div class="two_column">
        {% include elements/figure.html image="/assets/gears/bottom_section_labeled.png" caption="Section of lower clamp-rotor" %}
    </div>
    <div class="two_column">
        {% include elements/figure.html image="assets/gears/lower_assy.png" caption="The lower clamp-rotor outlined in red"%}
    </div>
</div>

<div class="row">
    <div class="two_column">
        {% include elements/figure.html image="/assets/gears/upper_center_bottom.png" caption="Bottom view of upper clamp-rotor" %}
    </div>
    <div class="two_column">
        {% include elements/figure.html image="assets/gears/upper_center_top.png" caption="Top view of upper clamp-rotor"%}
    </div>
</div>

### Imaging
The camera (Arducam B0498) and lens (50 mm) are mounted to two separate elevators, allowing the distance between camera and lens to be modified, varying focus depending on which gear is being analyzed. Gears with large diameters require that the camera be raised to the highest point of the 36" 80/20 column, otherwise a much smaller column would be used. A lens bellows was disassembled and placed between the camera and lens platforms to block light coming between the two platforms. The camera and lens are both mounted into 1/8" ABS plates that can be moved across the plaforms to adjust their alignment.

<div class="row">
    <div class="two_column">
        {% include elements/figure.html image="/assets/gears/camera_and_lens_cad.png" caption="Camera elevator and lens elevator designs" %}
    </div>
    <div class="two_column">
        {% include elements/figure.html image="assets/gears/camera_range.gif" caption="The camera and lens range of motion"%}
    </div>
</div>

The feed from the USB camera is analyzed using OpenCV. The gears analzed with this machine are all machined from single pieces of steel. This lack of color contrast makes feature detection somewhat difficult. To remedy this difficulty, the parts are backlit with a blue LED disk. The blue light disk is mounted to the lower clamp-rotor. An elevator with a red LED disk is used to light specific planes of the gears. These two disks light the background of the image blue and the top of the part red leaving the middle of the part dark, allowing several planes of features to be detected.

{% include elements/figure.html image="assets/gears/contrast.png" caption="Column and camera view (on screen) showing blue and red contrast"%}


## Analysis Process
The old manual process has ~10 manual steps. The new process has been reduced to 3 manual steps, consisting mainly of pressing buttons. These 3 steps are planned to be automated with one of Productive Robotics's cobot arms.

| General Step                              | Old Process                                                                                                                                   | New Process                                                                                                                                                                                                   |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Change gear type (if necessary)        | Select which gear type is being analyzed                                                                                                      | Select which gear type is being analyzed (no change)                                                                                                                                                          |
| 2. Insert gear                            | <mark>Manual</mark>: draw line with a marker on top of gear for visual reference                                                                |                                                                                                                                                                                                               |
|                                           | <mark>Manual</mark>: insert gear into chuck at bottom of fixture                                                                              | <mark>Manual</mark>: place gear between the clamping parts and press "close" button                                                                                                                           |
| 3. Adjust components into proper position | <mark>Manual</mark>: raise camera so that gear fills ~80% of the height of the image shown on screen (only necessary when changing gear type) | Automatic: camera, lens, and upper clamp-rotor elevators move to pre-set heights when "close" button is pressed                                                                                               |
|                                           | <mark>Manual</mark>: align the camera and gear to be perfectly vertical and coaxial                                                           |                                                                                                                                                                                                               |
| 4. Analyze                                | <mark>Manual</mark>: capture camera image                                                                                                     | <mark>Manual</mark>: press "analyze" button                                                                                                                                                                   |
|                                           |                                                                                                                                               | Automatic: red LED elevator moves to pre-set height when "analyze" button is pressed.                                                                                                                         |
|                                           | <mark>Manual</mark>: analyze image                                                                                                            | Automatic: when red LED elevator reaches proper height, camera image is captured and analyzed to find desired features using OpenCV                                                                            |
| 5. Finish and remove gear                 | <mark>Manual</mark>: remove gear from fixture                                                                                                 | Automatic: upper and lower rotors spin the gear so the desired feature is at the bottom of the image                                                                                                          |
|                                           |                                                                                                                                               | Automatic: the red LED elevator moves up                                                                                                                                                                      |
|                                           |                                                                                                                                               |                                                                                                                                                                                                               |
|                                           |                                                                                                                                               | <mark>Manual</mark>: press "open" button and remove gear                                                                                                                                                      |
|                                           |                                                                                                                                               | Automatic: upper clamp-rotor, camera, and lens elevators raise and red LED elevator lowers when "open" button is pressed. This opens up the machine to allow the gear to be removed by a person or robot arm. |

