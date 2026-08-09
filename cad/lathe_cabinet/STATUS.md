# Lathe Cabinet CAD Status

Updated: 2026-08-08

## Current state

- The original KCL project and STEP export are preserved.
- `motor-under-lathe/` is an experimental KCL fork; KCL is its authoritative
  parametric source.
- Zoo executed the fork successfully and produced
  `motor-under-lathe/exports/output.step`.
- `tools/cad-export` provides the repeatable deterministic STEP export path and
  validates the basic STEP envelope before replacing the prior snapshot.
- The motor, drive chase, shelf, and mobility-clearance dimensions are still
  provisional and must not be used for fabrication.

## Completed verification

- All local KCL imports resolve.
- The variant assembly includes the motor shelf, motor envelope, drive chase,
  and relocated mobility keep-out.
- The generated STEP is nonempty and has the expected ISO-10303-21 header and
  trailer.

## Next actions

1. Import `motor-under-lathe/exports/output.step` into FreeCAD.
2. Visually inspect object placement, intersections, chase geometry, and overall
   assembly integrity.
3. Record the actual motor, mount, shaft, pulleys, belt, guard, ventilation,
   electrical, and mobility-hardware dimensions.
4. Replace provisional values in `motor-under-lathe/parameters.kcl`.
5. Re-export and review structural support, balance, guarding, cooling, swarf
   exclusion, and service access before any fabrication decision.

## Source-of-truth boundary

KCL source is authoritative for this variant. STEP is a review/interchange
snapshot, and downstream FreeCAD edits do not flow back into KCL.
