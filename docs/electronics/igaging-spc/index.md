# iGaging SPC / DIY Data Interface

This subsystem covers an open, serviceable data interface for an iGaging caliper data port.

## Current Direction

- Treat the port as an unknown low-voltage digital interface until measured.
- Do not assume USB signaling.
- Do not assume electrical compatibility from connector fit alone.
- Use passive observation before driving any signal lines.
- Initial output target: USB HID keyboard wedge.
- Long-term field target: Android via USB-C OTG.

## Documents

- `architecture-v0.1.md` — first architecture snapshot
- `../../decisions/ADR-0001-igaging-android-target-platform.md` — Android-first target platform decision
- `../../thread-inits/MS-ELC-001-igaging-spc-diy-caliper-data-interface.md` — original thread init

## Future Folders

- `hardware/`
- `protocol-notes/`
- `firmware/`
- `captures/`
