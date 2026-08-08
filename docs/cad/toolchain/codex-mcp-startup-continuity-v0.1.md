# CAD + Codex/MCP Startup and Continuity v0.1

## Purpose

Establish a repeatable operating procedure for AI-assisted FreeCAD work within Project MicroShop using:

- FreeCAD 1.1.3 AppImage
- Robust MCP Bridge 0.6.2
- external `freecad-mcp`
- OpenAI Codex CLI
- the Project MicroShop CAD workspace and repository

The repository is the durable source of project context. Individual assistant sessions are working sessions and must not be treated as the sole persistence mechanism.

## Startup Procedure

### 1. Enter the CAD workspace

Launch Codex from the CAD portion of the Project MicroShop repository rather than from a broad home-directory context.

Example:

```bash
cd /path/to/projectMicroShop/cad
```

Trust should be scoped to the project-specific workspace. FreeCAD, addon installations, reusable workbench repositories, and other tooling do not need to reside inside that trusted workspace.

### 2. Start FreeCAD

Launch the FreeCAD 1.1.3 AppImage normally.

The Robust MCP Bridge should report a running state in the FreeCAD status area:

```text
MCP: Running (9875/9876)
```

Current validated bridge endpoints:

- XML-RPC: `localhost:9875`
- socket / JSON-RPC: `localhost:9876`

XML-RPC is the currently validated connection method.

### 3. Verify MCP connectivity when needed

From a shell:

```bash
freecad-mcp --check --mode xmlrpc
```

Known-good result includes:

```text
Testing connection to FreeCAD (xmlrpc mode)...
Host: localhost:9875
✓ Connection successful!
FreeCAD version: 1.1.3
GUI available: 1
```

Retain the explicit `--mode xmlrpc` until the installed MCP tooling demonstrates reliable default connection-mode behavior.

### 4. Start Codex

From the trusted CAD workspace:

```bash
codex
```

The current interaction path is:

```text
Codex
  |
  v
MCP / stdio
  |
  v
freecad-mcp
  |
  v
XML-RPC :9875
  |
  v
Robust MCP Bridge
  |
  v
FreeCAD GUI
```

When opening an unfamiliar document, begin with read-only inspection before modifying geometry.

## Session Continuity

Repository files are the durable operational memory for CAD work.

### `AGENTS.md`

Standing instructions for MicroShop CAD work may include:

- CAD and toolchain conventions
- MCP operating assumptions
- source-of-truth rules
- naming and export policy
- restrictions on modifying authoritative source material

### Project `README.md`

Each build-local CAD directory should document:

- purpose
- design origin
- authoritative inputs
- goals and constraints
- file roles

### `STATUS.md`

Where useful, each active CAD build may maintain a handoff file covering:

- work completed
- last known-good state
- decisions made
- unresolved questions
- exact next actions

At the end of a meaningful AI-assisted CAD session, update the build-local status record before closing the session.

A useful handoff instruction is:

> Update `STATUS.md` with work completed, decisions made, unresolved items, and exact next actions. Do not rewrite stable requirements unless they actually changed.

Git history remains authoritative for file changes. Conversation history is supplemental.

## Imported / External Design Organization

For externally originated designs, preserve both source/provenance material and interchange geometry.

Recommended structure:

```text
cad/
└── <build-name>/
    ├── README.md
    ├── STATUS.md
    ├── source-zoo/
    │   ├── original-export.zip
    │   └── *.kcl
    ├── interchange/
    │   └── main.step
    ├── freecad/
    │   └── <build-name>.FCStd
    └── exports/
```

For Zoo/KCL-originated designs:

- `.kcl` files remain source and provenance material.
- STEP is the geometry-interchange artifact.
- `.FCStd` becomes the FreeCAD-side working document.
- KCL source does not need to be embedded in the FreeCAD document.

## Known Compatibility Patch

Robust MCP Bridge 0.6.2 originally collided with UnistrutWB because both exposed a generic top-level Python `commands` module or package.

The validated local workaround renamed the Robust MCP module and rewrote its internal imports.

Canonical compatibility record:

`docs/cad/toolchain/compatibility/freecad-1.1.3-robust-mcp-0.6.2-unistrutwb-namespace-collision.md`

An update or reinstall of Robust MCP may overwrite the local patch and must trigger revalidation.

## Current Operational Status

```text
FreeCAD 1.1.3                    PASS
Robust MCP Bridge 0.6.2          PASS
XML-RPC localhost:9875           PASS
external freecad-mcp             PASS
Codex CLI integration            PASS
UnistrutWB coexistence           PASS
project-local trust model        ESTABLISHED
```

## Maintenance Rule

After changes to FreeCAD, Robust MCP, `freecad-mcp`, Codex integration, or addon load behavior:

1. re-run the MCP connectivity check;
2. confirm representative FreeCAD geometry still operates;
3. verify compatibility patches remain applicable;
4. update the relevant toolchain baseline, runbook, or compatibility note before declaring the environment operational.
