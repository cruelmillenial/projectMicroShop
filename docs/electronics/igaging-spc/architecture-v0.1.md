# Project Update — iGaging SPC / DIY Data Interface

**Status:** Planning / Architecture

## Objective

Develop an open, serviceable replacement for the proprietary iGaging data interface capable of exporting caliper measurements directly into modern software without relying on scarce or expensive vendor hardware.

The project explicitly prioritizes protocol discovery over assumptions about connector or signaling.

---

# Updated Hardware Assumptions

## Connector

Current evidence strongly suggests the caliper uses a **Mitutoyo Type F** mechanical connector.

Ordered for investigation:

* Mitutoyo **905338 SPC Digimatic Data Cable**
* Type F connector
* 1 meter
* Straight plug

This cable will primarily serve as:

* a mechanically compatible connector
* a breakout candidate
* a sacrificial reverse-engineering cable if necessary

**Important**

Mechanical compatibility **does not imply electrical compatibility.**

Until captures are obtained, the interface will be treated as an unknown low-voltage digital protocol.

No assumptions will be made regarding:

* USB signaling
* Digimatic packet format
* voltage levels
* pin functions
* clock direction

---

# Reverse Engineering Philosophy

The interface will be treated as an unknown embedded bus.

Workflow:

1. identify connector
2. map pins
3. identify ground
4. identify supply rails
5. observe idle voltages
6. observe activity with oscilloscope
7. capture with logic analyzer
8. decode protocol
9. implement firmware

No signal lines are to be driven until passive observation is complete.

---

# Development Phases

## Phase 0

Hardware acquisition

* connector
* breakout
* logic analyzer
* handheld oscilloscope
* RP2040-class microcontroller

---

## Phase 1

Electrical characterization

Deliverables:

* pinout
* voltage map
* timing captures
* packet captures

---

## Phase 2

Protocol decoding

Deliverables:

* packet format
* bit order
* sign encoding
* scale
* unit handling
* transmission timing

---

## Phase 3

USB serial prototype

Firmware outputs decoded measurements over USB serial for validation.

---

## Phase 4

USB HID keyboard wedge

Button press results in:

```
12.345<Tab>
```

or

```
12.345<Enter>
```

This validates decoding independently of any custom software.

---

## Phase 5

Android field integration

The long-term endpoint is **Android**, not Windows.

Preferred priority:

1. USB HID keyboard via USB-C OTG
2. USB CDC serial
3. Bluetooth HID
4. BLE custom application

The project should assume mobile operation from this point forward.

Laptop support exists primarily as a development environment.

---

# Design Goals

The finished adapter should:

* fit in a pocket
* require minimal setup
* operate from USB power
* survive field use
* avoid proprietary software
* work with LibreOffice Calc
* work with Google Sheets
* work with generic CSV logging applications
* remain fully open and reproducible

---

# Non-Goals (MVP)

The initial implementation intentionally excludes:

* Wi-Fi
* cloud synchronization
* databases
* FreeCAD integration
* statistical process control software
* wireless networking
* touchscreen interfaces
* complex GUIs

The first successful prototype should perform one task only:

> Read the current caliper measurement and inject it reliably into the active input field on a host device.

Everything beyond that is considered future expansion.

---

# Success Criteria

The MVP is considered complete when a user can:

1. Connect the adapter to an Android device (or development PC).
2. Measure a part.
3. Press a single button.
4. Observe the current measurement automatically entered into the active spreadsheet cell or text field.

The solution should be inexpensive, repairable, protocol-documented, and independent of proprietary vendor hardware.
