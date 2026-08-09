# CAD Toolchain Baseline v0.1

**Project:** Project MicroShop  
**Owner task:** MS-CAD-002 — CAD Toolchain + Parametric Modeling Infrastructure  
**Baseline date:** 2026-08-09  
**Status:** Operational baseline; selected add-on metadata and assembly standardization remain pending

## Purpose

Record the actual known CAD environment, explicitly distinguish confirmed state from unresolved metadata, and provide a reproducible compatibility reference for MicroShop CAD work.

This document does not infer installed state from upstream release history. Unknown local values remain unknown until captured from the running environment.

## Verified Baseline Summary

| Layer | Baseline state | Verification state |
|---|---|---|
| Host OS | Ubuntu 24.04.4 LTS with KDE/Plasma/XCB | confirmed from FreeCAD About block |
| Architecture | x86_64 | confirmed |
| FreeCAD distribution | AppImage managed through Gear Lever | confirmed |
| Previous distribution | Snap package removed | confirmed; no longer baseline |
| FreeCAD version/build | **1.1.3.20260725 (Git shallow) AppImage** | confirmed |
| FreeCAD build date | 2026-07-25 04:52:02 | confirmed |
| FreeCAD commit | `145529fe741292ff0b3977a01195bf0247425794` | confirmed |
| Bundled FreeCAD Python | **3.11.14** | confirmed |
| Qt / PySide | Qt 6.8.3 / PySide 6.8.3 | confirmed |
| OCC | 7.8.1 | confirmed |
| Assembly workflow | Assembly3 0.12.3 installed; program selection not frozen | installation confirmed |
| Fasteners workbench | previously used | exact current version pending |
| UnistrutWB | Project MicroShop reusable workbench/assets maintained separately | functional coexistence with MCP validated; exact version/commit pending |
| Robust MCP Bridge | **0.6.2** | installed and validated |
| MCP transport | XML-RPC on `localhost:9875` | connectivity validated |
| MCP secondary endpoint | socket/JSON-RPC on `localhost:9876` | bridge reports endpoint; XML-RPC remains validated path |
| external `freecad-mcp` | installed | successful connection check |
| Codex CLI | **0.147.0** | confirmed by `codex --version` |
| Zoo CLI | **0.2.187** at `/usr/local/bin/zoo` | confirmed by `zoo --version` |
| Git | **2.43.0** | confirmed by `git --version` |
| KCL → Zoo → STEP | working project capability | successful export demonstrated in lathe-cabinet PoC |
| GitHub engineering record | `cruelmillenial/projectMicroShop`, branch `main` | confirmed |
| Native FreeCAD source | FCStd | authoritative for FreeCAD-native designs |
| KCL source | KCL project files | authoritative for KCL-first designs |
| Neutral solid export | STEP | generated interchange/review geometry |
| Fabrication mesh | STL / 3MF | generated as required |
| 2D fabrication/interchange | DXF | generated as required |

## Captured FreeCAD Runtime

The production runtime was captured directly from FreeCAD:

```text
OS: Ubuntu 24.04.4 LTS (KDE/plasma/xcb)
Architecture: x86_64
Version: 1.1.3.20260725 (Git shallow) AppImage
Build date: 2026/07/25 04:52:02
Build type: Release
Hash: 145529fe741292ff0b3977a01195bf0247425794
Python 3.11.14, Qt 6.8.3, Coin 4.0.3, Vtk 9.3.1, boost 1_86, Eigen3 3.4.0, PySide 6.8.3
shiboken 6.8.3, xerces-c 3.3.0, IfcOpenShell 0.8.4, OCC 7.8.1
Installed mods:
  * Assembly3 0.12.3
```

This runtime block is authoritative for the v0.1 FreeCAD baseline unless superseded by a deliberate update.

## Verified External Tooling

### MCP connectivity

Validated command:

```bash
freecad-mcp --check --mode xmlrpc
```

Validated result:

```text
Testing connection to FreeCAD (xmlrpc mode)...
  Host: localhost:9875
✓ Connection successful!
  FreeCAD version: 1.1.3
  GUI available: 1
```

The explicit `--mode xmlrpc` remains the preferred validation path.

### Codex CLI

```text
codex-cli 0.147.0
```

Codex is used as an external agent from a project-scoped trusted CAD workspace. Repository files, not conversation state, are the durable project memory.

### Zoo CLI

```text
zoo 0.2.187
```

Installed executable:

```text
/usr/local/bin/zoo
```

Zoo has successfully executed a KCL-first design workflow through STEP generation in the lathe-cabinet proof of concept.

### Git

```text
git version 2.43.0
```

Git and the public GitHub repository provide the durable synchronization layer between CAD sessions, agents, and PM documentation.

## Distribution Decision

The program baseline is the **FreeCAD 1.1.3 AppImage installation managed by Gear Lever**, not the removed Snap package.

The AppImage provides a clear application-version boundary while project add-ons and reusable repositories remain user-space assets rather than being owned by the application package.

Gear Lever update and rollback policy remains a follow-on documentation item.

## FreeCAD / MCP Compatibility State

Robust MCP Bridge 0.6.2 and UnistrutWB have been demonstrated to coexist under FreeCAD 1.1.3 after resolving a Python namespace collision.

Both addons exposed a generic top-level `commands` module/package. The local Robust MCP installation was patched by renaming its `commands.py` module to `robust_mcp_commands.py` and updating its internal imports.

Validation after the patch included:

- FreeCAD startup without the namespace error,
- UnistrutWB P1000/P4100 generation,
- MCP bridge status operating,
- successful external XML-RPC connectivity.

The workaround is documented separately under the CAD toolchain compatibility records and MCP runbook. Updating or reinstalling Robust MCP may overwrite the patch and therefore triggers revalidation.

## Source-of-Truth Patterns

The program currently supports two legitimate CAD source patterns.

### FreeCAD-native

```text
parameters / measurements
        ↓
FCStd authoritative model
        ↓
STEP / STL / 3MF / DXF generated outputs
```

### KCL-first

```text
KCL authoritative project
        ↓
Zoo execution
        ↓
STEP generated snapshot
        ↓
FreeCAD inspection / downstream work as required
```

Generated STEP geometry must not silently replace the authoritative KCL source for a KCL-first design.

## Reusable Tooling

`cad/tools/cad-export` is a demonstrated shared CAD helper for KCL/Zoo export work.

The successful lathe-cabinet proof of concept established that generated outputs should normally remain local to the design lineage that generated them rather than being globally segregated by file format.

## Assembly and Add-on State

### Assembly

Assembly3 **0.12.3** is confirmed installed. This records availability only; it does not freeze Assembly3 as the program-wide preferred assembly workflow.

### UnistrutWB

Functional coexistence with the current FreeCAD/MCP environment has been demonstrated through representative P1000/P4100 generation.

Exact repository version/commit remains pending capture.

### Fasteners

Fasteners has been used previously in the MicroShop CAD environment, but the exact current installed version/source has not yet been captured. This is an unresolved metadata field, not a blocker to publishing D1.

## Operational Doctrine

- MCP is an automation layer, not authoritative CAD state.
- Manual FreeCAD operation remains a recovery path.
- KCL source remains authoritative for KCL-first projects.
- Generated interchange geometry must retain clear provenance.
- Codex sessions are working contexts; repository artifacts are durable context.
- Toolchain upgrades should trigger targeted revalidation rather than silent baseline drift.
- Existing physical models should not be rewritten merely to conform to standards that have not demonstrated practical value.

## Known Open Items

| Item | State | Required action |
|---|---|---|
| Gear Lever update/rollback policy | pending | document before relying on unattended application updates |
| UnistrutWB exact version/commit | pending metadata | capture when convenient |
| Fasteners exact version/source | pending metadata | capture when convenient |
| Preferred assembly workflow | not standardized | evaluate when an actual multi-part build makes the choice consequential |
| Robust MCP namespace workaround | validated local patch | revalidate after MCP update/reinstall |
| KCL → STEP → FreeCAD round-trip | STEP generation proven; downstream inspection remains workflow-dependent | validate when next required by a build |

## Revalidation Triggers

Recheck the affected portions of this baseline after:

- FreeCAD AppImage upgrade or replacement,
- Robust MCP update or reinstall,
- UnistrutWB update,
- Zoo CLI update,
- Codex CLI change that affects MCP behavior,
- assembly-workbench standardization,
- significant changes to `cad/tools/cad-export`,
- migration to a different host or FreeCAD packaging method.

## D1 Status

**D1 — CAD Toolchain Baseline v0.1 is published and operational.**

The remaining unresolved fields are deliberately recorded as pending metadata or future standardization decisions. They do not prevent the current toolchain from serving as the program baseline.

## Source Relationships

- MS-CAD-002 defines this deliverable and its version-aware doctrine.
- `docs/architecture/cad-toolchain-v0.2.md` describes the wider CAD source architecture.
- `docs/cad/toolchain/freecad-mcp-runbook-v0.1.md` contains operating and recovery procedures.
- CAD toolchain compatibility records document the Robust MCP / UnistrutWB collision workaround.
- CAD toolchain checkpoints record the KCL/Zoo/STEP proof of concept.
- `cad/lathe_cabinet/` provides the first working KCL-first application case.
