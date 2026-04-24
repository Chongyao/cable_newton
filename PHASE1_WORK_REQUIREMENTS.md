# Phase 1 Work Requirements

## 1. Phase Objective

Phase 1 focuses on **cables (1D deformables / VBD)**, with the goal of delivering **Newton-ready** cable assets and associated solver capabilities for NVIDIA's Newton physics engine.

Core objectives:

- Author all required cable asset classes per the NVIDIA cable taxonomy
- Ensure geometry and parameterization are compatible with the Newton VBD solver
- Calibrate anisotropic stiffness profiles for each cable class
- Provide at least one validation scene per asset class demonstrating plausible behavior
- Design and implement custom Newton / Warp plugin solvers where the existing Newton rod solver is insufficient
- Deliver a consolidated asset pack, plugins, documentation, and a trial retrospective

## 2. Asset Scope

Based on the Statement of Work and the NVIDIA cable taxonomy, Phase 1 covers the following cable classes:

1. Electrical wire
2. Electrical cable
3. Ribbon cable
4. Flex cable
5. Coaxial cable
6. Industrial hoses
7. Tensile / tendon cables
8. Cable bundles

> The taxonomy document also references **Bowden cables** under a miscellaneous category, but the formal SOW deliverable scope is limited to the 8 classes listed above.

## 3. Per-Asset Delivery Requirements

Each cable class must satisfy all of the following requirements.

### 3.1 Geometry and Asset Structure

- Deliver Newton-compatible cable assets for each class
- Geometry and parameterization must be compatible with the Newton VBD solver
- Triangle mesh geometry shall be generated from a centerline and material frame suitable for the Company's automated asset pipeline

### 3.2 File Format

- Deliver Open USD asset files with appropriate Newton API annotations

### 3.3 Physical Parameter Calibration

Calibrate anisotropic stiffness properties for each cable class. Parameters must cover at minimum:

| Parameter   | Description                          |
|-------------|--------------------------------------|
| bending-Y   | Bending stiffness in the X-Y plane   |
| bending-Z   | Bending stiffness in the X-Z plane   |
| torsion     | Torsional stiffness around the X axis|
| axial ±     | Tensile and compressive axial stiffness|

Calibrated values must be consistent with the material and structural characteristics described in the cable taxonomy.

### 3.4 Validation Scenes

- At least one validation scene per cable class
- Each scene must demonstrate plausible and interpretable dynamic behavior
- Acceptable scenarios include routing, insertion, or other behavior representative of real-world use

## 4. Custom Solver / Plugin Requirements

Where the Newton built-in rod solver is insufficient — particularly for cable classes that require non-isotropic bending or ribbon-like geometry — custom Newton / Warp plugin solvers must be designed and implemented. Expected cases include:

- Ribbon cable
- Flex cable
- Tensile / tendon cables
- Cable bundles
- Any other class whose behavior cannot be accurately captured by the default rod solver

Deliverables for each custom solver:

- **Design document** covering architecture, Newton / Warp integration approach, and performance targets
- **Working plugin implementation** exercised against the applicable cable class(es)

## 5. Packaging Requirements

Final deliverables must form a self-contained, usable bundle — not just individual files:

- Each custom solver / plugin must be packaged together with its corresponding asset class(es)
- A downstream customer must be able to run the provided assets using the provided plugins without additional setup
- All solver and plugin code, designs, and artifacts produced under this SOW are owned exclusively by the Company

## 6. Out of Scope

The following are explicitly excluded from Phase 1 / the 4-week trial:

- Plastic deformation, crease, and crack behavior at the material level
- Any work related to thin / surface deformables (Phase 2)
- Any work related to 3D volumetric deformables (Phase 3)
- Phase 2 and Phase 3 formal deliverables

## 7. Collaboration and Communication Requirements

In addition to technical deliverables, Phase 1 includes defined collaboration obligations:

- Attend scheduled status meetings **3 times per week** (targeting ~8:00 AM CST)
- Daily collaboration via Company-designated channels (Slack)
- Submit a **brief weekly written progress update** covering:
  - Work completed
  - Current blockers
  - Next steps
- If limitations in Newton are identified, report them to the Company (Steven Ren / Krish Mehta) first; the Company decides whether to escalate to the NVIDIA Newton team
- Do **not** share Company solver designs or plugin implementations with NVIDIA or any third party without prior written approval from the Company

## 8. Tools and Environment

| Tool / Platform               | Role                                         |
|-------------------------------|----------------------------------------------|
| Newton physics engine / Warp  | Primary simulation and VBD solver runtime    |
| Open USD                      | Asset file format                            |
| Python                        | Scripting, pipeline tooling                  |
| C++                           | Plugin / solver implementation               |
| CUDA                          | GPU acceleration as needed                   |
| Company-controlled git repo   | All code reviewed before merge               |

## 9. Milestones

### 9.1 Job Spec Version (Phase 1, 3-week plan — for reference)

| Week | Deliverable |
|------|-------------|
| 1    | Newton / VBD dev environment operational; pipeline design doc complete; first 2 cable classes delivered |
| 2    | 4 additional cable classes + validation scenes delivered |
| 3    | Final 2 cable classes delivered; Phase 1 asset pack + documentation handed off |

### 9.2 Formal SOW Version (4-week trial — **authoritative**)

| Week | Deliverable |
|------|-------------|
| 1    | Newton / Warp / VBD dev environment operational; cable asset pipeline design doc complete; first draft of solver / plugin design doc delivered; first 2 cable classes (suited to Newton's existing rod solver, e.g. electrical wire and electrical cable) delivered as Open USD assets with Newton API annotations |
| 2    | Additional cable classes + validation scenes delivered; custom plugin solver scaffold implemented and exercised against one non-isotropic cable class |
| 3    | Remaining cable classes delivered; custom solver exercised against additional non-isotropic classes (e.g. ribbon cable, flex cable, tensile / tendon cables, cable bundles) |
| 4    | Consolidated cable asset pack, custom plugin solver(s), and supporting documentation delivered; written trial retrospective submitted covering solver stability, realistic workload assessment, recommended next steps, and proposed scope for a follow-on SOW |

> Where the job spec and the SOW differ, the **formal Consulting Agreement + Exhibit A (SOW)** takes precedence.

## 10. Acceptance Criteria

All deliverables are subject to Company's internal validation and approval, in the Company's sole and reasonable discretion. If any deliverable does not satisfy validation criteria, the consultant shall make commercially reasonable corrections without additional charge until accepted.

Key acceptance requirements:

- All target cable classes completed per spec
- Assets are Newton-ready and usable in the target pipeline
- Open USD files carry correct Newton API annotations
- Calibrated stiffness profiles are consistent with taxonomy characteristics
- At least one plausible validation scene per cable class
- Custom plugin solvers (where required) are working and validated
- Final submission includes the complete asset pack, plugins, documentation, and a trial retrospective

## 11. Recommended Execution Priorities

Synthesizing all three reference documents, the recommended execution focus for Phase 1 is:

1. **Set up the environment and asset pipeline first** — establish the Newton / Warp / VBD environment and the automated asset generation workflow before authoring assets.
2. **Start with rod-solver-compatible classes** — electrical wire and electrical cable are the natural starting point.
3. **Identify custom-solver classes early** — ribbon, flex, tensile/tendon, and bundles will likely require custom solver work; begin design work in parallel, not after the simpler classes are done.
4. **Validate assets and solvers together** — do not treat asset authoring and validation scenes as separate work streams.
5. **Build toward the final bundle from day one** — assets, plugins, and docs should compose into a deliverable package at every stage.
6. **Collect retrospective material continuously** — track stability issues, actual hours, and scope surprises as they occur so the Week 4 retrospective is grounded in data.

## 12. Document Sources

This document is synthesized from:

- *Contractor Job Spec — Chongyao Zhao (Newton Deformables)*
- *Chongyao_Consulting_Agreement_v2* (including Exhibit A / Statement of Work)
- *Cable Taxonomy* (NVIDIA cable classification reference)
