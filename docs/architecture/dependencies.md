# Project MicroShop — Capability Dependencies

This document records cross-subsystem dependencies at the capability and milestone level.

## Current Dependency Chain

```text
Electronics Workstation Operational
        |
        v
MS-ELC-001 iGaging SPC Reverse Engineering
        |
        v
USB Serial Validation Prototype
        |
        v
USB HID Keyboard Wedge
        |
        v
Android Measurement Tool
```

## Interpretation

The iGaging SPC reverse-engineering task is not presently blocked by lack of protocol ideas. It is blocked by the absence of a reliable, repeatable electronics measurement environment.

The **Electronics Workstation Operational** milestone should be considered satisfied when the bench can support:

- stable instrument power and placement
- dependable grounding and probe access
- logic analyzer validation against a known-good source
- repeatable oscilloscope and logic captures
- secure cable and breakout retention
- documented channel mapping
- practical storage and setup without improvised rewiring

Once that milestone is reached, MS-ELC-001 may resume from the checkpoint documented in:

`docs/electronics/igaging-spc/checkpoints/checkpoint-2026-07-10-reverse-engineering.md`

## PM Doctrine

When multiple dependent tasks are blocked by the same missing capability, prioritize the shared capability milestone rather than continuing low-confidence workarounds in each dependent task.
