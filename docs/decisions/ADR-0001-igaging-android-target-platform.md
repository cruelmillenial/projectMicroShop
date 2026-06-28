# ADR-0001 — iGaging Interface Target Platform Is Android-First

## Status

Accepted

## Context

The iGaging SPC / DIY Data Interface project needs a practical host target for the first usable field adapter.

The project began with a generic spreadsheet-output goal, but the mobile kit requirement changes the architecture. The adapter is expected to be useful away from a full desktop workstation.

The current architecture snapshot states that the long-term endpoint is Android, with desktop/laptop support treated primarily as a development path.

## Decision

The deployment target for the iGaging SPC / DIY Data Interface is Android-first.

Preferred host-output order:

1. USB HID keyboard via USB-C OTG
2. USB CDC serial
3. Bluetooth HID
4. BLE custom application

The MVP should prioritize a boring USB HID keyboard wedge that can type a measurement into the active input field of Android spreadsheet or logging software.

## Consequences

### Positive

- Supports mobile field measurement.
- Avoids dependence on Windows-specific software.
- Keeps the first prototype simple and host-agnostic.
- Works with spreadsheet-first workflows.
- Makes Android OTG compatibility an early test item rather than a late surprise.

### Negative / Constraints

- USB HID behavior must be tested against Android devices, not only development PCs.
- Enclosure and cable strain-relief choices should assume phone/tablet field use.
- Serial-only output is useful for validation but is not the primary user experience.
- Bluetooth and BLE are deferred until the wired workflow is proven.

## Related Documents

- `docs/electronics/igaging-spc/architecture-v0.1.md`
- `docs/thread-inits/MS-ELC-001-igaging-spc-diy-caliper-data-interface.md`
- GitHub issue: `MS-ELC-001: iGaging SPC / DIY Caliper Data Interface`
