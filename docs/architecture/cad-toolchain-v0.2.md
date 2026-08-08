# CAD Toolchain Architecture v0.2

## Purpose

Define Project MicroShop CAD infrastructure without assuming that every physical build uses the same native parametric authoring system.

This revision extends v0.1 to support both FreeCAD-native and code-based KCL-first workflows.

## Core Principle

The authoritative design state should remain reconstructible from:

- measured inputs
- design intent
- controlling parameters
- authoritative parametric source
- documented assumptions
- reusable library dependencies

The authoritative parametric source may differ by project.

## Supported Source Patterns

### FreeCAD-Native Pattern

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

Use this pattern when FreeCAD contains the primary parametric design logic.

### KCL-First Pattern

```text
Measured inputs / design intent
        |
        v
KCL parameters and source
        |
        +--> Codex / text-based editing
        |
        v
Zoo execution
        |
        v
STEP interchange snapshot
        |
        v
FreeCAD downstream use
        |
        +--> visual inspection
        +--> assemblies / reference geometry
        +--> drawings / follow-on operations
        +--> MCP-assisted inspection or edits
```

Use this pattern when KCL remains the primary parametric design source.

FreeCAD changes to imported STEP geometry do not automatically propagate back to KCL.

## Source-of-Truth Rule

Every CAD project should declare its authoritative parametric source explicitly.

Examples:

```text
Authoritative source: FCStd
```

or:

```text
Authoritative source: KCL
Interchange snapshot: STEP
Downstream inspection environment: FreeCAD
```

Do not infer source authority from file extension presence alone.

## Toolchain Layers

### Parametric Authoring

May include:

- FreeCAD
- KCL
- future program-approved authoring systems

### Geometry Execution / Translation

May include:

- FreeCAD recompute/export
- Zoo KCL execution and export
- neutral STEP interchange

### Automation

May include:

- Python macros
- shell wrappers
- Codex CLI
- MCP-assisted actions
- headless FreeCAD validation

### Repository Infrastructure

Includes:

- source files
- parameter records
- measurement registers
- reusable libraries
- project README/STATUS files
- selected generated interchange or fabrication outputs
- toolchain and compatibility documentation

## Repository Continuity

Interactive AI sessions are working contexts, not durable project memory.

Repository-local continuity should use:

- `AGENTS.md` for standing CAD/toolchain instructions
- project `README.md` for stable definition and file roles
- project `STATUS.md` for current handoff state
- checkpoint documents for significant workflow findings
- Git history for authoritative file-change history

## Local Tool Pinning

Where practical, external CLI tooling used by automated CAD workflows should be version-recorded and may be placed in a project-local tooling location such as:

```text
.tools/bin/
```

This reduces ambiguity from mutable global PATH state.

Credentials and authentication tokens must not be committed.

## Validation Doctrine

Validation should occur at the boundaries that matter for the active source pattern.

For FreeCAD-native work:

- model recomputes cleanly
- expected objects exist
- outputs export successfully

For KCL-first work:

- local source imports resolve
- KCL executes successfully
- generated STEP exists and is nonempty
- STEP imports into FreeCAD successfully
- representative geometry is visually and dimensionally reviewed

A static source check alone does not establish geometric validity.

## Reuse Boundary

Build-local geometry remains with its physical build until it demonstrates reuse value.

Reusable assets should be promoted only when they provide a stable interface or repeated geometry across multiple builds.

## Version Control Principle

The toolchain must record enough environment information to distinguish:

- source/model defect
- authoring-tool defect
- add-on incompatibility
- FreeCAD version change
- MCP failure
- Zoo/KCL execution failure
- interchange-format limitation
- automation-wrapper defect

Toolchain upgrades should remain deliberate when active builds depend on current behavior.

## Relationship to Existing Work

- `MS-SW-001` establishes FreeCAD MCP server capability.
- `MS-CAD-001` is an application-level crane modeling task.
- `MS-CAD-002` governs shared CAD infrastructure.
- `cad/lathe_cabinet/` is an early application of the KCL-first pattern.
- `docs/cad/toolchain/checkpoints/cad-mcp-poc-2026-08-08.md` records the initial KCL → Zoo → STEP → FreeCAD PoC.

## Desired End State

A new physical-build thread should be able to select an approved source pattern and begin with:

- a known authoring-tool baseline
- explicit authoritative-source declaration
- standard parameter and measurement conventions
- reusable components where available
- predictable repository placement
- known interchange/export targets
- optional MCP/AI automation
- documented validation and recovery paths

without recreating the CAD workflow from scratch.
