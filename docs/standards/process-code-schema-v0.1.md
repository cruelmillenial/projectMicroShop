# Process Code Schema v0.1

## Status

Early working standard for Project MicroShop internal control.

This schema is intentionally provisional. Revisions should preserve a clear version history rather than silently changing the meaning of previously assigned codes.

## Purpose

The process-code schema provides a compact way to describe how far an element has progressed from idea to maintained operational capability.

It may be applied to:

- tools
- fixtures
- workstations
- storage systems
- procedures
- software
- documentation
- shared infrastructure
- milestone dependencies

The codes are not project phases. Different elements may advance independently and may hold different codes at the same time.

## Canonical Codes

### α — Concept Identified

The need, use case, or intended function has been identified.

Typical evidence:

- problem statement
- rough requirement
- candidate concept
- initial scope note

An α item is not yet expected to function.

### β — Functional Blank

A first crude, provisional, or minimally functional implementation exists.

Typical evidence:

- rough prototype
- unrefined tool or fixture
- temporary mounting
- first working script
- proof-of-concept procedure

A β item may function, but should not be mistaken for a safe, integrated, or repeatable solution.

### γ — Clean and Safe Enough to Continue

The item has been cleaned up, deburred, insulated, guarded, strain-relieved, or otherwise made reasonably safe for continued handling and development.

Typical evidence:

- sharp edges removed
- obvious hazards corrected
- temporary wiring secured
- basic protective measures added
- gross contamination or clutter removed

γ does not prove workflow suitability.

### δ — Locally Integrated

The item has been mounted, placed, connected, or incorporated into its intended local system.

Typical evidence:

- permanent or controlled mounting
- assigned storage location
- service connections established
- interface fit verified
- local layout integrated

A δ item may still be awkward or unreliable in real use.

### ε — Workflow Tested

The item has been used in its actual intended workflow and its suitability has been evaluated.

Typical evidence:

- real task completed
- operator interaction observed
- setup and teardown exercised
- failure modes or friction points recorded
- performance checked under representative conditions

ε establishes operational evidence but not necessarily standardization.

### ζ — Standardized and Repeatable

The item has been made repeatable through appropriate labeling, documentation, standard work, visual control, configuration control, or reproducible setup.

Typical evidence:

- labeled location or interface
- documented setup
- controlled dimensions or configuration
- repeatable process
- replacement or restoration path
- other users could understand the intended state

ζ is the normal target for dependable operational use.

### η — Maintained and Audited

The standardized state is being sustained through inspection, audit, maintenance, corrective action, or periodic confirmation.

Typical evidence:

- inspection or maintenance record
- recurring audit
- calibration or verification history
- corrective-action loop
- obsolete state detected and repaired

η is not a one-time finishing step. It describes an actively sustained control condition.

## Assignment Rules

1. Assign the lowest defensible code when evidence is mixed.
2. A higher code normally implies that lower-code requirements remain satisfied.
3. Codes describe the current state, not effort expended or percentage complete.
4. Separate elements of one subsystem may hold different codes.
5. A code may regress when a modification invalidates previous integration, testing, or standardization.
6. Use a short note or evidence reference when the assigned code would otherwise be ambiguous.
7. Do not use η unless a real maintenance or audit loop exists.

## Example

```text
Milestone: Electronics Workstation Operational

bench structure: ζ
power distribution: ζ
ESD system: ε
task lighting: ζ
logic-analyzer validation procedure: ε
probe organization: δ
```

The milestone owner defines which codes are sufficient for acceptance. The schema does not impose one universal threshold.

## Unresolved Extensions

Future versions may define separate notation for conditions that are not maturity levels, including:

- blocked
- experimental
- quarantined
- retired
- superseded
- unsafe or prohibited from use

These should not be inserted into the α–η ladder without determining whether they are truly maturity states or orthogonal status modifiers.

## Change Control

Changes that materially alter code meaning require a new version of this document.

Applied examples and interpretive guidance may be expanded without changing the core meanings, provided the additions do not contradict earlier assignments.
