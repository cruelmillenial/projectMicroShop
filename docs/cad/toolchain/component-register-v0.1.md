# CAD Toolchain Component Register v0.1

## Purpose

Track the software, integrations, source formats, and reusable design infrastructure that make up the Project MicroShop CAD toolchain.

This register records component identity and role. Exact versions, installation methods, and compatibility notes belong in the CAD Toolchain Baseline.

## Components

| Component | Role | Initial state |
|---|---|---|
| FreeCAD | Primary downstream CAD environment; native parametric authoring for FreeCAD-first builds | active |
| Part Design workbench | Feature-based solid modeling | active |
| Part workbench | Constructive and general solid operations | active |
| Spreadsheet workbench | Parameter tables and model-driving values | active |
| Assembly workflow | Multi-body and multi-component assembly management | baseline selection pending |
| Fasteners workbench or equivalent | Reusable standard hardware | active / version verification pending |
| UnistrutWB / Project MicroShop Unistrut assets | Reusable structural framing geometry | active development |
| Python macros and scripts | Automation, export, and helper operations | active development |
| FreeCAD MCP server | External interaction and automation layer | active; setup tracked by MS-SW-001 |
| external `freecad-mcp` | CLI/MCP transport between automation client and FreeCAD bridge | active; XML-RPC validated |
| OpenAI Codex CLI | AI-assisted project-scoped CAD workspace client | active; project-local trust model established |
| KCL | Code-based parametric source format for KCL-first builds | PoC active |
| Zoo CLI | KCL execution and geometry export layer | installation/authentication pending in PoC |
| workspace-local `.tools/bin/` | Version-explicit location for external CAD CLI tools | proposed / PoC |
| `tools/cad-export` wrapper | Repeatable KCL → STEP export and optional validation command | proposed after manual export is proven |
| GitHub repository | Durable engineering record and session-continuity layer | active |
| `AGENTS.md` | Standing CAD/toolchain instructions for AI-assisted sessions | recommended |
| build-local `README.md` | Stable project definition, provenance, and file-role declaration | recommended |
| build-local `STATUS.md` | Session-to-session handoff and exact next-action record | recommended |
| FCStd | Authoritative native model for FreeCAD-first projects; downstream working format where appropriate | active |
| STEP | Neutral solid interchange snapshot | active |
| STL / 3MF | Fabrication-oriented mesh export | as required |
| DXF | 2D fabrication/interchange output | as required |
| SVG / drawing outputs | Documentation and layout output | as required |

## Current Operational Notes

- FreeCAD 1.1.3 and Robust MCP Bridge 0.6.2 have been validated together with UnistrutWB after applying the documented namespace-collision workaround.
- XML-RPC on `localhost:9875` is the currently validated external MCP transport.
- Codex should be launched from a project-scoped CAD workspace rather than a broad home-directory trust context.
- Repository files such as `AGENTS.md`, build-local `README.md`, and `STATUS.md` are preferred for durable session continuity.
- The 2026-08-08 CAD PoC established a second source pattern: KCL may remain authoritative parametric source, with Zoo exporting STEP for downstream FreeCAD use.
- Static KCL import validation has been demonstrated; Zoo execution, STEP export, and FreeCAD round-trip validation remain pending.

## Register Rules

- Version numbers are not assumed from memory; verify against the installed environment.
- Add-ons and external CLI tools should include source repository and version or commit where practical.
- Experimental components should be marked explicitly.
- A reusable component should not be promoted to program infrastructure until it has survived use outside its originating build.
- Generated exports do not replace authoritative parametric source or source parameters.
- Every project should declare whether its authoritative source is FCStd, KCL, or another approved source format.
- External source formats should retain provenance even when STEP or FCStd becomes an active downstream working format.
- Credentials and authentication tokens must not be stored in the repository.

## Companion Outputs

- `docs/architecture/cad-toolchain-v0.2.md`
- `docs/cad/toolchain/cad-toolchain-baseline-v0.1.md`
- `docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`
- `docs/cad/toolchain/codex-mcp-startup-continuity-v0.1.md`
- `docs/cad/toolchain/checkpoints/cad-mcp-poc-2026-08-08.md`
- `docs/cad/toolchain/compatibility/freecad-1.1.3-robust-mcp-0.6.2-unistrutwb-namespace-collision.md`
- `docs/cad/library/component-register-v0.1.md`
- `docs/standards/parametric-modeling-standard-v0.1.md`
- `docs/standards/cad-repository-layout-v0.1.md`
- `docs/standards/cad-export-interchange-policy-v0.1.md`
