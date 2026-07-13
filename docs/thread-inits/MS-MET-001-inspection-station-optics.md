# THREAD INIT: MS-MET-001 — Modular Inspection Station Optics

## Purpose

Develop a modular optical inspection capability for Project MicroShop using surplus lenses, wedge prisms, controlled illumination, and 3D-printed mounting hardware.

The thread should begin experimentally. It must not assume the final optical architecture before the components are measured and characterized.

## Mission

Explore and develop practical bench inspection configurations for tasks such as:

- illuminated magnification
- close-focus visual inspection
- edge, finish, burr, and marking inspection
- solder-joint inspection
- small-object inspection
- camera-assisted documentation
- redirected or split illumination
- modular optical experiments that inform a standardized inspection station

## Initial Components

Engineering aliases and apparent descriptions are recorded in:

`docs/metrology/inspection-optics/component-register-v0.1.md`

Do not place purchase screenshots, names, addresses, tracking numbers, payment details, or order identifiers in the public repository.

## Dependency

This task depends on:

> **Working 3D Print Capability**

The dependency is satisfied when repeatable parts can be produced for:

- lens cells
- retaining rings or clips
- adjustable tubes
- test stands
- light baffles
- prism mounts
- camera adapters
- modular mating interfaces

The task may still advance through component inventory, measurement, characterization, and concept development before this dependency is complete.

## Design Doctrine

- Treat all optics as incompletely specified until measured.
- Do not permanently bond optics during early experimentation.
- Avoid point loading and aggressive clamping.
- Use broad, low-force, replaceable contact surfaces.
- Preserve orientation information for asymmetric components.
- Control stray light where useful.
- Prefer modular and reversible mounts.
- Separate optical experimentation from final station standardization.

## Characterization Requirements

For each component, establish where practical:

- actual diameter
- edge and center thickness
- clear aperture
- focal behavior
- useful working distance
- orientation sensitivity
- coating evidence
- surface condition
- chip or scratch condition
- safe retention method

## Initial Work Products

1. Component register
2. Dimensional measurement sheet
3. Optical characterization plan
4. Modular mount interface concept
5. First printed lens cell
6. First bench optical prototype
7. Workflow test against representative inspection tasks
8. Standardized inspection module or documented rejection of the concept

## Process-Code Starting Point

Suggested initial assignments:

- component inventory: β
- optical bench concept: α
- lens characterization plan: α
- printed mounting system: blocked at α pending print capability
- assembled prototype: not yet δ
- workflow testing: not yet ε

These assignments are provisional and should be updated only when evidence supports advancement.

## Open Questions

1. Which lenses provide useful naked-eye magnification at practical working distances?
2. Which lenses are better suited to camera coupling than direct viewing?
3. Can wedge prisms improve illumination, split a beam, or provide useful viewing geometry?
4. What standard mechanical interface should optical modules share?
5. Should the station support direct viewing, camera viewing, or both?
6. What lighting geometries best reveal burrs, scratches, surface texture, and solder defects?
7. What level of cleanliness and enclosure is justified?

## Repository Outputs

- `docs/metrology/inspection-optics/component-register-v0.1.md`
- future measurement sheets
- future CAD and printable files
- future experiment records and checkpoints
- corresponding GitHub issue for active work
