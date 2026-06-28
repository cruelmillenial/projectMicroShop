# THREAD INIT: FreeCAD MCP Server Setup

## Purpose

This thread is for setting up the FreeCAD MCP server workflow later, likely during the Seattle trip or after returning.

This is a software and local tooling thread, separate from the physical crane-measurement thread.

## Project Context

The repository of interest is:

https://github.com/spkane/freecad-addon-robust-mcp-server

The goal is to get a local MCP-capable assistant workflow connected to FreeCAD so that FreeCAD documents, macros, objects, imports, exports, and screenshots can eventually be manipulated or inspected through an MCP interface.

## Important Constraint

This ChatGPT web session cannot directly connect to the user's local 127.0.0.1 FreeCAD instance.

The MCP setup is therefore for a local MCP-compatible client environment, not for this web chat directly controlling FreeCAD.

## Working Plan

Do not make this the critical path for the shop crane project.

The crane CAD work should be usable without MCP.

MCP becomes useful once there is:

- a FreeCAD install
- the Robust MCP Bridge installed
- a local MCP-capable client
- a named FreeCAD document structure
- predictable object names
- repeatable macros or workflows

## Likely Setup Tasks

Investigate and execute:

- FreeCAD version compatibility
- Python version requirements
- whether FreeCAD is installed by apt, AppImage, Snap, Flatpak, or source
- Addon Manager install path for Robust MCP Bridge
- bridge start procedure inside FreeCAD
- XML-RPC and socket ports
- MCP client configuration
- whether the MCP server command can be launched cleanly
- whether screenshots and document inspection work
- whether object creation and macro execution work

## Suggested Smoke Test

The first success condition is not full automation.

The first success condition is:

- FreeCAD opens
- Robust MCP Bridge is installed
- bridge starts
- expected local ports are listening
- MCP client can list tools or query FreeCAD state
- a trivial object can be created or inspected
- a screenshot or document summary can be retrieved

## Keep Separate From

Do not mix this thread with:

- physical crane measurements
- caster procurement
- caliper SPC decoding
- hydraulic system design
- lathe lifting operations

This thread is tooling infrastructure only.

## First Task

Help plan the installation and smoke-test sequence for the FreeCAD Robust MCP server, including likely failure points on Ubuntu or Kubuntu and how to keep the setup reversible.
