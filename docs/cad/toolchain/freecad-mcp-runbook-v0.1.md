# FreeCAD MCP Integration Runbook v0.1

## Purpose

Operational runbook for establishing, validating, recovering, and maintaining the FreeCAD MCP integration used by Project MicroShop.

This is a version-aware working document. Record environment-specific changes rather than assuming addon behavior is stable across FreeCAD or MCP releases.

## Current Verified Compatibility State

Verified combination:

- FreeCAD 1.1.3
- Robust MCP Bridge 0.6.2
- UnistrutWB present and functional
- XML-RPC connectivity verified

Known local compatibility patch:

`docs/cad/toolchain/compatibility/freecad-1.1.3-robust-mcp-0.6.2-unistrutwb-namespace-collision.md`

## Startup Check

After launching FreeCAD, confirm:

1. FreeCAD starts without addon import errors.
2. UnistrutWB loads normally.
3. Robust MCP reports a running state.
4. No deferred status-bar synchronization error references an unexpected addon module.

Known-good status indication:

```text
MCP: Running (9875/9876)
```

## External Connectivity Check

Run:

```text
freecad-mcp --check --mode xmlrpc
```

Known-good result includes:

```text
✓ Connection successful!
FreeCAD version: 1.1.3
GUI available: 1
```

Treat a successful transport check as necessary but not sufficient. Also verify that target workbenches and representative geometry operate normally.

## Representative Functional Smoke Test

For the current MicroShop toolchain:

1. Launch FreeCAD.
2. Confirm MCP bridge running.
3. Load UnistrutWB.
4. Create or render representative P1000/P4100 geometry.
5. Run the external MCP connectivity check.
6. Confirm no startup or deferred-import errors appear.

## Known Failure: Generic `commands` Namespace Collision

### Symptom

An error similar to:

```text
cannot import name 'is_bridge_running' from 'commands'
(.../UnistrutWB/commands/__init__.py)
```

### Cause

Robust MCP Bridge 0.6.2 exposes a top-level `commands.py`, while UnistrutWB exposes a top-level `commands/` package. Unqualified imports inside Robust MCP may resolve to the wrong addon depending on Python import-path ordering.

### Current Local Workaround

Within the Robust MCP addon directory:

```text
commands.py
→ robust_mcp_commands.py
```

Update internal imports:

```python
from commands import ...
→ from robust_mcp_commands import ...
```

and:

```python
import commands
→ import robust_mcp_commands as commands
```

The validated patch required updates to eight internal imports.

Always back up the unmodified addon before applying the patch.

## Upgrade / Reinstall Procedure

After any Robust MCP update or reinstall:

1. Assume the local namespace patch may have been overwritten.
2. Start FreeCAD and observe startup diagnostics.
3. Confirm whether upstream has fixed the naming collision.
4. If the generic `commands` module remains and the collision recurs, reapply the documented patch.
5. Run the full representative smoke test.
6. Record the new FreeCAD and Robust MCP versions before declaring the integration operational.

Also revalidate after:

- FreeCAD version changes
- UnistrutWB packaging changes
- addon directory changes
- Python environment changes

## Failure Isolation Order

When MCP integration fails, separate the layers:

1. **FreeCAD startup** — does FreeCAD load normally?
2. **Addon imports** — do Robust MCP and UnistrutWB load without namespace/import errors?
3. **Bridge state** — does the MCP bridge report running?
4. **Transport** — does `freecad-mcp --check --mode xmlrpc` succeed?
5. **CAD function** — can representative MicroShop geometry be created or queried?
6. **Automation client** — only after the lower layers are known-good, troubleshoot the external MCP client.

Do not treat an automation-client error as evidence that the FreeCAD addon itself is broken until the lower layers have been checked.

## Source-of-Truth Doctrine

MCP remains an interaction and automation layer.

Authoritative project state remains in:

- native CAD documents
- parameters and measurement registers
- reusable scripts
- repository documentation

The MicroShop CAD workflow must remain recoverable without MCP where practical.

## Maintenance Notes

Keep local patches small, documented, reversible, and version-specific.

When an upstream release eliminates a workaround, retain the compatibility note as historical evidence but mark the workaround retired in a later runbook revision.
