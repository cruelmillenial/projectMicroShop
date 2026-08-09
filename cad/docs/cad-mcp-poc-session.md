# CAD MCP PoC session handoff

Date: 2026-08-08
Workspace: `/home/control/src/projectMicroShop/cad`

## Purpose

This session explored a proof-of-concept CAD workbench in which Codex can inspect
and revise a code-based KCL design, export the resulting geometry through Zoo,
and hand the model to FreeCAD as STEP geometry.

The demonstration target was the existing lathe cabinet. A separate design fork
was created to investigate placing the lathe motor directly beneath the machine,
inside the cabinet.

## Source material found

The original lathe cabinet material is under `lathe_cabinet/` and includes:

- `lathe_cabinet/main.step`
- `lathe_cabinet/demo-project.zip`
- `lathe_cabinet/demo-project/`, containing the multi-file KCL project

The original `demo-project` was preserved.

## Design fork created

The motor-under-lathe variant is located at:

`lathe_cabinet/motor-under-lathe/`

Principal files:

- `main.kcl` — revised cabinet assembly
- `parameters.kcl` — centralized cabinet, motor, shelf, chase, and keep-out dimensions
- `motorEnvelope.kcl` — translucent reference volume for the motor
- `motorShelf.kcl` — doubled plywood motor mounting pad
- `driveChaseEnvelope.kcl` — translucent belt and service keep-out
- `topDeck.kcl` — four-piece deck surrounding a rectangular chase
- `butcherBlock.kcl` — four-piece top layer surrounding the same chase
- `README.md` — variant-specific assumptions and fabrication cautions

## Provisional design assumptions

The motor and drive dimensions are placeholders for layout and demonstration.
They must be replaced with measured hardware dimensions before fabrication.

- Motor envelope: 15 × 12 × 12 in
- Motor center: X = 12 in from the left end, Y = cabinet centerline
- Motor mounting surface: Z = 9.5 in
- Motor shelf: 24 × 20 × 1.5 in
- Belt/service chase: 4 × 10 in
- Chase location: aligned with the provisional motor center

The motor mounting pad sits on the existing lower ballast shelf. The original
central caster/jack reservation conflicted with the new motor volume, so the
variant reduces that reservation and moves it toward the right side.

The top deck and butcher block retain front and rear bridge material around the
rectangular chase. The metal chip tray is still continuous in the CAD model. A
real implementation would require a guarded, flashed, swarf-resistant tray
penetration matched to the final belt guard.

## Required measurements

Before treating the variant as a fabrication design, collect:

- Motor body length, width, and height
- Motor mounting-foot pattern and adjustment travel
- Motor shaft diameter, axis direction, and center height
- Motor pulley diameter and axial position
- Lathe spindle pulley position
- Belt width, length, operating path, and tensioning travel
- Belt-guard dimensions and service clearance
- Cooling-air requirements
- Electrical enclosure, disconnect, grounding, and cable-routing requirements
- Actual caster or mobility-hardware envelope

The resulting design should also be checked for shelf deflection, fastener loads,
cabinet balance, center of gravity, vibration, belt guarding, and service access.

## Verification completed

A static source check found 17 KCL files in the fork and confirmed that every
local KCL import resolves to a file in the project. The assembly includes the
motor shelf, motor keep-out, drive chase, and relocated mobility keep-out.

The fork was subsequently executed by Zoo and exported successfully. The
resulting `lathe_cabinet/motor-under-lathe/exports/output.step` is a nonempty
STEP file with a valid ISO-10303-21 header and trailer. The repository wrapper
at `tools/cad-export` captures the proven deterministic export command and
performs basic output validation.

Visual inspection and geometric validation in FreeCAD remain outstanding.

## KCL, Zoo, and FreeCAD workflow

FreeCAD does not natively interpret KCL source. The intended bridge is:

```text
Codex edits KCL
      ↓
Zoo CLI executes KCL and exports STEP
      ↓
FreeCAD imports the STEP snapshot
```

The STEP model is downstream geometry. Parametric design changes should remain
in KCL and be re-exported; edits made to the imported FreeCAD solid do not flow
back into the KCL project automatically.

The existing `lathe_cabinet/main.step` can already be opened in FreeCAD, but it
represents the original design rather than the motor-under-lathe fork.

## Zoo CLI setup

Zoo distributes its CLI as a standalone binary for Linux, macOS, and Windows.
For this PoC, the preferred arrangement is a workspace-local executable:

```text
.tools/bin/zoo
```

This avoids relying on a mutable global `PATH`. Verify the checksum published
with the selected Zoo CLI release before running the binary.

Authentication can use either:

```bash
zoo auth login
```

or a securely injected `ZOO_API_TOKEN`. Tokens must not be committed to this
repository. KCL execution and export use Zoo's hosted service, so outbound
network access and possibly a one-time Codex command approval are required.

Expected export command:

```bash
.tools/bin/zoo kcl export \
  --output-format=step \
  lathe_cabinet/motor-under-lathe \
  lathe_cabinet/motor-under-lathe/exports
```

## Proposed semi-automatic integration

Add a repository wrapper such as:

```text
tools/cad-export
```

The wrapper should:

1. Resolve the KCL project and output directory.
2. Refuse to overwrite unrelated output.
3. Invoke the workspace-local Zoo CLI.
4. Request deterministic STEP output if supported by the installed CLI.
5. Report KCL execution errors clearly.
6. Verify that the resulting STEP exists and is nonempty.
7. Optionally retain timestamped or named variants.
8. Optionally use `FreeCADCmd` for a headless STEP import check.

This command could later be described by a Codex skill so requests such as
“export and verify the motor-under-lathe variant” follow a repeatable workflow.
A Zoo MCP server is another possible integration, but the CLI wrapper is the
simplest transparent PoC because each operation remains reproducible in a shell.

Launching the interactive FreeCAD GUI is a separate desktop action and may still
require explicit permission. Headless checking with `FreeCADCmd`, if installed,
is more suitable for automation.

## Suggested resume sequence

1. Open the generated STEP in FreeCAD and visually inspect the assembly.
2. Record any geometry, placement, or clearance defects.
3. Replace the provisional motor and belt dimensions with measurements.
4. Re-export and review clearances, guarding, structure, and service access.
5. Add an optional headless FreeCAD import check to `tools/cad-export` if useful.

## Current status

The code-based design fork, documentation, repeatable export wrapper, and first
STEP export are present. The original design is preserved. The next meaningful
milestone is FreeCAD inspection followed by replacement of provisional drive
dimensions with measured hardware data.
