# CAD MCP Proof-of-Concept Checkpoint — 2026-08-08

## Classification

**Type:** Toolchain / workflow checkpoint  
**Scope:** MS-CAD-002 — CAD Toolchain + Parametric Modeling Infrastructure  
**Status:** KCL editing, project restructuring, Zoo execution, and STEP export complete; FreeCAD validation pending

## Purpose

Record a proof-of-concept workflow in which Codex can inspect and revise a code-based KCL design, prepare it for export through Zoo, and hand resulting geometry to FreeCAD as STEP interchange geometry.

The demonstration target was the existing lathe cabinet project. A design fork was created to investigate placing the lathe motor beneath the machine, inside the cabinet.

## Source Material

The local CAD workspace contains an original lathe-cabinet design under:

```text
cad/lathe_cabinet/
```

Known source material includes:

- original STEP geometry
- archived Zoo/KCL source
- expanded multi-file KCL project

The original source was preserved before creating the design fork.

## Design Fork

The experimental motor-under-lathe variant is organized locally under:

```text
cad/lathe_cabinet/motor-under-lathe/
```

Principal source roles:

- `main.kcl` — revised cabinet assembly
- `parameters.kcl` — centralized cabinet, motor, shelf, chase, and keep-out dimensions
- `motorEnvelope.kcl` — translucent motor reference volume
- `motorShelf.kcl` — doubled plywood motor mounting pad
- `driveChaseEnvelope.kcl` — belt and service keep-out
- `topDeck.kcl` — segmented deck around the drive chase
- `butcherBlock.kcl` — segmented top layer around the drive chase
- `README.md` — variant assumptions and fabrication cautions

## Provisional Design Inputs

The following dimensions are placeholders for layout and workflow demonstration only:

- motor envelope: 15 × 12 × 12 in
- motor center: X = 12 in from the left end, Y = cabinet centerline
- motor mounting surface: Z = 9.5 in
- motor shelf: 24 × 20 × 1.5 in
- belt/service chase: 4 × 10 in
- chase aligned with the provisional motor center

These values must be replaced by measured hardware dimensions before fabrication decisions are made.

## Design Consequences Observed

The conceptual fork produced several useful integration observations:

- the motor mounting pad occupies the existing lower ballast-shelf region
- the original central caster/jack reservation conflicts with the provisional motor volume
- the mobility reservation was therefore reduced and shifted laterally in the experimental variant
- the top deck and butcher-block layers retain bridge material around the chase
- the chip tray remains continuous in the current conceptual model

Any physical implementation would require a guarded, flashed, swarf-resistant tray penetration matched to the final belt guard and drive geometry.

## Measurements Required Before Fabrication Use

Collect and record:

- motor body length, width, and height
- mounting-foot pattern and adjustment travel
- shaft diameter, direction, and center height
- motor pulley diameter and axial position
- spindle pulley position
- belt width, length, path, and tensioning travel
- belt-guard dimensions and service clearance
- cooling-air requirements
- electrical enclosure, disconnect, grounding, and cable-routing requirements
- actual caster or mobility-hardware envelope

The resulting design also requires review for:

- shelf deflection
- fastener loading
- cabinet balance and center of gravity
- vibration
- belt guarding
- service access

## Static Verification Completed

The session performed a static KCL source check:

- 17 KCL files were present in the fork
- all local KCL imports resolved to files in the project
- the assembly source references the motor shelf, motor keep-out, drive chase, and relocated mobility keep-out

Zoo subsequently executed the fork and produced a 193,003-byte STEP snapshot at
`cad/lathe_cabinet/motor-under-lathe/exports/output.step`. The snapshot has the
expected ISO-10303-21 header and trailer.

The remaining validation is to import the snapshot into FreeCAD, inspect the
geometry and clearances, and replace provisional drive dimensions with measured
hardware inputs.

## KCL → Zoo → FreeCAD Workflow

FreeCAD does not natively interpret KCL source.

The demonstrated toolchain model is:

```text
Codex edits KCL source
        |
        v
Zoo CLI executes KCL and exports STEP
        |
        v
FreeCAD imports STEP snapshot
```

### Source-of-Truth Rule

For a KCL-originated build:

- KCL remains the authoritative parametric source
- Zoo execution produces downstream geometry
- STEP is the interchange snapshot
- FreeCAD may inspect, reference, assemble, document, or derive from that snapshot
- edits to imported FreeCAD solids do not automatically flow back into KCL

This is a distinct workflow from FreeCAD-native projects in which FCStd is the primary parametric source.

## Zoo CLI Operating Model

The preferred proof-of-concept arrangement is a workspace-local executable:

```text
.tools/bin/zoo
```

Reasons:

- avoids reliance on mutable global `PATH`
- makes the expected tool location explicit to automation
- reduces ambiguity between CLI versions

Before use:

- verify the published checksum for the selected Zoo CLI release
- authenticate without committing credentials
- treat hosted KCL execution/export as network-dependent

Authentication may use an interactive login or securely injected token. Credentials must not enter the repository.

Representative export shape:

```bash
.tools/bin/zoo kcl export \
  --output-format=step \
  cad/lathe_cabinet/motor-under-lathe \
  cad/lathe_cabinet/motor-under-lathe/exports
```

Exact CLI syntax must be verified against the installed Zoo CLI version before the command is standardized.

## Repository Wrapper

Implemented at:

```text
tools/cad-export
```

Current behavior:

1. Resolve KCL project and output directories.
2. Refuse unsafe or unrelated overwrites.
3. Invoke the workspace-local Zoo CLI.
4. Request deterministic STEP output where supported.
5. Surface KCL execution errors clearly.
6. Verify that STEP output exists and is nonempty.
7. Optionally retain named or timestamped variants.
8. Optionally call `FreeCADCmd` for a headless STEP import check.

Items 1–6 are implemented. Named history and a headless FreeCAD check remain
optional extensions.

## Codex / MCP Continuity Model

The repository remains the durable project memory.

Useful repository-local continuity artifacts include:

- `AGENTS.md` — standing CAD/toolchain instructions
- project `README.md` — stable project definition and file roles
- project `STATUS.md` — current handoff state and exact next actions

Codex conversation history is supplemental rather than canonical.

A meaningful working session should end by updating the project status record before closure.

## Relationship to FreeCAD MCP

The FreeCAD MCP bridge remains valuable for:

- inspecting imported STEP geometry
- querying document and object structure
- manipulating FreeCAD-native follow-on geometry
- validating exports
- reducing repetitive GUI work

It is not required to become the source of truth for a KCL-first design.

The validated FreeCAD/MCP compatibility stack remains documented separately in:

`docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`

## Suggested Resume Sequence

1. Install a verified Zoo CLI binary at the workspace-local tool path.
2. Authenticate without storing credentials in the repository.
3. Record the installed Zoo CLI version.
4. Run a minimal authenticated check.
5. Export the motor-under-lathe fork to STEP.
6. Resolve KCL parser or geometry errors.
7. Import the generated STEP into FreeCAD.
8. Perform visual and geometric inspection.
9. Replace provisional motor and belt dimensions with measurements.
10. Re-export and review clearances, guarding, structure, and service access.
11. Add `tools/cad-export` after the manual path is repeatable.

## PM / Toolchain Impact

This PoC establishes that Project MicroShop may support at least two legitimate parametric-source patterns:

```text
FreeCAD-native:
measurements/parameters → FCStd → exports

KCL-first:
measurements/parameters → KCL → Zoo execution → STEP → FreeCAD downstream use
```

The CAD architecture and repository standards should therefore describe the **authoritative parametric source** generically rather than assuming FCStd is always upstream of interchange geometry.

## Current Status

**Code-based fork:** present locally  
**Static import check:** passed  
**Zoo execution:** passed
**STEP export of fork:** passed
**FreeCAD visual/geometric validation:** pending
**Measured motor/drive inputs:** pending

The next meaningful toolchain milestone is FreeCAD import and visual/geometric validation.