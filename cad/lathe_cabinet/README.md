# Lathe Cabinet CAD Workspace

## Purpose

This directory contains the CAD project for the lathe cabinet / stand build.

The working structure is intentionally organized around **design lineage and project ownership**, not primarily by file format. The successful KCL/Zoo proof of concept established this as a better fit for this project than the earlier illustrative `source-zoo/`, `interchange/`, `freecad/`, and `exports/` directory sketch.

## Design Origin

The project includes geometry and source material originating from Zoo/KCL tooling, together with downstream STEP snapshots and future FreeCAD-native work where required.

A 2026-08-08 proof-of-concept session created and exported a KCL design fork for a motor-under-lathe variant.

## Source Pattern

For the KCL-originated design and its motor-under-lathe fork:

```text
measurements / design intent
        |
        v
KCL source
        |
        v
Zoo execution
        |
        v
STEP review/interchange snapshot
        |
        v
FreeCAD downstream inspection / follow-on work
```

### Authority

- KCL is the authoritative parametric source for the KCL-originated variant.
- STEP is a downstream interchange/review snapshot.
- FreeCAD may inspect, reference, assemble, document, or derive from the STEP snapshot.
- Edits to imported FreeCAD solids do not automatically propagate back into KCL.

## Current Repository Structure

The current structure reflects the actual workflow that emerged from the proof of concept:

```text
cad/
├── AGENTS.md
├── tools/
│   └── cad-export
└── lathe_cabinet/
    ├── README.md
    ├── STATUS.md
    ├── main.step
    ├── demo-project.zip
    ├── demo-project/
    │   └── *.kcl
    └── motor-under-lathe/
        ├── README.md
        ├── main.kcl
        ├── parameters.kcl
        ├── motorEnvelope.kcl
        ├── motorShelf.kcl
        ├── driveChaseEnvelope.kcl
        ├── topDeck.kcl
        ├── butcherBlock.kcl
        ├── ...supporting KCL...
        └── exports/
            └── output.step
```

This tree is descriptive of the current working pattern. Additional files may be added as the project develops.

## Repository Layout Principle

For KCL-originated projects, prefer **design-lineage locality** over format-based segregation:

- keep an upstream/original project intact when doing so preserves provenance;
- keep a design fork or variant self-contained beneath its owning project;
- keep generated outputs close to the source project that generated them;
- place shared CAD workflow tools under `cad/tools/`;
- introduce a dedicated FreeCAD subdirectory only when a substantial FreeCAD-native branch of work actually exists.

The earlier format-oriented directory example was illustrative rather than normative and is superseded here by the proven working structure.

## File Roles

For Zoo/KCL-originated designs:

- `.kcl` files are authoritative source/provenance material.
- generated `.step` files are review/interchange artifacts.
- `.FCStd` files are FreeCAD-native downstream working documents where FreeCAD-specific work is required.
- KCL source does not need to be embedded inside the FreeCAD document.

Generated exports must not become the only surviving representation of authoritative geometry.

## Motor-Under-Lathe Variant Status

The current fork is a proof-of-concept, not a fabrication-ready design.

The source has passed a static local import check, has been executed by Zoo, and has produced a validated STEP snapshot through the repeatable `cad/tools/cad-export` wrapper. The fork still needs:

- FreeCAD import and visual/geometric validation
- replacement of provisional motor/drive dimensions with measured hardware dimensions
- structural, guarding, cooling, swarf-exclusion, electrical-routing, and service-access review

See:

`docs/cad/toolchain/checkpoints/cad-mcp-poc-2026-08-08.md`

## Toolchain Relationship

Current CAD architecture:

`docs/architecture/cad-toolchain-v0.2.md`

General CAD startup and continuity procedure:

`docs/cad/toolchain/codex-mcp-startup-continuity-v0.1.md`

MCP runbook:

`docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`

CAD toolchain thread:

`docs/thread-inits/MS-CAD-002-cad-toolchain-parametric-modeling-infrastructure.md`

## Status Discipline

Project-specific status and exact next actions should be maintained in `STATUS.md` as work progresses.

Git history is authoritative for committed file changes; interactive Codex/MCP session history is supplemental.
