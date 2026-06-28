# THREAD INIT: FreeCAD MCP Server Setup

## Purpose

This thread is for planning a FreeCAD MCP server workflow.

## Project Context

Reference repository:

https://github.com/spkane/freecad-addon-robust-mcp-server

The goal is to connect a local MCP-capable assistant workflow to FreeCAD so documents, macros, objects, imports, exports, and screenshots can eventually be inspected or manipulated through an MCP interface.

## Constraint

This web chat does not directly control a local FreeCAD process. The setup is for a separate local MCP-capable client environment.

## Working Plan

Do not make this the critical path for the crane CAD project.

The crane CAD work should remain usable without MCP.

MCP becomes useful once there is:

- a FreeCAD install
- the Robust MCP Bridge installed
- a local MCP-capable client
- predictable document and object names
- repeatable macros or workflows

## First Task

Plan the installation and smoke-test sequence for the FreeCAD Robust MCP server, including likely failure points on Ubuntu or Kubuntu and how to keep the setup reversible.
