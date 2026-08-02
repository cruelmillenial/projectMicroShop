# Project MicroShop — Capability Dependencies

This document records cross-subsystem dependencies at the capability and milestone level.

## Current Dependency Chains

### Electronics / Caliper Interface

```text
Electronics Workstation Operational
        |
        v
MS-ELC-001 iGaging SPC Reverse Engineering
        |
        v
USB Serial Validation Prototype
        |
        v
USB HID Keyboard Wedge
        |
        v
Android Measurement Tool
```

### Metrology / Inspection Optics

```text
Working 3D Print Capability
        |
        v
MS-MET-001 Modular Inspection Station Optics
        |
        v
Modular Optical Inspection Capability
        |
        v
Inspection Station Operational
```

### CAD Toolchain / Reusable Design Infrastructure

```text
MS-SW-001 FreeCAD MCP Server Setup
        |
        v
MS-CAD-002 CAD Toolchain + Parametric Modeling Infrastructure
        |
        +--> MS-CAD-001 HF Crane CAD + Measurement Register
        +--> reusable structural libraries
        +--> metrology fixtures and optical mounts
        +--> workstation / enclosure / cart / machine-base models
        +--> future physical-build CAD tasks
```

## Interpretation

### iGaging SPC Interface

The iGaging SPC reverse-engineering task is not presently blocked by lack of protocol ideas. It is blocked by the absence of a reliable, repeatable electronics measurement environment.

The **Electronics Workstation Operational** milestone should be considered satisfied when the bench can support:

- stable instrument power and placement
- dependable grounding and probe access
- logic analyzer validation against a known-good source
- repeatable oscilloscope and logic captures
- secure cable and breakout retention
- documented channel mapping
- practical storage and setup without improvised rewiring

Once that milestone is reached, MS-ELC-001 may resume from the checkpoint documented in:

`docs/electronics/igaging-spc/checkpoints/checkpoint-2026-07-10-reverse-engineering.md`

### Inspection Station Optics

MS-MET-001 depends on a working 3D-print capability because the optical components require custom, low-force, reversible mounting hardware.

The **Working 3D Print Capability** dependency is satisfied when Project MicroShop can reliably produce:

- lens cells
- retaining rings or clips
- adjustable tubes
- test stands
- light baffles
- prism mounts
- camera adapters
- repeatable modular mating interfaces

MS-MET-001 may advance through inventory, measurement, optical characterization, and conceptual design before the printing dependency is complete. Assembly and workflow testing remain blocked until suitable mounts can be produced.

### CAD Toolchain

MS-SW-001 establishes the narrow FreeCAD MCP server capability. MS-CAD-002 consumes that capability and governs the wider program-level CAD workflow.

MS-CAD-002 is shared infrastructure rather than a prerequisite that must be fully finished before physical modeling can occur. Existing physical-build models may continue while the toolchain matures, and those builds should provide test cases for the standards and reusable libraries.

The desired capability is a stable, version-aware CAD environment in which new physical-build tasks can reuse parameter conventions, library components, automation, repository structure, and export practices without rebuilding the workflow from scratch.

## PM Doctrine

When multiple dependent tasks are blocked by the same missing capability, prioritize the shared capability milestone rather than continuing low-confidence workarounds in each dependent task.

Shared infrastructure should be developed iteratively against real physical-build consumers rather than designed in isolation.
