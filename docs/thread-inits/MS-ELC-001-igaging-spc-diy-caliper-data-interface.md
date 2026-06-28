# THREAD INIT: iGaging SPC / DIY Caliper Data Interface

## Purpose

This thread is for a later electronics project: building a DIY data interface for an iGaging caliper with an SPC/USB-labeled data port.

This is not urgent. It is not part of the immediate crane measurement mission.

## Project Context

The proprietary iGaging SPC/USB interface cable or control box appears scarce, overpriced, or possibly unavailable from trustworthy sources.

The user may already have a physically compatible connector in leftover data center, mining, computer, or electronics cable junk.

The goal is to avoid buying an overpriced proprietary device if the protocol can be mapped and read with ordinary tools.

## Desired End State

A small adapter that does this:

caliper data port to microcontroller to USB keyboard or serial output to spreadsheet or CSV

Preferred user experience:

- open LibreOffice Calc or a CSV logger
- measure with caliper
- press a button
- current caliper value is typed into the active cell
- optionally send Tab or Enter after the value

## Important Assumptions

Do not assume the port is real USB.

Do not plug a random cable from the caliper port directly into a computer.

Treat the port as unknown low-voltage measurement data output until proven otherwise.

Sniff first. Drive lines later.

## Likely Protocol Families

Possible cases include:

- Mitutoyo-style SPC or Digimatic-like request, clock, data, ground
- iGaging or cheap-DRO 21-bit or 24-bit clocked protocol
- micro-USB-shaped connector carrying non-USB signals
- some proprietary variant that still can likely be decoded with a logic analyzer

## Tooling Likely Needed

- physically compatible connector or sacrificial cable
- multimeter
- handheld oscilloscope
- USB logic analyzer
- 3.3 V USB-capable microcontroller
- RP2040, SAMD21, Teensy, or similar
- resistors for pullups, pulldowns, dividers, or protection
- jumper wires
- strain relief
- small enclosure later

## Safe Mapping Procedure

1. Identify the physical connector.
2. Remove caliper battery before test-fitting unknown plugs.
3. Find or make a breakout cable.
4. Label connector contacts by position, not assumed function.
5. Install battery and use multimeter to identify ground and voltage rails.
6. Use handheld scope to inspect idle voltage, pulses, and clock-like behavior.
7. Use logic analyzer to capture all candidate lines.
8. Test captures at zero, known inch values, known metric values, negative values, and unit changes.
9. Identify packet structure, bit order, sign, scale, and unit behavior.
10. Only then write microcontroller firmware.

## Microcontroller Output Target

First version should be boring:

- read caliper
- convert to displayed decimal value if needed
- type the value as USB HID keyboard text
- optionally type Tab or Enter

Do not start with a complex GUI, database, wireless link, or FreeCAD integration.

## First Task

Define the minimum viable protocol-mapping kit and step-by-step safe probing workflow, starting from connector identification and ending at a USB keyboard wedge prototype.
