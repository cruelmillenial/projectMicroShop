# THREAD INIT: MS-CAD-002 — CAD Toolchain, Parametric Modeling, and Reusable Design Infrastructure

## Purpose

This thread governs the Project MicroShop CAD toolchain and the reusable modeling infrastructure that supports multiple physical builds.

Its focus is not any one machine, bench, crane, enclosure, or fixture. It exists to make those downstream models faster to create, easier to revise, and more consistent across the program.

## Mission

Develop and maintain a version-aware, reusable CAD workflow centered on FreeCAD, parametric modeling, automation where useful, and MCP-assisted interaction where supported.

The thread should produce durable standards, templates, libraries, naming conventions, reusable geometry, and workflow documentation rather than one-off modeling advice.

## Scope

Included:

- FreeCAD installation and version strategy
- workbench selection and compatibility
- parametric modeling doctrine
- spreadsheet-driven and property-driven models
- assemblies and reusable subassemblies
- configuration and variant handling
- reusable profiles, fasteners, structural members, and interfaces
- model naming and document structure
- coordinate systems and datum conventions
- design tables and measurement registers
- FreeCAD macros and helper scripts
- BOM export strategy
- reusable CAD templates
- interoperability between workbenches
- MCP server integration and smoke testing
- local automation interfaces
- import/export policy
- STEP/STL/DXF/3MF and native FCStd handling
- version control practices for CAD-adjacent text assets
- reproducible regeneration of generated outputs
- model validation and dependency hygiene
- reusable infrastructure for physical MicroShop builds

Excluded unless they affect the common toolchain:

- detailed design of a single physical build
- fabrication sequencing for one-off parts
- purchasing decisions unrelated to the CAD workflow
- general software administration not required by CAD or MCP

## Version-Aware Doctrine

Advice in this thread must be version-aware.

When recommending a feature, workbench, add-on, macro, MCP integration, or workflow:

1. Identify the relevant FreeCAD version or version family where practical.
2. Distinguish stable built-in capability from add-on or experimental capability.
3. Do not assume a menu path, API, workbench, or command behaves identically across releases.
4. Record known compatibility constraints when they affect reproducibility.
5. Prefer workflows that degrade gracefully when an add-on is unavailable.
6. Avoid locking the program to a fragile plugin unless the benefit clearly justifies it.

## Modeling Doctrine

Prefer models that are:

- parametric
- measurement-driven
- reusable
- modular
- inspectable
- regeneration-safe
- understandable after time away from the project

Favor source-of-truth dimensions over duplicated literals.

Where practical:

- centralize controlling dimensions
- expose important parameters clearly
- separate measured values from design assumptions
- document coordinate-system intent
- use stable references instead of fragile face/edge dependencies
- minimize topological naming sensitivity
- treat imported geometry as reference unless explicitly promoted to authoritative geometry

## Reuse Doctrine

A recurring element should become reusable infrastructure when repetition justifies it.

Candidate reusable assets include:

- Unistrut profiles
- T-slot profiles
- fastener families
- casters
- machine feet
- standard hole patterns
- interface plates
- common tubing and structural shapes
- electrical enclosure footprints
- bench and workstation envelopes
- lifting interfaces
- optical and instrument mounts
- shop-space reference geometry

The goal is to model common primitives once and instantiate or configure them across multiple physical builds.

## FreeCAD / MCP Relationship

MCP is an automation and interaction layer, not the CAD source of truth.

The native CAD files, parameters, scripts, and documented workflows remain authoritative.

MCP integration should be evaluated for:

- creating and editing parametric features
- inspecting document structure
- querying dimensions and properties
- generating repeatable operations
- validating model state
- exporting artifacts
- reducing repetitive GUI work

Any MCP workflow must retain a manual recovery path when practical.

## Relationship to Existing Tasks

### MS-SW-001 — FreeCAD MCP Server Setup

MS-SW-001 is the narrow infrastructure task for establishing and smoke-testing the MCP server environment.

MS-CAD-002 consumes that capability and defines how MCP should be used within the wider CAD workflow.

### MS-CAD-001 — HF Crane CAD + Measurement Register

MS-CAD-001 is a physical-model application task.

It should serve as an early test case for the standards and reusable infrastructure developed here, but its crane-specific geometry remains in its own task.

## Agent Deliverables

The agent responsible for this thread should progressively produce and maintain the following named deliverables.

### D1 — CAD Toolchain Baseline

Document:

`docs/cad/toolchain/cad-toolchain-baseline-v0.1.md`

Record:

- FreeCAD release/version
- distribution method
- Python version where relevant
- enabled workbenches
- critical add-ons
- MCP server implementation and version/commit where practical
- known compatibility constraints

### D2 — Parametric Modeling Standard

Document:

`docs/standards/parametric-modeling-standard-v0.1.md`

Define:

- parameter naming
- unit handling
- spreadsheet/property conventions
- coordinate and datum conventions
- measured-vs-designed dimensions
- reference stability rules
- configuration handling
- model validation expectations

### D3 — CAD Repository Layout Standard

Document:

`docs/standards/cad-repository-layout-v0.1.md`

Define where native models, generated exports, reusable libraries, scripts, measurement registers, and build-specific CAD outputs belong.

### D4 — Reusable CAD Component Register

Document:

`docs/cad/library/component-register-v0.1.md`

Track reusable parametric assets and their maturity.

### D5 — MCP Integration Runbook

Document:

`docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`

Cover:

- startup
- connectivity
- smoke tests
- failure isolation
- version notes
- safe fallback to manual FreeCAD use

### D6 — CAD Project Template

Output:

A reusable template structure for new MicroShop CAD tasks, including parameter register, assumptions, source measurements, model tree conventions, and export targets.

### D7 — Export and Interchange Policy

Document:

`docs/standards/cad-export-interchange-policy-v0.1.md`

Define intended use of:

- FCStd
- STEP
- STL
- 3MF
- DXF
- SVG or drawing exports where relevant

### D8 — Reusable Library Pilot

Output:

At least one reusable cross-project component family demonstrated in two distinct physical builds.

The existing Unistrut work is a strong candidate.

### D9 — Toolchain Validation Checkpoint

Checkpoint demonstrating that a new physical-build thread can start from the shared infrastructure and produce a model, BOM/export, and documented revision path without rebuilding the workflow from scratch.

## Initial Components to Track

The toolchain component register should begin with:

- FreeCAD
- Part Design workbench
- Part workbench
- Spreadsheet workbench
- Assembly workflow currently selected by the program
- Fasteners workbench or equivalent reusable fastener source
- UnistrutWB / Project MicroShop Unistrut parametric assets
- Python macros and scripts
- FreeCAD MCP server
- GitHub repository as durable engineering record
- native FCStd files
- neutral STEP exports
- fabrication exports such as STL/3MF/DXF as required

Versions and installation methods should be recorded in D1 rather than assumed here.

## Output Doctrine

For every significant CAD artifact, distinguish:

- source model
- source parameters
- measured input
- generated output
- fabrication export
- documentation/render

Generated files should not become the only copy of authoritative geometry.

## Initial Questions

1. What FreeCAD release should be the program baseline?
2. Which assembly workflow should be preferred and why?
3. What belongs in a shared component library versus a build-local model?
4. How should reusable components expose configurable dimensions?
5. Which generated exports belong in Git and which should be reproducible artifacts only?
6. How should native FCStd files be versioned alongside text-based parameter sources?
7. How much automation should MCP perform before it becomes harder to troubleshoot than the GUI?
8. What checks constitute a valid regenerated model?
9. How should the program handle FreeCAD or add-on upgrades without destabilizing active builds?

## Immediate First Task

Establish D1 — CAD Toolchain Baseline from the actual current FreeCAD environment, then compare the existing MS-SW-001 MCP setup and MS-CAD-001 crane workflow against that baseline.

Do not redesign existing physical models merely to conform to a standard that has not yet proven its value.
