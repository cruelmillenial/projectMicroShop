# Lathe Cabinet CAD Workspace

## Purpose

This directory contains the CAD project for the lathe cabinet / stand build.

The local working tree has been reorganized so project-specific CAD files reside under:

```text
cad/lathe_cabinet/
```

## Design Origin

The project includes geometry and source material originating from Zoo/KCL tooling and may also contain FreeCAD-native working files and interchange exports.

A 2026-08-08 proof-of-concept session created a KCL design fork for a motor-under-lathe variant under the local project workspace.

## Current Local Source Pattern

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
STEP interchange snapshot
        |
        v
FreeCAD downstream inspection / follow-on work
```

### Authority

- KCL is the authoritative parametric source for the KCL-originated variant.
- STEP is a downstream interchange snapshot.
- FreeCAD may inspect, reference, assemble, document, or derive from the STEP snapshot.
- Edits to imported FreeCAD solids do not automatically propagate back into KCL.

## Known Local Project Material

The local working tree includes original lathe-cabinet material and an experimental fork.

Representative roles include:

```text
cad/lathe_cabinet/
├── README.md
├── STATUS.md
├── original KCL / Zoo source
├── original STEP geometry
├── motor-under-lathe/
│   ├── main.kcl
│   ├── parameters.kcl
│   ├── motorEnvelope.kcl
│   ├── motorShelf.kcl
│   ├── driveChaseEnvelope.kcl
│   ├── topDeck.kcl
│   ├── butcherBlock.kcl
│   ├── README.md
│   └── exports/
├── freecad/
└── exports/
```

Exact remote contents depend on what has been committed and pushed from the local working tree.

## File Roles

For Zoo/KCL-originated designs:

- `.kcl` files remain authoritative source/provenance material.
- generated `.step` files are geometry interchange artifacts.
- `.FCStd` files are FreeCAD-native downstream working documents where FreeCAD-specific work is required.
- KCL source does not need to be embedded inside the FreeCAD document.

Generated exports must not become the only surviving representation of authoritative geometry.

## Motor-Under-Lathe Variant Status

The current fork is a proof-of-concept, not a fabrication-ready design.

The source has passed a static local import check and has been executed by Zoo.
A repeatable wrapper produced a validated STEP snapshot. The fork still needs:

- FreeCAD import and visual validation
- replacement of provisional motor/drive dimensions with measured hardware dimensions
- structural, guarding, cooling, swarf-exclusion, and service-access review

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
