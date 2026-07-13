# Internal Control Meta v0.1

## Purpose

Project MicroShop requires a lightweight internal-control layer that can describe whether an element merely exists or has become dependable operational capability.

The first implementation is the process-code schema defined in:

`docs/standards/process-code-schema-v0.1.md`

This architecture note explains how that schema fits into the wider project.

## Control Problem

Workshop development produces many misleading intermediate states:

- a tool has been purchased but has no assigned place
- a fixture works once but is unsafe or awkward
- a workstation is assembled but has not been used in the real workflow
- a procedure exists but is not repeatable
- a subsystem worked previously but is no longer maintained

Simple task states such as `open`, `in progress`, and `done` do not express these differences well.

The process codes therefore track maturation of individual elements while milestones track capability unlocks.

## Two-Level Model

### Milestones

Milestones describe operational outcomes.

They answer:

> What can Project MicroShop now do that it could not reliably do before?

Examples:

- Electronics Workstation Operational
- Precision Metrology Operational
- Heavy Mechanical Infrastructure Operational

### Process Codes

Process codes describe the maturity of contributing elements.

They answer:

> What evidence exists that this element has progressed from concept through integration, workflow use, standardization, and sustained control?

A milestone may contain dependencies at several different process-code states.

## Internal-Control Use

The process-code schema may support:

- milestone definitions of done
- workstation readiness reviews
- 6S audits
- visual labels
- maintenance planning
- project checkpoints
- issue triage
- identification of incomplete integration
- distinction between temporary prototypes and standard work

## Non-Goals

The schema is not intended to:

- replace GitHub issue state
- replace priority or scheduling
- measure labor hours
- claim percentage completion
- force all work into one chronological phase
- imply that every item must reach η

## Evidence Model

An assigned code should be tied to observable evidence where practical.

Examples:

| Element | Code | Evidence |
|---|---:|---|
| bench frame | ζ | dimensioned design, installed structure, labeled interfaces |
| logic analyzer setup | ε | validated against known-good waveform and used in a real capture |
| maintenance procedure | α | need identified, no procedure yet |
| mobile tool kit | δ | assigned carrier and contents, field workflow not yet tested |

The control value comes from the evidence, not the symbol alone.

## Regression

Codes may move backward.

Examples:

- a redesign can return a ζ fixture to β or γ
- moving equipment can invalidate δ placement and ε workflow evidence
- missing labels or obsolete instructions can reduce ζ confidence
- failure to sustain audits means η no longer applies

Regression is not necessarily failure. It is a truthful representation of changed control conditions.

## Relationship to 6S

The process-code schema is broader than 6S but can make 6S work more explicit.

- Sort may reveal elements that should be retired or removed.
- Set in Order commonly advances storage and placement toward δ.
- Shine and safety work often contribute to γ.
- Standardize is strongly associated with ζ.
- Sustain is represented by η.

The mapping is not exact, and process codes should not be treated as renamed 6S steps.

## Audit Model

Future audit procedures may inspect:

- whether assigned codes remain defensible
- whether required evidence exists
- whether milestone dependencies satisfy their minimum states
- whether ζ controls remain current
- whether η maintenance loops are actually operating
- whether regression or corrective action is required

Audits should sample the integrity of the control system rather than reward inflated code assignments.

## Evolution

This is an early internal-control meta, not a finished management system.

The MS-OPS-001 thread should test it against real MicroShop cases and determine whether the project needs:

- orthogonal status modifiers
- code-assignment templates
- machine-readable metadata
- repository automation
- visual placards or labels
- periodic integrity audits

Changes should remain proportional to the value they provide. The control system must not become more burdensome than the work it is intended to clarify.
