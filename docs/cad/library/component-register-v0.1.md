# Reusable CAD Component Register v0.1

## Purpose

Track reusable parametric design assets that are candidates for use across multiple Project MicroShop builds.

This register is separate from the toolchain component register. It tracks modeled physical design primitives rather than software components.

## Initial Candidates

| Component family | Intended role | Current status |
|---|---|---|
| Unistrut P1000 / P4100 profiles | Structural framing primitives | active development |
| Unistrut slots / hole patterns | Reusable placement logic | active development |
| Unistrut plates / brackets | Connection hardware | partial / expand as reused |
| Standard fastener families | Shared hardware references | source workflow pending |
| Casters and machine feet | Mobility and support interfaces | candidate |
| Standard tubing / structural shapes | Generic fabrication primitives | candidate |
| Optical mount interfaces | Metrology fixture infrastructure | future candidate |
| Electrical enclosure footprints | Electronics / facility integration | future candidate |
| Workbench envelopes | Layout and interference checking | future candidate |
| Lifting / crane interfaces | Heavy mechanical integration | candidate |

## Promotion Rule

A build-local model becomes reusable program infrastructure when:

1. the geometry or interface has a stable definition,
2. configurable dimensions are explicit,
3. the asset is documented well enough to use outside its originating build,
4. it has survived use or validation in more than one physical-build context where practical,
5. its dependencies are understood.

## Required Metadata for Mature Library Assets

- stable asset name
- source or governing standard
- configurable parameters
- units
- coordinate-system convention
- interface dimensions
- version or revision
- source model location
- generated export locations
- known limitations
- validation or usage examples

## Process-Code Use

The Project MicroShop process-code schema may be used to track library maturity.

A reusable asset should not normally be considered program-standard at ζ until it has a repeatable interface and documented reuse path.
