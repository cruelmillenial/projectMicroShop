# THREAD INIT: HF Crane CAD + Measurement Register

## Purpose

This thread is for building a usable FreeCAD reference model of the Harbor Freight / Pittsburgh 2-ton foldable shop crane, item 58755.

The original lathe lift mission is complete. This is now a CAD and measurement-control thread.

## Project Context

The crane is physically present at home now, but the user will soon be away in Seattle. The goal is to capture enough measurements before leaving so that remote CAD work is productive.

A generic imported crane model may be used as a reference mannequin, but it should not be treated as dimensional truth.

The actual design target is a simplified parametric FreeCAD model based on measured geometry.

## Relevant Files

Use these project files if available:

- Harbor Freight manual PDF for item 58755
- HF 2-ton crane measurement register CSV
- HF 2-ton crane measurement register XLSX
- Metric shoulder bolt size chart PDF if pin or shoulder bolt references become relevant

## Modeling Doctrine

Do not chase visual perfection.

Model mechanically meaningful geometry:

- tube envelopes
- pin axes
- caster envelopes
- boom extension positions
- ram closed and extended envelope
- hook/load point
- floor plane
- folded and deployed leg positions
- custom leg and outrigger design space

The important objects are pin centers, tube sizes, hole locations, caster mounted height, and interference zones.

## FreeCAD Structure Proposal

Use a document structure like:

- 00_Spreadsheet
- 01_Datums_Pin_Axes
- 02_Stock_Crane_Reference
- 03_Casters_Reference
- 04_Custom_Legs
- 05_Outriggers_Jacks
- 06_Boom_Extensions
- 07_Rigging_Envelope
- 99_Imported_Generic_Do_Not_Trust

## Measurement Priority

Before doing design work, help organize and populate these measurements:

- mast tube outside width and depth
- boom tube outside width and depth
- boom extension outside width and depth
- base and leg tube outside dimensions
- pin diameters
- boom pivot to ram upper pin
- ram lower pin to boom pivot
- boom pivot to boom extension holes
- boom pivot to hook/load point
- caster plate patterns
- caster mounted heights
- deployed leg length and spread
- folded leg envelope
- ram closed length, extended length if possible, and body clearance

## Working Assumptions

Manual dimensions are useful reference data but physical measurement wins.

Imported models are useful for layout and sanity checking but should not drive final geometry.

The model should support future design of:

- caster adapter plates
- complete caster assembly swaps
- custom shorter legs
- stock-length replacement legs
- slide-out or swing-out outriggers
- screw-down or cam-deploy stabilizer feet
- boom extensions
- hydraulic ram replacement envelopes

## First Task

Help set up the FreeCAD measurement-driven model plan and decide what measurements must be captured immediately before the user leaves town.
