# Project MicroShop — Shop Wall

## Purpose

The Shop Wall preserves short remarks, accidental one-liners, aphorisms, and bits of project philosophy that are worth retaining but are not engineering doctrine.

Entries here may point toward useful architectural ideas, but they do not become requirements or specifications merely by appearing here. When an entry has technical implications, the relevant engineering artifact should carry the actual design context.

---

## Downloadable Body Parts

> “Eventually you could have something amusingly close to a machine accessory API:
> `AuxSpindleCarrier(tool_profile, machine_interface, axis_height, orientation, offset)`
> At which point the lathe starts accumulating downloadable body parts.”

**Context:** Discussion of a modular auxiliary-spindle carrier for the South Bend 9x36 lathe.

The useful idea behind the line is to treat a machine tool as a stable physical platform with measured interfaces and explicit datums. A reusable accessory architecture can then separate the machine-specific interface from the payload-specific profile and positioning parameters.

In conceptual form:

```text
physical machine
    ↓
measured machine definition
    ↓
standardized machine interface
    ↓
parametric accessory family
    ↓
generated fabrication geometry
```

The current auxiliary-spindle concept is an early test of this idea. The project should not prematurely declare a formal accessory API; repeated successful use across multiple payloads and machine accessories should be allowed to reveal which abstractions are actually durable.

See: `cad/concepts/south_bend_9x36/compound_auxiliary_spindle/PREPARAMETRIC.md`
