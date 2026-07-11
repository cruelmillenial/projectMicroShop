# Project Checkpoint — iGaging SPC Interface Reverse Engineering

**Date:** 2026-07-10  
**Subsystem:** MS-ELC-001 — iGaging SPC / DIY Data Interface  
**Status:** Blocked pending reliable electronics workstation infrastructure

## Objective

Interface an iGaging digital caliper with a microcontroller by characterizing its SPC output protocol.

## Hardware

### Caliper

- iGaging digital caliper
- 5-pin SPC connector
- Physically compatible with Mitutoyo Type-F cable

### Cable and Continuity Mapping

| Caliper side | Cable conductor |
|---|---|
| M9 | F5 |
| M8 | F3 |
| M7 | F1 |
| J4 | F4 |
| J3 | F2 |

Where:

- `M` = Mitutoyo connector side
- `J` = caliper PCB side

## Voltage Measurements

Ground reference: `J4`

| Pin | Voltage |
|---|---|
| M9 | approximately 2.9–3.0 V |
| M8 | approximately 0 V |
| M7 | near 0 V |
| J3 | near 0 V |

Measurements were repeatable.

## Oscilloscope Investigation

Instrument: FNIRSI 2C53T

With probe ground on `J4` and probe tip on `M9`, a waveform was observed.

Observed behavior:

- jaw movement changed the waveform
- pressing `mm/in` caused a visible disturbance
- waveform activity appeared continuous

Alternative reference combinations caused the signal to disappear, suggesting either an incorrect reference, loading, or connection sensitivity.

## Logic Analyzer

Analyzer:

- Lakeview Research Saleae-compatible clone
- USB ID: `0925:3881`
- Host: Ubuntu 24.04

After installation of the required sigrok firmware package, PulseView firmware errors disappeared and the analyzer operated.

Approximate channel mapping:

| Logic analyzer channel | Caliper pin |
|---|---|
| D0 | M9 |
| D2 | M8 |
| D4 | M7 |
| D1 | J4 |
| D3 | J3 |

This mapping requires one final confirmation.

## Captures and Observations

### Earlier known-good state

- D0 showed repetitive pulse activity.
- Other enabled channels remained flat.
- Jaw movement changed pulse spacing.
- Pressing `mm/in` produced a localized disturbance.

### Latest state

- D0 later stopped showing activity.
- Continuity testing did not reveal an obvious broken feeder or poor connection.
- The measurement chain became unreliable before protocol characterization was complete.

## Confirmed Findings

- The caliper and cable can produce observable activity on the M9/D0 path.
- The analyzer was previously detected and functional under Ubuntu/PulseView.
- Jaw motion and unit switching affected the observed signal.
- M9 measures approximately 3 V with a DMM while also having shown digital activity.

## Current Unknowns

- whether the logic analyzer remains reliable
- whether the M9/D0 signal can be reproduced consistently
- whether a second protocol line exists
- whether the interface is open-collector or otherwise requires biasing
- whether the protocol is single-wire, multiplexed, host-requested, or multi-wire
- whether any cable behavior is contributing to the observation

## Hypothesis Handling

The leading hypothesis is that M9 may carry an encoded or clocked digital signal with a pull-up, but the available evidence is not sufficient to conclude that the interface is definitively single-wire.

The immediate task is not protocol decoding. The immediate task is restoring confidence in the instrumentation chain.

## Resume Point

1. Re-establish a stable electronics bench setup.
2. Validate the logic analyzer against a known-good signal source.
3. Confirm analyzer channel continuity and channel-to-pin mapping.
4. Reproduce D0 activity from the caliper.
5. Capture all conductors simultaneously.
6. Record power-on, idle, movement, unit-change, and button-event captures.
7. Measure pulse widths and repetition intervals.
8. Determine whether another conductor is input-only or requires host stimulation.
9. Only then resume framing and encoding analysis.

## Dependency

This subsystem depends on the milestone:

**Electronics Workstation Operational**

The project is paused until the workstation provides a reliable, repeatable measurement environment.
