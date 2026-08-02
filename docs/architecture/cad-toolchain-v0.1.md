# CAD Toolchain Architecture v0.1

## Purpose

Define the Project MicroShop CAD toolchain as shared engineering infrastructure rather than a collection of isolated model files.

## Architecture

```text
Measured inputs / design intent
        |
        v
Parameter register
        |
        v
FreeCAD native model (FCStd)
        |
        +--> reusable library components
        +--> macros / helper scripts
        +--> MCP-assisted operations
        |
        v
Validation
        |
        +--> STEP interchange
        +--> STL / 3MF fabrication
        +--> DXF / SVG / drawings
        +--> BOM / measurement exports
```

## Source of Truth

The authoritative design state should remain reconstructible from:

- native CAD source
- controlling parameters
- measured inputs
- documented assumptions
- reusable library dependencies

MCP, exports, screenshots, renders, and generated files are secondary interfaces or outputs.

## Reuse Boundary

Build-local geometry remains with the physical build until it demonstrates reuse value.

Reusable assets should be promoted only when they provide a stable interface or repeated geometry across multiple builds.

## Toolchain Layers

### Core CAD

FreeCAD and built-in modeling workbenches.

### Add-ons

Assembly tools, fastener libraries, specialized workbenches, and Project MicroShop-specific reusable assets.

### Automation

Python macros, scripts, BOM/export helpers, and MCP-assisted actions.

### Repository Infrastructure

Text standards, measurement registers, parameter sources, reusable libraries, native models, and selected generated outputs.

### Physical Build Consumers

Crane models, workstations, enclosures, metrology fixtures, carts, machine bases, optical mounts, and future MicroShop hardware.

## Version Control Principle

The toolchain must record enough environment information to distinguish:

- a model defect
- an add-on incompatibility
- a FreeCAD-version change
- an MCP failure
- an export-format limitation

Toolchain upgrades should be deliberate when active builds depend on current behavior.

## Relationship to Existing Work

- `MS-SW-001` establishes the FreeCAD MCP server capability.
- `MS-CAD-001` is an application-level crane modeling task.
- `MS-CAD-002` governs the shared CAD infrastructure that both can use.

## Desired End State

A new MicroShop physical-build thread should be able to start with:

- a known FreeCAD baseline
- a standard parameter pattern
- reusable structural and hardware components
- predictable repository placement
- known export targets
- optional MCP automation
- a documented validation path

without recreating the CAD workflow from scratch.
