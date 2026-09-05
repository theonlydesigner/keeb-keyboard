---
title: "kyps75 build journal"
author: "theonlydesigner(or perhaps Pratham Rupera)"
description: "a comprehensive log of designing a custom 75% mechanical keyboard featuring dual rotary encoders and an oled display [and me losing my sanity]."
created_at: "2026-08-20"
---

# august 20: ergonomic evaluation & keymap architecture
started the project originally thinking about a standard 60% layout, but quickly realized how much i miss dedicated arrow keys, navigation keys, and specialized macro controls during late-night coding and drawing sessions. [turns out i'm not a masochist and actually like being productive]. settled on an exploded 75% layout. spent hours tweaking key placements on keyboard layout editor (KLE), evaluating spacing for dual rotary encoders [one for master volume, one for brush size/timeline scrolling because scrolling with a mouse is for peasants] and a dedicated 0.91" oled display. spent time double-checking keycap row profiles (r1 to r4) to ensure non-standard key sizes like the short 1.75u right shift and 1u bottom-row modifiers wouldn't cause fitment issues with off-the-shelf keycap sets.
![layout planning diagram](keyboard-layout.png)
**total time spent: 2.0 hours**

# august 21: cad plate outline & mounting strategy
exported the KLE raw json data into swillkb plate builder to generate the preliminary dxf vector file for the top plate switch matrix. had a long design debate with myself over mounting styles: gasket mount, top mount, or integrated plate. while gasket mount provides better sound dampening, sandwich top mounting is far more forgiving for 3d printing and structural rigidity [and let's be real, i'm not spending 10 extra hours designing gasket tabs]. modified the switch cutout corners from crisp right angles to 0.5mm fillets to accommodate fdm 3d printer nozzle radii and prevent stress fractures around the perimeter. exported updated cad files for testing.
![plate vector draft](dxf.png)
**total time spent: 2.5 hours**

# august 22: schematic initialization & mcu pin allocation
opened kicad to begin electrical schematic capture. selected the micro-controller unit (mcu) board, mapping out total pin requirements. an 82-key matrix configured in a 6-row by 15-column layout requires 21 gpio pins. the dual ec11 rotary encoders require 2 quadrature signals and 1 push-button pin each (6 pins total), and the i2c oled screen takes 2 pins (sda/scl). [math is hard but running out of pins is harder]. placed the switch components along with 1n4148 switching diodes across every single node to prevent ghosting and key rollover issues. wired up the initial matrix grid, carefully verifying diode polarity [because desoldering 82 backwards diodes sounds like my personal hell].
![kicad schematic matrix](schematic_new.png)
**total time spent: 3.5 hours**

# august 23: peripheral wiring & bus pulldown logic
shifted focus to integrating the peripheral schematics into the main matrix schematic. wired up the i2c bus line for the 128x32 oled display, adding 4.7kΩ pull-up resistors to both sda and scl lines to ensure clean signal transmission and prevent bus locks. placed the footprint logic for the two ec11 rotary encoders, adding rc low-pass filter networks (10kΩ resistors and 10nf capacitors) to hardware-debounce the noisy encoder signals before reaching the mcu pins. [turns out hardware debouncing saves you from writing terrible software debounce code later]. consulted two friends to review the logic connections and verify i didn't create any voltage rail shorts [they basically saved me from starting a small desk fire].
![peripheral schematic detail](schematic_new.png)
**total time spent: 3.5 hours**

# august 24: footprint layout & matrix routing strategy
imported the schematic netlist into kicad pcbnew. spent the first two hours doing manual component arrangement [which is just digital tetris for nerds]. placed the 82 switch footprints in a strict 19.05mm x 19.05mm grid alignment to ensure keycap alignment matches standard key spacing. nestled the switch diodes directly underneath each switch footprint to keep trace lengths short. positioned the rotary encoder footprints in the top corners and set the oled module display window flush along the upper top bezel. verified component clear zones so switch housing clips won't collide with surrounding passive smd components.
![pcb footprint placement](pcb_new_1.png)
**total time spent: 4.0 hours**

# august 25: trace routing & clearance drc failures
the most intense routing session of the build. ran traces for the matrix rows and columns on the top layer while reserving the bottom layer primarily for a solid ground plane. ran into massive routing congestion near the usb-c cutout and mcu socket pins. kept triggering automated design rule check (drc) clearance errors due to 0.2mm trace widths overlapping trace-to-pad clearances. [drc errors are literally the bane of my existence]. had to manually drop trace widths down to 0.15mm and reroute signals around the second rotary encoder footprint. cleared all drc errors after three full rerouting passes. my eyes hurt.
![pcb trace routing completed](pcb_new_2.png)
**total time spent: 4.5 hours**

# august 27: 3d case modeling & internal standoffs
transitioned to 3d cad modeling to design the main housing. created a two-piece case design consisting of a top bezel frame and a bottom enclosure tray. modeled internal pcb mounting standoffs with m2 threaded brass insert pockets. carefully calculated wall thickness (3.0mm minimum) to avoid case flex and resonance. set an ergonomic typing angle of 6 degrees. added 0.3mm tolerance buffers around all internal walls so minor fdm printer expansion won't cause the pcb to bend or bind during installation [because 3d printers lie about their tolerances and i refuse to sand PLA for 3 hours].
![3d case cad model](case_1.png)
**total time spent: 4.5 hours**

# august 28: oled bezel, port cutouts & slicer setup
finalized the top plate cad enclosure details. designed a recessed window frame for the oled screen to sit flush without touching the glass face. created the usb-c breakout port cutout on the rear wall, adding chamfered edges for cable connector clearance [mostly so it doesn't look like i gnawed the hole out with my teeth]. exported all components as high-density stl files. imported the models into prusaslicer to configure print settings: 0.2mm layer height, 25% cubic infill for sound resonance tuning, and organic tree supports for the internal overhangs. ready for test printing and final firmware configuration.
![slicer preview and render](case_3.png)
**total time spent: 3.0 hours**
