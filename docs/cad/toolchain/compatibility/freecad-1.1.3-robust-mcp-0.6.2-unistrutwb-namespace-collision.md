# FreeCAD Robust MCP / UnistrutWB Namespace Collision — Resolution Note

## Classification

**Type:** Toolchain compatibility incident / resolved local workaround  
**Affected scope:** MS-SW-001, MS-CAD-002  
**Status:** Resolved / validated  
**Environment:** FreeCAD 1.1.3, Robust MCP Bridge 0.6.2, UnistrutWB

## Problem

After restoring `UnistrutWB` alongside the FreeCAD Robust MCP Bridge, FreeCAD reported the following startup error:

```text
Robust MCP Bridge: Deferred status bar sync failed:
cannot import name 'is_bridge_running' from 'commands'
(.../UnistrutWB/commands/__init__.py)
```

The cause was a Python module namespace collision.

Both addons exposed a top-level module or package named `commands`:

- Robust MCP Bridge 0.6.2: `commands.py`
- UnistrutWB: `commands/`

FreeCAD places addon directories on Python's import path. Robust MCP used unqualified imports such as:

```python
from commands import is_bridge_running
```

Depending on addon load order, Python resolved `commands` to the UnistrutWB package instead of Robust MCP's own module.

## Fix Applied

Installed Robust MCP location, generalized for portability:

```text
$HOME/.local/share/FreeCAD/v1-1/Mod/freecad-mcp-workbench-0.6.2
```

The Robust MCP module was renamed:

```text
commands.py
→ robust_mcp_commands.py
```

All eight internal Robust MCP imports were updated accordingly:

```python
from commands import ...
→ from robust_mcp_commands import ...
```

and:

```python
import commands
→ import robust_mcp_commands as commands
```

A backup of the unmodified workbench was created before applying the patch.

## Validation

After restarting FreeCAD:

- the startup namespace error no longer appeared
- UnistrutWB loaded and rendered P1000/P4100 geometry normally
- Robust MCP status indicator showed:

```text
MCP: Running (9875/9876)
```

- external MCP connectivity test passed:

```text
freecad-mcp --check --mode xmlrpc

✓ Connection successful!
FreeCAD version: 1.1.3
GUI available: 1
```

## Root Cause Summary

The failure was not caused by Unistrut geometry, FreeCAD document state, MCP transport, or XML-RPC connectivity.

The defect arose from generic top-level Python naming inside an addon environment where multiple addon roots coexist on `sys.path`.

## Maintenance Risk

An update or reinstall of Robust MCP Bridge may overwrite this local namespace patch.

Until upstream adopts collision-safe module naming or package-relative imports, treat this workaround as a local compatibility patch that must be revalidated after:

- Robust MCP upgrade or reinstall
- FreeCAD major/minor upgrade
- UnistrutWB packaging changes
- addon-path or load-order changes

## Recommended Upstream Direction

Prefer collision-safe packaging, for example:

- package-relative imports
- uniquely named internal modules
- avoiding generic top-level names such as `commands`

## Canonical Follow-up

Operational recovery and validation steps are retained in:

`docs/cad/toolchain/freecad-mcp-runbook-v0.1.md`
