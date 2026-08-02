# CAD Toolchain Baseline v0.1

**Project:** Project MicroShop  
**Owner task:** MS-CAD-002 — CAD Toolchain + Parametric Modeling Infrastructure  
**Baseline date:** 2026-08-01  
**Status:** Provisional baseline; exact running FreeCAD build capture pending

## Purpose

Record the actual known CAD environment, explicitly distinguish confirmed state from unverified carry-over state, and provide a compatibility reference for MS-SW-001 and MS-CAD-001.

This document does not infer an installed version from upstream release history. Unknown local values remain unknown until captured from the running FreeCAD process.

## Baseline Summary

| Layer | Baseline state | Verification state |
|---|---|---|
| Host OS | Ubuntu 24.04 with KDE desktop | confirmed from current workstation context |
| FreeCAD distribution | AppImage managed through Gear Lever | confirmed |
| Previous distribution | Snap package removed | confirmed; no longer baseline |
| FreeCAD launch | Current AppImage launches successfully | confirmed |
| Exact FreeCAD version/build | **not yet captured** | required before baseline freeze |
| Upstream stable release on baseline date | FreeCAD 1.1.3 | external reference only; not assumed installed |
| Bundled FreeCAD Python | **not yet captured** | required before MCP activation |
| Part Design | program-required / previously used | post-migration load verification pending |
| Part | program-required / previously used | post-migration load verification pending |
| Spreadsheet | program-required / previously used | post-migration load verification pending |
| Assembly workflow | prior Assembly3/Assembly4 experimentation; program selection not frozen | verify installed state, then select deliberately |
| Fasteners workbench | previously used | post-migration version/load verification pending |
| UnistrutWB | Project MicroShop reusable workbench/assets maintained in a separate repository with user-space linkage | verify linkage loads under current AppImage |
| Python macros/scripts | active project capability | exact runtime assumptions not frozen |
| MCP implementation | `spkane/freecad-addon-robust-mcp-server` | selected by MS-SW-001; not yet smoke-tested in current environment |
| MCP release target | Robust MCP Server / Bridge Workbench v0.6.2 | current external reference; installed state not assumed |
| MCP transport target | XML-RPC | upstream-recommended default |
| MCP default ports | 9875 XML-RPC; 9876 JSON-RPC socket | upstream defaults |
| GitHub engineering record | `cruelmillenial/projectMicroShop`, default branch `main` | confirmed |
| Native CAD source | FCStd | authoritative model format |
| Neutral solid export | STEP | interchange output |
| Fabrication mesh | STL / 3MF | generated as required |
| 2D fabrication/interchange | DXF | generated as required |

## Distribution Decision

The program baseline is now the **AppImage installation managed by Gear Lever**, not the removed Snap package.

Reasoning:

- the Snap package has been intentionally retired,
- the AppImage installation has been launched successfully,
- an AppImage gives the CAD program a clearer version boundary than a distribution package that may lag or patch differently,
- Project MicroShop add-ons and reusable repositories should remain user-space assets rather than being owned by the application package.

The exact AppImage release remains a required capture item. Do not label the local install `1.1.3` merely because 1.1.3 is the current upstream stable release.

## FreeCAD Version Policy at v0.1

Use a stable 1.1.x AppImage as the production CAD line unless a specific build requires otherwise.

As of 2026-08-01, upstream stable is FreeCAD 1.1.3. FreeCAD 1.1.2 included security and stability backports; 1.1.3 followed with an additional save/version-warning fix.

Once the exact installed build is captured:

- if it is 1.1.3, freeze that as the v0.1 program baseline;
- if it is 1.1.2, continued use is acceptable while the 1.1.3 update is evaluated deliberately;
- if it is older than 1.1.2, prefer a controlled update to the current stable 1.1.x line before declaring the baseline frozen;
- do not move active build work onto weekly/development builds by default.

## Local Environment Capture Gate

Before this baseline becomes **frozen**, capture the running environment from FreeCAD itself.

Preferred GUI method:

1. Open FreeCAD.
2. Use **Help → About FreeCAD → Copy to clipboard**.
3. Record the complete version block here.

Useful Python-console capture:

```python
import sys
import FreeCAD as App
import FreeCADGui as Gui

print("FreeCAD:", App.Version())
print("Python:", sys.version)
print("UserAppData:", App.getUserAppDataDir())
print("ResourceDir:", App.getResourceDir())
print("Workbenches:", sorted(Gui.listWorkbenches().keys()))
```

Record at minimum:

- FreeCAD version and revision/build identifier,
- bundled Python version,
- Qt/PySide information from the About block,
- application architecture,
- loaded/available workbench names,
- user application-data path.

## Add-on Verification Gate

After the AppImage migration, verify rather than assume persistence of add-on state.

### UnistrutWB

Expected architecture:

- source repository exists outside the FreeCAD package,
- FreeCAD user-space workbench path links or points to that repository,
- removing the old Snap package must not be treated as removing authoritative UnistrutWB source.

Verification required:

- workbench appears in the current AppImage,
- module imports without error,
- one known P1000/P4100 object regenerates successfully,
- existing JSON/profile configuration is found from the expected source location,
- BOM export still executes if currently implemented.

### Fasteners

Verify:

- workbench is present,
- version/source is captured,
- a representative fastener inserts and recomputes successfully.

### Assembly

Do not freeze an assembly standard merely because Assembly3 or Assembly4 existed in an older installation.

First verify what is installed under the AppImage. Selection of the preferred assembly workflow remains a separate MS-CAD-002 standardization decision.

## MCP Baseline

MS-SW-001 selected `spkane/freecad-addon-robust-mcp-server` as the MCP implementation.

Current upstream architecture separates:

1. **Robust MCP Bridge Workbench** inside FreeCAD, and
2. **Robust MCP Server** used by the external MCP-capable client.

For v0.1 the target is:

- Robust MCP Server v0.6.2,
- Robust MCP Bridge Workbench v0.6.2,
- XML-RPC transport as the default,
- bridge on `localhost:9875`,
- JSON-RPC socket retained as fallback on `localhost:9876`,
- external server environment using Python 3.11 as required by the implementation.

The MCP layer remains optional automation. It is not authoritative CAD state and is not a prerequisite for manual FreeCAD modeling.

### MCP activation gate

Do not mark MS-SW-001 complete until all of the following are demonstrated against the actual AppImage baseline:

1. current FreeCAD build captured,
2. bundled Python version captured,
3. Robust MCP Bridge installed and visible,
4. bridge starts cleanly,
5. XML-RPC listener is reachable locally,
6. MCP server starts under its intended Python 3.11 environment,
7. `get_connection_status` succeeds,
8. `get_freecad_version` returns the same FreeCAD instance/build recorded by this baseline,
9. a read-only document/object query succeeds,
10. a reversible write test creates and deletes a disposable object,
11. normal GUI modeling remains usable with MCP stopped.

## Comparison: MS-SW-001

**Result: aligned, with implementation details needing refresh.**

The existing MS-SW-001 architecture remains correct:

- MCP is local/external automation,
- it must not become the crane project's critical path,
- manual FreeCAD remains the fallback,
- predictable object/document naming improves automation reliability.

Required updates to the task when work resumes:

- use the current split Bridge Workbench + MCP Server architecture,
- target v0.6.2 unless a newer release is deliberately adopted,
- verify Python compatibility against the actual AppImage before installation,
- prefer XML-RPC first,
- use the activation gate above as the smoke-test definition.

No redesign of CAD models is required for MCP.

## Comparison: MS-CAD-001

**Result: strongly aligned; no corrective redesign required.**

MS-CAD-001 already establishes the correct authority hierarchy:

1. actual crane measurements,
2. simplified parametric FreeCAD geometry derived from those measurements,
3. manual/reference dimensions as secondary evidence,
4. imported generic models as non-authoritative mannequins.

That is consistent with the MS-CAD-002 modeling doctrine.

The crane task should continue independently of MCP. When D2 is mature enough to prove useful, MS-CAD-001 may adopt shared naming, datum, parameter-register, and validation conventions prospectively. Existing geometry should not be rewritten merely for conformity.

## Baseline Risks / Open Items

| Item | Risk | Action |
|---|---|---|
| Exact AppImage build unknown | version-specific behavior cannot yet be reproduced precisely | capture About block |
| Bundled Python unknown | MCP ABI/runtime assumptions cannot be verified | capture About block / Python console |
| Post-migration add-on load state unknown | UnistrutWB/Fasteners/Assembly may appear installed but fail at import or recompute | execute add-on verification gate |
| Assembly workflow not selected | cross-build assembly practice may fragment | defer selection until installed state and 1.1.x capability are compared |
| MCP not smoke-tested | automation cannot yet be treated as available capability | execute MS-SW-001 activation gate |

## Freeze Criteria

Change status from **Provisional** to **Frozen v0.1** when:

- exact FreeCAD build is recorded,
- bundled Python is recorded,
- required core workbenches are confirmed,
- UnistrutWB linkage is verified,
- Fasteners state is recorded,
- assembly state is recorded even if the preferred workflow remains undecided,
- MS-SW-001 either passes its MCP smoke test or is explicitly marked unavailable/optional for this baseline.

## Source Relationships

- MS-CAD-002 thread init defines this document and its version-aware doctrine.
- `docs/architecture/cad-toolchain-v0.1.md` defines the source-of-truth architecture.
- `docs/cad/toolchain/component-register-v0.1.md` identifies toolchain components whose versions belong here.
- `docs/cad/library/component-register-v0.1.md` tracks reusable physical CAD assets separately from software components.
- MS-SW-001 owns MCP environment setup and smoke testing.
- MS-CAD-001 owns the Harbor Freight crane measurement-driven application model.
