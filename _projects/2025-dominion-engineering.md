---
layout: project
title: Robotic Clamp Validation for Nuclear Piping Decontamination
description: Robotic clamp validation for nuclear piping decontamination, built around automated vibration testing, calibration, and data visualization.
technologies: [Robotic Automation, Vibration Testing, MATLAB]
image: /assets/images/dominion/NU-DEC-preview.png
hero_image: /assets/images/dominion/Horizontal-NUDEC-rig.png
---

### Problem / Motivation

Dominion Energy’s **NU-DEC** system (**N**on-intrusive **U**ltrasonic **DEC**ontamination) is designed to clean nuclear piping without opening the system. Instead of invasive internal cleaning, an ultrasonic transducer excites the pipe wall at resonance, helping dislodge internal buildup so contaminants can be filtered downstream.

One challenge is that nuclear piping often includes welded joints, and those regions are more sensitive to stress concentrations. Applying high-amplitude ultrasonic vibration too close to a weld can risk damage, which limits how effectively the full pipe can be cleaned.

This project supported the development of clamp concepts intended to attenuate vibration near sensitive regions while preserving cleaning performance upstream.![Clamp Prototype on Pipe]({{ "/assets/images/dominion/chain-clamp-pipe.png" | relative_url }}){: .wide-image}


![Transducer Mounted to Pipe]({{ "/assets/images/dominion/transducer-laser-dot.png" | relative_url }}){: .wide-image}
*Ultrasonic transducer mounted to the test pipe, with the vibrometer laser point visible on the measurement surface.*

---

### Automated Testing Rig

A major bottleneck in clamp evaluation was data collection speed. Manual scanning required roughly **6 hours for 25 measurement points**, or about **864 seconds per point**.

To accelerate iteration, I helped develop an automated scanning workflow using a **6-DOF Universal Robots arm** with a **laser vibrometer** mounted as the end effector.

The measurement sequence was fully automated:

1. The robot moved to a target point on the pipe  
2. The controller triggered a relay  
3. The vibrometer captured displacement data  
4. Data was sent to a connected laptop  
5. The robot advanced to the next point  

This reduced acquisition time to roughly **2 seconds per point**, a **432× improvement** over the original manual process.

![Laser Vibrometer Setup]({{ "/assets/images/dominion/vibrometer-closeup.png" | relative_url }}){: .wide-image}
*Laser vibrometer mounted on the robotic arm for automated vibration measurements along the pipe surface.*

---

### Calibration and Spatial Alignment

To make the automated scans reliable, I developed the robot calibration workflow used to locate the pipe relative to the robot frame.

I designed a **rounded probing tool** for contact-based calibration and tuned the robot’s probing motion so it approached the pipe slowly enough to avoid measurement error. Faster probing introduced enough momentum to slightly deflect the pipe and delay contact registration, reducing calibration accuracy.

During calibration, the robot advanced the probe until contact was detected through increased joint loading. By probing points on two different pipe cross-sections, I could estimate the centers of those circles and reconstruct the pipe centerline in 3D space. This allowed scan paths to be generated consistently relative to the pipe rather than relying on manual alignment.

---

### Pipe Excitation and Thermal Reliability

The ultrasonic transducer converted electrical input into mechanical vibration for pipe cleaning and testing. Early in the internship, its documented operating time was limited to roughly **8 minutes** before overheating.

I tested and implemented a forced-air cooling setup using an industrial fan, which removed that runtime constraint and kept the transducer temperature stable during operation. Removing this thermal bottleneck made long-duration testing and higher-density scans practical, enabling the more detailed vibration mapping used later in the project.

---

### Data Acquisition and Post-Processing

I also built the software pipeline for data acquisition and post-processing using **Python and MATLAB**.

This workflow took robotic scan data and converted it into visual outputs such as line plots, heatmaps, and 3D vibration maps. These visualizations made it much easier to compare test cases and identify where standing-wave behavior was concentrating along the pipe.

The improved testing workflow was not just faster — it also produced much clearer spatial insight into how the pipe responded under ultrasonic excitation.

---

### Clamp Concepts and Experimental Findings

Multiple clamp concepts were tested during the internship, including 3D-printed clamps, resin clamps, custom cast-metal concepts, and off-the-shelf hardware mounted directly on the pipe. The goal was to identify designs that could attenuate vibration near weld-sensitive regions without compromising the cleaning zone.

Although no clamp design produced consistently acceptable attenuation across all tested configurations, the automated test platform made it possible to evaluate designs far more efficiently and with much better visibility than before.

One especially useful result came from a **high-density scan** that I ran on the vertical pipe setup. To reduce scan time while still capturing the dominant behavior, I limited the scan to **90° of pipe circumference** and the region **below the transducer**, based on symmetry assumptions in both the circumferential and axial directions.

Within that scanned region, the processed data showed that standing-wave vibration concentrated approximately **6 inches below the transducer**. Clamping that region significantly reduced downstream vibration, although the location was too close to the cleaning zone to be a practical final solution.

<div class="image-row">
  <div class="image-col">
    <img src="{{ '/assets/images/dominion/LinePlot.png' | relative_url }}" alt="High-density scan line plot">
    <p><em>Line plot of vibration amplitude versus axial distance below the transducer at multiple angular positions.</em></p>
  </div>
  <div class="image-col">
    <img src="{{ '/assets/images/dominion/3D-scan.png' | relative_url }}" alt="3D vibration map">
    <p><em>3D visualization of the same scan, showing vibration magnitude on the measured pipe surface.</em></p>
  </div>
</div>

---

### Outcome

By the end of the internship, I had helped establish a much more reliable and scalable clamp evaluation workflow, including:

- Automated robotic vibration scanning  
- Pipe-relative calibration using a custom probing tool  
- Continuous transducer operation through added cooling  
- Streamlined Python/MATLAB post-processing  
- Clear visualizations for identifying standing-wave behavior  

I also documented the full setup, calibration process, data workflow, and operating procedure so future engineers could reproduce the system and continue clamp development efficiently.