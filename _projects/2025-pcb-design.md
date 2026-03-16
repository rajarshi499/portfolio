---
layout: project
title: Capacitive Keyboard PCB Design
description: A capacitive touch keyboard for Greek symbols, built to learn PCB design, embedded firmware, and modular design.
technologies: [KiCad, Soldering, Embedded C]
image: /assets/images/pcb/Capacitive-keyboard-preview.png
---

## Capacitive Greek Symbol Keyboard

### Problem / Motivation

While writing engineering reports, I constantly need Greek symbols like θ, λ, π, α, and β.  
Typing them in Google Docs requires navigating through *Insert → Special Characters → Search* (too tedious).

I wondered: what if there were a **small dedicated keyboard for Greek symbols**?

At the same time, I wanted to learn PCB design. As a mechanical engineering student, most of my electronics experience had been with Arduinos and breadboards, which are functional but messy. I wanted to design a **clean, purpose-built embedded device**.

This project is a **prototype capacitive touch keyboard** for Greek symbols.  
The current version includes four capacitive pads with LED feedback, powered by a Raspberry Pi Pico 2W.

Future versions will incorporate haptic feedback and wireless connectivity.

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

---

### Modular and Iteration-Friendly Design

I mounted the Raspberry Pi Pico using female headers rather than soldering it directly to the PCB. This allows the same microcontroller to be reused across future board revisions without desoldering.

Because mounting the Pico this way limits direct access to its pins, I routed selected GPIO lines, I2C, 5V, and GND to an expansion header. This allows us to add external modules (for ex. LRA haptic feedback board) without redesigning the main keyboard PCB.

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

### Development Process

The hardware pipeline was:

1. Design schematic in KiCad
2. Select footprints and component packages
3. Route the PCB
4. Fabricate boards through JLCPCB
5. Order components from LCSC
6. Hand-solder the board
7. Flash the Pico with MicroPython
8. Develop firmware for LED control and capacitive sensing

The LEDs were used initially as a simple bring-up test to confirm that the microcontroller and power system were working before implementing the sensing firmware.

---

### Debugging

During initial testing, none of the LEDs were working.

After probing the circuit with a multimeter, I discovered that the **bulk capacitor for the LED power rail had been placed in series instead of parallel**. As a result, no voltage was reaching the LED supply rail.

Bridging the capacitor restored power to the LEDs and allowed the system to function. The board now runs with individual 0.1 µF capacitors per LED, though the bulk capacitor will be corrected in the next revision.

This debugging process reinforced the importance of verifying power distribution early in board bring-up.

---

### Current Status

The LEDs and firmware infrastructure are working, and the board successfully runs LED animations.

The remaining task is tuning the capacitive sensing firmware. Determining the correct detection thresholds for the pads has proven to be the most challenging aspect so far.

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