# iGaging SPC / DIY Data Interface

This subsystem covers an open, serviceable data interface for an iGaging caliper data port.

## Current Status

**State:** Blocked — Electronics Workstation Operational milestone

The most recent protocol captures became unreliable before characterization was complete. The immediate task is to restore confidence in the instrumentation chain, not to commit to a protocol hypothesis.

## Completed

- Connector and cable continuity mapped
- Voltage survey completed
- Oscilloscope activity observed on M9
- Logic analyzer detected and operated under Ubuntu/PulseView
- Digital activity previously observed on M9 / D0
- Jaw movement affected observed timing
- `mm/in` event affected the observed signal

## Outstanding

- Validate the logic analyzer against a known-good signal source
- Verify complete channel mapping
- Restore repeatable D0 captures
- Capture all conductors simultaneously
- Determine whether additional protocol lines exist
- Characterize pulse timing, framing, and encoding
- Produce a protocol specification
- Implement serial and USB HID prototypes

## Current Direction

- Treat the port as an unknown low-voltage digital interface until measured.
- Do not assume USB signaling.
- Do not assume electrical compatibility from connector fit alone.
- Use passive observation before driving any signal lines.
- Do not conclude single-wire operation until alternate explanations are excluded.
- Initial output target: USB HID keyboard wedge.
- Long-term field target: Android via USB-C OTG.

## Documents

- `architecture-v0.1.md` — first architecture snapshot
- `checkpoints/checkpoint-2026-07-10-reverse-engineering.md` — latest engineering checkpoint
- `../../decisions/ADR-0001-igaging-android-target-platform.md` — Android-first target platform decision
- `../../thread-inits/MS-ELC-001-igaging-spc-diy-caliper-data-interface.md` — original thread init

## Planned Folders

- `hardware/`
- `protocol-notes/`
- `firmware/`
- `captures/`
