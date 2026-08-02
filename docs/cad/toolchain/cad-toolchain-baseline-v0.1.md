# CAD Toolchain Baseline v0.1

**Project:** Project MicroShop  
**Owner task:** MS-CAD-002 — CAD Toolchain + Parametric Modeling Infrastructure  
**Baseline date:** 2026-08-01  
**Status:** Provisional baseline; runtime captured, add-on and MCP verification pending

## Purpose

Record the actual known CAD environment, explicitly distinguish confirmed state from unverified carry-over state, and provide a compatibility reference for MS-SW-001 and MS-CAD-001.

This document does not infer installed state from upstream release history. Unknown local values remain unknown until captured from the running FreeCAD process.

## Baseline Summary

| Layer | Baseline state | Verification state |
|---|---|---|
| Host OS | Ubuntu 24.04.4 LTS with KDE/Plasma/XCB | confirmed from FreeCAD About block |
| Architecture | x86_64 | confirmed |
| FreeCAD distribution | AppImage managed through Gear Lever | confirmed |
| Previous distribution | Snap package removed | confirmed; no longer baseline |
| FreeCAD version/build | **1.1.3.20260725 (Git shallow) AppImage** | confirmed |
| FreeCAD build date | 2026-07-25 04:52:02 | confirmed |
| FreeCAD build type | Release | confirmed |
| FreeCAD commit | `145529fe741292ff0b3977a01195bf0247425794` | confirmed |
| Bundled FreeCAD Python | **3.11.14** | confirmed |
| Qt / PySide | Qt 6.8.3 / PySide 6.8.3 | confirmed |
| OCC | 7.8.1 | confirmed |
| Part Design | built-in program-required workbench | functional verification pending |
| Part | built-in program-required workbench | functional verification pending |
| Spreadsheet | built-in program-required workbench | functional verification pending |
| Assembly workflow | Assembly3 0.12.3 installed; program selection not frozen | installation confirmed |
| Fasteners workbench | previously used | not listed in captured installed-mod block; verification pending |
| UnistrutWB | Project MicroShop reusable workbench/assets maintained in a separate repository with user-space linkage | linkage/load verification pending |
| Python macros/scripts | active project capability | runtime now anchored to Python 3.11.14 |
| MCP implementation | `spkane/freecad-addon-robust-mcp-server` | selected by MS-SW-001; not yet smoke-tested in current environment |
| MCP release target | Robust MCP Server / Bridge Workbench v0.6.2 | target; installed state not assumed |
| MCP transport target | XML-RPC | preferred default |
| MCP default ports | 9875 XML-RPC; 9876 JSON-RPC socket | upstream defaults |
| GitHub engineering record | `cruelmillenial/projectMicroShop`, default branch `main` | confirmed |
| Native CAD source | FCStd | authoritative model format |
| Neutral solid export | STEP | interchange output |
| Fabrication mesh | STL / 3MF | generated as required |
| 2D fabrication/interchange | DXF | generated as required |

## Captured Runtime

The production runtime was captured directly from **Help → About FreeCAD → Copy to clipboard** on 2026-08-01:

```text
OS: Ubuntu 24.04.4 LTS (KDE/plasma/xcb)
Architecture: x86_64
Version: 1.1.3.20260725 (Git shallow) AppImage
Build date: 2026/07/25 04:52:02
Build type: Release
Branch: grafted,grafted
Hash: 145529fe741292ff0b3977a01195bf0247425794
Python 3.11.14, Qt 6.8.3, Coin 4.0.3, Vtk 9.3.1, boost 1_86, Eigen3 3.4.0, PySide 6.8.3
shiboken 6.8.3, xerces-c 3.3.0, IfcOpenShell 0.8.4, OCC 7.8.1
Locale: English/United States (en_US)
Navigation Style/Orbit Style/Rotation Mode: CAD/Rounded Arcball/Window center
Stylesheet/Theme/QtStyle: FreeCAD.qss/FreeCAD Dark/
Logical DPI/Physical DPI/Pixel Ratio: 96/156.308/1
Installed mods:
  * Assembly3 0.12.3
```

This runtime block is authoritative for the v0.1 local software baseline unless superseded by a deliberate update.

## Distribution Decision

The program baseline is the **FreeCAD 1.1.3 AppImage installation managed by Gear Lever**, not the removed Snap package.

Reasoning:

- the Snap package has been intentionally retired,
- the AppImage installation launches successfully,
- the actual running build has now been captured,
- an AppImage provides a clear program version boundary,
- Project MicroShop add-ons and reusable repositories should remain user-space assets rather than being owned by the application package.

Gear Lever configuration, update behavior, application-data placement, and rollback/update policy remain a follow-on review item.

## FreeCAD Version Policy at v0.1

Freeze **FreeCAD 1.1.3.20260725**, commit `145529fe741292ff0b3977a01195bf0247425794`, as the CAD runtime for the v0.1 baseline.

Do not move active build work onto weekly/development builds by default. A future stable upgrade should be treated as a controlled toolchain change and checked against active models and critical add-ons before becoming the new baseline.

## Runtime Capture Gate

**Complete for v0.1.**

The following are now captured:

- FreeCAD release and build identifier,
- commit hash,
- bundled Python version,
- Qt/PySide versions,
- application architecture,
- core dependency versions,
- reported installed add-ons.

For deeper diagnostics, the Python console can still be used to capture user application-data paths and the workbench registry:

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

That information is useful for the Gear Lever/add-on review but is no longer required to identify the running FreeCAD build.

## Add-on Verification Gate

After the AppImage migration, verify rather than assume persistence of add-on state.

The About block reports only:

- **Assembly3 0.12.3**

Absence from that list is not by itself proof that a manually linked or otherwise user-space workbench is unavailable. UnistrutWB and Fasteners therefore remain verification items rather than being declared missing.

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

Assembly3 **0.12.3** is confirmed installed under the current AppImage.

This confirms availability, not program-wide preference. Selection of the preferred assembly workflow remains a separate MS-CAD-002 standardization decision.

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

The FreeCAD runtime itself is now confirmed to bundle Python **3.11.14**, removing one previously unknown compatibility variable. The external MCP server environment remains separately managed and must still be verified.

The MCP layer remains optional automation. It is not authoritative CAD state and is not a prerequisite for manual FreeCAD modeling.

### MCP activation gate

Do not mark MS-SW-001 complete until all of the following are demonstrated against the actual AppImage baseline:

1. Robust MCP Bridge installed and visible,
2. bridge starts cleanly,
3. XML-RPC listener is reachable locally,
4. MCP server starts under its intended Python 3.11 environment,
5. `get_connection_status` succeeds,
6. `get_freecad_version` returns FreeCAD 1.1.3.20260725 / the recorded runtime,
7. a read-only document/object query succeeds,
8. a reversible write test creates and deletes a disposable object,
9. normal GUI modeling remains usable with MCP stopped.

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
- anchor testing to FreeCAD 1.1.3.20260725 / Python 3.11.14,
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
| Gear Lever configuration/update policy not yet documented | an automatic or opaque update could move the CAD runtime unexpectedly | review Gear Lever next session and define update/rollback policy |
| UnistrutWB linkage not yet verified in AppImage | reusable structural library may not be visible after package migration | execute UnistrutWB verification gate |
| Fasteners state not yet verified | standard hardware workflow may be unavailable or version-uncertain | verify presence and capture version/source |
| Assembly workflow not selected | cross-build assembly practice may fragment | compare available/built-in options against Assembly3 before freezing D2 assembly doctrine |
| MCP not smoke-tested | automation cannot yet be treated as available capability | execute MS-SW-001 activation gate |

## Freeze Criteria

The **FreeCAD runtime portion** of D1 is frozen at 1.1.3.20260725.

Change the overall D1 status from **Provisional** to **Frozen v0.1** when:

- required core workbenches are confirmed functional,
- UnistrutWB linkage is verified,
- Fasteners state is recorded,
- assembly state is recorded and its role understood even if the preferred workflow remains undecided,
- Gear Lever update/rollback behavior is documented sufficiently to preserve the runtime baseline,
- MS-SW-001 either passes its MCP smoke test or is explicitly marked unavailable/optional for this baseline.

## Source Relationships

- MS-CAD-002 thread init defines this document and its version-aware doctrine.
- `docs/architecture/cad-toolchain-v0.1.md` defines the source-of-truth architecture.
- `docs/cad/toolchain/component-register-v0.1.md` identifies toolchain components whose versions belong here.
- `docs/cad/library/component-register-v0.1.md` tracks reusable physical CAD assets separately from software components.
- MS-SW-001 owns MCP environment setup and smoke testing.
- MS-CAD-001 owns the Harbor Freight crane measurement-driven application model.
