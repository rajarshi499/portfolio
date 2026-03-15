---
layout: project
title: Airfoil Design
description: Wind turbine blade design, fabrication, and testing for MAE 4272 at Cornell.
technologies: [Autodesk Fusion, Microsoft Excel, Wind Tunnel Testing]
image: /assets/images/blade-assembly.png
---

As part of MAE 4272, our team designed, built, and tested a small wind-turbine blade for operation in Cornell's Big Blue wind tunnel. The goal was to maximize power extraction under a realistic wind environment while meeting strict geometric, structural, and facility constraints. The project emphasized making engineering tradeoffs and validating design decisions through experimental testing.

##### Design Process
We began by analyzing the given wind environment using a power-weighted Weibull distribution, which showed that most long-term energy production occurs near 5.3 m/s. Based on this result and facility limits, we selected a fixed operating speed of 1900 rpm, corresponding to an efficient tip-speed ratio for a three-bladed rotor. Using this operating point, we designed a twisted blade geometry based on the NACA 4412 airfoil, chosen for its predictable behavior and robustness at low Reynolds numbers. Chord and twist distributions were selected to keep blade sections operating near efficient lift-producing angles while remaining manufacturable and structurally safe.

*CAD model of the final blade geometry:*

![Blade Taper]({{ "/assets/images/blade-chord-taper.png" | relative_url }}){: .inline-image}

##### Testing & Results
The blade was tested in the wind tunnel by generating power curves across wind speeds from approximately 3.4 to 6.5 m/s. At each wind speed, brake torque was incrementally increased to measure equilibrium RPM, torque, and power. The resulting power curves consistently showed peak power near 1900 rpm and within the predicted 5.3–6.0 m/s wind-speed range. This close agreement between predicted and measured behavior validated the design approach and confirmed that the blade was optimized for the most energy-relevant operating conditions.

*Power curves at varying wind speeds:*

![Power Curve]({{ "/assets/images/blade-power-curve.png" | relative_url }}){: .inline-image}

##### My Contribution
I worked on aerodynamic design and analysis, including wind-distribution analysis, operating-point selection, and interpretation of experimental power curves. I also supported wind-tunnel testing and helped connect experimental results back to the original design assumptions.
