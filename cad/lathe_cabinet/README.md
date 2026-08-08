# Lathe Cabinet CAD Workspace

## Purpose

This directory contains the CAD project for the lathe cabinet / stand build.

The local working tree has been reorganized so project-specific CAD files reside under:

```text
cad/lathe_cabinet/
```

## Design Origin

The project includes geometry and source material originating from Zoo/KCL tooling and may also contain FreeCAD-native working files and interchange exports.

## File Roles

Recommended organization:

```text
cad/lathe_cabinet/
├── README.md
├── STATUS.md
├── source-zoo/
│   └── *.kcl
├── interchange/
│   └── *.step
├── freecad/
│   └── *.FCStd
└── exports/
```

Exact filenames may differ from this template. The important distinction is between source/provenance material, interchange geometry, FreeCAD-native working documents, and generated outputs.

## Source-of-Truth Rules

- KCL source remains provenance/source material when the design originates in Zoo.
- STEP is an interchange artifact, not the preferred long-term editable source.
- FCStd is the FreeCAD-side working document once active FreeCAD development begins.
- Generated exports must not become the only surviving representation of authoritative geometry.
- Preserve enough source context to understand how imported geometry was produced.

## Toolchain Relationship

General CAD startup and continuity procedure:

`docs/cad/toolchain/codex-mcp-startup-continuity-v0.1.md`

MCP runbook:

`docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`

CAD toolchain thread:

`docs/thread-inits/MS-CAD-002-cad-toolchain-parametric-modeling-infrastructure.md`

## Status

The project directory exists in the local repository and project files have been moved into it. Project-specific status and next actions should be recorded in `STATUS.md` as the build progresses.
