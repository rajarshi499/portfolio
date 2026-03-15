---
layout: project
title: "EverSeat: Modular Child Car Seat"
description: Senior design project — process engineering, ANSYS crash simulation, and manufacturing planning for a car seat that replaces four.
technologies: [ANSYS Static Structural, Fusion 360, DFMEA, Composite Layup, CNC, Sustainable Minds]
image: /assets/images/Everseat-preview.png
---

EverSeat is a modular child car seat designed to safely restrain a child from infancy through age 12 using a single adaptive platform — replacing the three to four separate seats families typically buy. I served as the **Process Engineering and Integration lead** on a four-person team for MAE 4351 (Senior Design) at Cornell.

My work focused on three things: making sure the structure wouldn't fail under crash loading, figuring out how to actually manufacture it, and making sure the design decisions across the team stayed connected to our failure analysis.

##### Why This Problem Matters

Families in the U.S. spend roughly $900–$1,200 per child cycling through multiple car seats, and over 12 million seats are landfilled annually. Most of these aren't broken — they're just outgrown. We wanted to build a single platform that adapts instead of getting replaced, using a carbon fiber shell with adjustable side bolsters and repurposable components (for example, the infant leg rest becomes the headrest for older children).

##### Structural Verification with ANSYS

The most critical question for any car seat is whether it survives a crash. I ran ANSYS Static Structural simulations based on FMVSS 213 frontal collision conditions (30 mph sled test equivalent) to verify the carbon fiber shell before we committed to prototyping.

The shell was constrained at the LATCH anchor and seatbelt interfaces, with equivalent inertial loads applied across four child-weight configurations — each using the upper-bound weight for that age group to be intentionally conservative. Material properties represented a quasi-isotropic carbon fiber laminate with an estimated flexural strength of 700 MPa.

<!-- Replace with your ANSYS screenshot: -->
<!-- ![ANSYS Stress Solution]({{ "/assets/images/everseat-ansys.png" | relative_url }}){: .inline-image} -->

Results across all four configurations:

| Age Range | Upper Bound Weight | Max Von Mises Stress | Factor of Safety |
|---|---|---|---|
| 6 mo – 2 yr | 15 kg | 224 MPa | 3.7 |
| 2 – 4 yr | 24 kg | 227 MPa | 3.3 |
| 4 – 8 yr | 37 kg | 233 MPa | 2.8 |
| 8 – 12 yr | 59 kg | 236 MPa | 2.5 |

The highest stresses occurred in the oldest configuration as expected, and all remained well below the material limit. This confirmed that the primary load-bearing structure doesn't approach fracture under crash-level loading — the most critical failure mode we identified in our DFMEA.

This simulation doesn't replace regulatory certification (that requires physical sled testing with instrumented dummies), but it served as an early verification gate that gave us confidence to move forward with the design.

##### From DFMEA to Design Decisions

Our DFMEA wasn't just a table we filled out for a grade — it actively shaped design choices. A few examples of how failure analysis drove the engineering:

The risk of "false lock states" from partial hinge engagement led us to design a single-piece titanium locking plate that links all detent pins, guaranteeing simultaneous engagement. The concern about two-handed operation contradicting our accessibility goals pushed us toward mechanisms that can be adjusted with one hand. And the risk of fabric tearing during repeated removal led us to use snap fasteners instead of Velcro for the washable merino wool covers.

These connections between the DFMEA and actual hardware decisions were something I worked to maintain throughout the project — making sure the failure analysis stayed upstream of design, not downstream.

##### Manufacturing Process

I developed the full manufacturing process plan, thinking through each stage from composite layup to final assembly:

**Composite Shell:** Hand layup of carbon fiber sheets into a three-piece aluminum mold, vacuum bagged and oven cured. After demolding, the shell gets CNC trimmed to final edge geometry, sanded, and finished with a polyurethane/gelcoat surface layer to prevent delamination. Threaded titanium inserts are then bonded in at predetermined locations for hinge and hardware mounting.

**Titanium Mechanisms:** The hinge system and belt clamp components are CNC milled from Ti-6Al-4V for its strength-to-weight ratio and machinability. Each part gets deburred, tolerance-checked with calipers and pin gauges, and temporarily assembled on a fixturing block to validate mechanism behavior before installation.

**Comfort Stack:** Cork sheets are laser-cut and bonded to polyurethane foam using heat-activated adhesive film. The foam is shaped via hot wire cutting, and the outer merino wool cover is patterned, sewn, and attached with snaps. The full stack goes through compression set evaluation and repeated install/removal testing before integration.

**Quality Control:** Layup uniformity and cure temperature are inspected to prevent voids. Titanium components undergo cycle testing for smooth rotation and reliable lock engagement. The comfort stack is verified through repeated installation to confirm stitching integrity and foam stability.

##### Sustainability

We ran a Sustainable Minds analysis comparing EverSeat to the Chicco Convertible (the closest competitor in multi-stage coverage). EverSeat showed a 47.9% reduction in CO₂-equivalent emissions across the full product lifecycle, driven primarily by the carbon fiber and bio-based material choices versus the stainless steel and polypropylene in conventional seats.

##### What I Learned

This project taught me that manufacturing planning isn't something you do after the design is "done" — it has to happen in parallel, because the decisions about how something gets made constrain what you can design in the first place. The DFMEA was only useful because we kept it alive throughout the project instead of treating it as a one-time deliverable. And the ANSYS work reinforced that simulation is most valuable when you're honest about what it can and can't tell you — our results were strong, but I was careful to frame them as a feasibility gate, not a certification claim.
