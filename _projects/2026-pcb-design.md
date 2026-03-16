---
layout: project
title: Capacitive Keyboard PCB Design
description: Capacitive touch keyboard for Greek symbols, built to explore PCB design, embedded firmware, and modular hardware design.
technologies: [KiCad, Capacitive Sensing, Embedded Systems]
image: /assets/images/pcb/kicad-render-preview.png
# hero_image: /assets/images/pcb/kicad-render.png
---

### Problem / Motivation

While writing engineering reports, I constantly need Greek symbols like θ, λ, π, α, and β.  
Typing them in Google Docs requires navigating through *Insert → Special Characters → Search* (too tedious).

What if there were a ***small dedicated keyboard for Greek symbols?***

At the same time, I wanted to learn PCB design. As a mechanical engineering student, most of my electronics experience had been with Arduinos and breadboards, which are functional but messy. I wanted to design a **clean, purpose-built embedded device**.

This project is a **prototype capacitive touch keyboard** for Greek symbols.  
The current version includes four capacitive pads with LED feedback, powered by a Raspberry Pi Pico 2W.

The current prototype is designed with expansion in mind, including support for future haptic feedback modules and wireless functionality using the existing Pico 2W hardware.

---

### Design Overview

The keyboard uses **capacitive touch sensing** instead of mechanical switches. The Raspberry Pi Pico repeatedly charges each pad and then measures how long it takes for the pad to discharge. When a finger touches the pad, the capacitance changes, altering the discharge time and allowing the microcontroller to detect a press.

To make the sensing stable and predictable, each pad discharges through a **1M pull-down resistor**, which controls the discharge rate. Without this resistor the pads would discharge unpredictably, making it difficult to tune the sensing thresholds.

Key hardware components:

- Raspberry Pi Pico 2W microcontroller
- Four capacitive touch pads
- RGBW LEDs for visual feedback
- Expansion header for future haptic driver board
- 2-layer PCB designed in KiCad

The board was fabricated through JLCPCB using an **ENIG surface finish**, which provides a smoother surface and better durability for capacitive pads.

![Board Schematic]({{ "/assets/images/pcb/schematic.png" | relative_url }}){: .wide-image}

*Annotated schematic of the Pico 2W, touch pads, LED feedback circuit, and expansion header.*

---

### Modular and Iteration-Friendly Design

I mounted the Raspberry Pi Pico using female headers rather than soldering it directly to the PCB. This allows the same microcontroller to be reused across future board revisions without desoldering.

Because mounting the Pico this way limits direct access to its pins after assembly, I routed selected GPIO lines, I2C, 5V, and GND to an expansion header. This allows external modules, such as an LRA haptic feedback board, to be added without redesigning the main PCB.

![Top Board Layout]({{ "/assets/images/pcb/modular-design-layout.png" | relative_url }}){: .wide-image}

*Annotated layout showing the socketed Pico headers and expansion header.*

---

### PCB Design Considerations

Routing the board on only **two layers** was one of the more challenging aspects.  
I wanted to keep fabrication inexpensive while maintaining clean layout practices.

Several layout constraints were important for reliable capacitive sensing:

- Avoiding ground pours beneath capacitive pads
- PCB mounting screws at least ~5 mm away from pads
- Avoiding parallel runs between 5V traces and sensing traces
- Strictly 45º angle trace bends
- All traces clear of the Pico W antenna region
- Clean and debuggable layout

These considerations helped reduce electrical noise that could interfere with capacitive measurements.

All passive components use **0805 packages** to keep the board hand-solderable.

---

### Debugging

The LED circuit served as an early bring-up check for the microcontroller and power system before I moved on to the more complex capacitive sensing firmware.

During initial bring-up, the LED test failed, which suggested the problem was in the power path rather than the sensing logic. Using a multimeter, I found that the **bulk capacitor for the LED rail had been placed in series instead of parallel**, which prevented voltage from reaching the LEDs.

Temporarily bridging the capacitor restored power and allowed the system to function. The board now runs with individual 0.1 µF capacitors per LED, though the bulk capacitor placement will be corrected in the next revision.

This reinforced the importance of verifying power distribution early in board bring-up.

---

### Current Status

The LEDs and firmware infrastructure are working, and the board successfully runs LED animations.

The primary remaining task is tuning the capacitive sensing firmware. Determining robust detection thresholds for the pads has been the most challenging aspect of the project so far.

![LEDs On]({{ "/assets/images/pcb/LED.png" | relative_url }}){: .wide-image}

*Board bring-up with LED feedback functioning.*

---

### Next Steps

Near-term expansions on current board:

- Adding an external **LRA haptic feedback module** through the onboard expansion header
- Finishing capacitive sensing calibration and threshold tuning
- Exploring BLE communication using the existing **Pico 2W** hardware

A future board revision may include:

- Refine and fix layout mistakes
- More capacitive pads
- Direct integration of the **RP2350 microcontroller** instead of the Pico module
- Consolidation of haptic support onto the main PCB

The long-term goal is to create a lightweight, customizable keyboard designed specifically for engineers and researchers who frequently use mathematical notation.