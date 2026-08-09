# Motor-under-lathe cabinet fork

This project forks `../demo-project` and reserves space for a belt-driven motor
inside the cabinet beneath the lathe. The original project is unchanged.

## Default reference geometry

- Motor envelope: 15 × 12 × 12 in
- Motor position: X = 12 in from the left end, centered front-to-rear
- Motor mounting surface: Z = 9.5 in
- Belt/service chase: 4 × 10 in through the top deck and butcher block
- Motor shelf: doubled 3/4 in plywood, 24 × 20 in

Edit the motor and chase values in `parameters.kcl` after measuring the actual
motor, mount, shaft center, pulley/guard, and belt travel. The translucent motor
and chase bodies are keep-out references, not fabricated parts.

## Export

From the `cad` repository root, export and validate a deterministic STEP file:

```sh
tools/cad-export
```

The result is written to `exports/output.step` in this project. Pass another
KCL project and optional output directory to export a different model; run
`tools/cad-export --help` for details.

## Fabrication notes

- Add framing/cleats on both chase edges and keep mounting bolts clear.
- The tray remains continuous in CAD. Cut and flash a guarded, swarf-resistant
  penetration to the final belt guard; do not leave an unguarded slot.
- Provide a removable front guard/door, ventilation, electrical strain relief,
  grounding, and belt-tension access.
- The central caster keep-out is reduced and moved right; verify balance.
- Validate cooling, guarding, shelf deflection, fasteners, and center of gravity
  before fabrication. This is a layout model, not a stamped safety design.
