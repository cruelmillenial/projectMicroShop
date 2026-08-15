# CAD Concept Seeds

This directory contains pre-parametric design seeds intended for Codex / FreeCAD MCP work before a concept has matured into an active build-specific CAD project.

## Role

A concept seed captures design intent, parameter families, datums, constraints, validation requirements, and expected outputs without pretending that unmeasured machine interfaces or provisional geometry are final.

These files are inputs to CAD work, not fabrication drawings.

## Promotion path

```text
pre-parametric seed
        ↓
Codex / FreeCAD rough parametric model
        ↓
measurement reconciliation
        ↓
validated CAD project
        ↓
fabrication / inspection package when justified
```

When a seed becomes active, preserve the original seed and create the working CAD project beside or beneath it rather than silently rewriting the historical brief.

## Current South Bend 9x36 seeds

- `south_bend_9x36/spindle_fly_cutter/PREPARAMETRIC.md` — compact directly spindle-mounted single-point facing cutter.
- `south_bend_9x36/compound_auxiliary_spindle/PREPARAMETRIC.md` — modular compound/toolpost-mounted high-speed auxiliary spindle carrier.
- `south_bend_9x36/tm010_resonant_cavity/PREPARAMETRIC.md` — approximately 2.45 GHz cylindrical TM010 resonant-cavity manufacturing demonstrator.

The first two are machine accessories. The cavity seed is a manufacturing demonstrator whose geometry is intentionally chosen to exercise the South Bend, metrology workflow, and later RF measurement loop.

## Doctrine

- Do not freeze machine-interface dimensions without measurement.
- Keep theoretical, nominal, measured, and corrected values distinct.
- Preserve source-of-truth relationships defined by MS-CAD-002.
- Reuse common machine-envelope, spindle-axis, datum, fastener, and workholding infrastructure where practical.
- Promote repeated geometry into the shared CAD library only after reuse is demonstrated.
