# Project MicroShop — Public Journal

## Purpose

This journal is the plain-English narrative layer of Project MicroShop.

The repository already contains engineering records: issues, checkpoints, standards, architecture notes, CAD files, status documents, and Git history. Those artifacts are optimized for preserving technical state. The journal instead records the story of the work: what the program was trying to accomplish, what was built or tested, what changed our minds, what failed, what became a dependency, and why priorities moved.

The journal is intended to be publicly readable.

## Format

Entries are maintained as rolling monthly files under `docs/journal/`.

The default style is concise technical prose rather than formal reports. Entries may link to durable repository artifacts rather than repeating them.

## Editorial Rules

- Write for an interested technical reader.
- Preserve dead ends, reversals, and failed assumptions when they explain later decisions.
- Distinguish ideas, experiments, validated capability, and adopted doctrine.
- Do not convert hindsight into false certainty.
- Prefer engineering significance over exhaustive chronology.
- Link to formal artifacts when the technical details already exist elsewhere.
- Treat the journal as narrative context, not as the source of truth for dimensions, procedures, specifications, or safety-critical information.

## Public-Exposure Rules

Do not publish:

- personal names unless deliberately intended for public attribution
- home or work addresses
- travel plans or location chronology
- private contact information
- account, order, payment, or tracking identifiers
- serial numbers or other uniquely identifying equipment identifiers
- credentials, tokens, private endpoints, or authentication material
- screenshots containing sensitive metadata
- unnecessary personal chronology

Localhost addresses such as `127.0.0.1` and `localhost` are ordinary technical information and are not considered sensitive by themselves.

When private source material informs an entry, extract only the engineering-relevant facts.

## Relationship to Other Records

- **Journal:** public narrative and project evolution.
- **README:** stable purpose and local doctrine.
- **STATUS:** current handoff state and next actions.
- **Checkpoint:** technically meaningful state capture.
- **Architecture:** current system structure and relationships.
- **Standard:** normative project practice.
- **ADR / decision record:** consequential choice and rationale.
- **Issue:** active work, questions, and task tracking.
- **Git history:** authoritative record of committed file changes.

The journal may summarize all of these, but does not replace them.

## Maintenance

The Project Manager node owns journal integration because it already sees cross-subsystem dependencies and project-level changes. Subtask agents may supply handoff notes or proposed entries, but the PM node should reconcile them into the public narrative.

A separate journal-only node is not required at the present scale. If journal maintenance later becomes substantial editorial work, it may be delegated without changing the journal's role or repository location.
