# CAD Toolchain Component Register v0.1

## Purpose

Track the software, integrations, source formats, and reusable design infrastructure that make up the Project MicroShop CAD toolchain.

This register records component identity and role. Exact versions, installation methods, and compatibility notes belong in the CAD Toolchain Baseline.

## Components

| Component | Role | Initial state |
|---|---|---|
| FreeCAD | Primary parametric CAD environment | active |
| Part Design workbench | Feature-based solid modeling | active |
| Part workbench | Constructive and general solid operations | active |
| Spreadsheet workbench | Parameter tables and model-driving values | active |
| Assembly workflow | Multi-body and multi-component assembly management | baseline selection pending |
| Fasteners workbench or equivalent | Reusable standard hardware | active / version verification pending |
| UnistrutWB / Project MicroShop Unistrut assets | Reusable structural framing geometry | active development |
| Python macros and scripts | Automation, export, and helper operations | active development |
| FreeCAD MCP server | External interaction and automation layer | setup tracked by MS-SW-001 |
| GitHub repository | Durable engineering record | active |
| FCStd | Authoritative native model format | active |
| STEP | Neutral solid interchange | active |
| STL / 3MF | Fabrication-oriented mesh export | as required |
| DXF | 2D fabrication/interchange output | as required |
| SVG / drawing outputs | Documentation and layout output | as required |

## Register Rules

- Version numbers are not assumed from memory; verify against the installed environment.
- Add-ons should include source repository and version or commit where practical.
- Experimental components should be marked explicitly.
- A reusable component should not be promoted to program infrastructure until it has survived use outside its originating build.
- Generated exports do not replace native source models or source parameters.

## Planned Companion Outputs

- `docs/cad/toolchain/cad-toolchain-baseline-v0.1.md`
- `docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`
- `docs/cad/library/component-register-v0.1.md`
- `docs/standards/parametric-modeling-standard-v0.1.md`
- `docs/standards/cad-repository-layout-v0.1.md`
- `docs/standards/cad-export-interchange-policy-v0.1.md`
