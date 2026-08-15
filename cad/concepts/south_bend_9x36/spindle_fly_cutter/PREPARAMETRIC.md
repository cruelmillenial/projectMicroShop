ARTIFACT: PREPARAMETRIC_SPINDLE_MOUNT_FLY_CUTTER
PURPOSE: Codex / FreeCAD MCP Bridge handoff seed
STATUS: Pre-parametric concept definition; do not freeze machine-interface dimensions without measurement

OBJECTIVE

Develop a compact, rigid, directly spindle-mounted single-point facing cutter for a South Bend 9x36 lathe when the workpiece is fixtured to the compound/cross-slide assembly and the lathe is being used as a limited horizontal milling/facing machine.

The design objective is surface flatness and geometric control, not high material-removal rate.

The preferred architecture is closer to a one-tooth face mill than a traditional long-arm fly cutter:

    LATHE SPINDLE
         |
    [spindle interface]
         |
    [short rigid circular body]
         |
    [radially positioned single cutting edge]

Avoid unnecessarily long tool projection.

PRIMARY DESIGN PRINCIPLES

1. Minimize distance from spindle bearing system to cutting edge.
2. Maximize body stiffness.
3. Use one cutting edge only.
4. Provide positive cutter retention.
5. Permit controlled adjustment of swept diameter.
6. Permit cutter geometry to be changed without redesigning the spindle interface.
7. Provide optional balancing provisions opposite the cutting tool.
8. Make all critical geometry expression-driven.
9. Separate machine-specific spindle geometry from generic cutter-body geometry.
10. Do not depend on a drill chuck as the production mounting interface.

ARCHITECTURE

Create the assembly as at least three logical components:

A. SPINDLE INTERFACE MODULE
B. FLY-CUTTER BODY
C. CUTTING-TOOL / INSERT MODULE

Optional:

D. COUNTERWEIGHT MODULE

The spindle-interface module shall be replaceable without redesigning the cutter body.

Potential interfaces to support parametrically:

- South Bend threaded spindle nose / register-mounted backplate
- Morse-taper arbor if positively retained and suitable for interrupted cutting
- ER collet straight-shank arbor
- Weldon-style straight-shank arbor
- future custom spindle adapter

For the South Bend implementation, inspect and measure the actual lathe before choosing or generating the final interface. Do not assume nominal spindle-thread/register dimensions from historical documentation without verification.

PARAMETER FAMILIES

Create a FreeCAD Spreadsheet or equivalent master parameter object.

Suggested parameter groups:

MACHINE_INTERFACE:
    InterfaceType
    SpindleThreadMajorDiameter
    SpindleThreadPitch
    SpindleThreadLength
    SpindleRegisterDiameter
    SpindleRegisterDepth
    TaperMajorDiameter
    TaperMinorDiameter
    TaperLength
    ArborDiameter
    ArborLength

CUTTER_BODY:
    BodyDiameter
    BodyThickness
    HubDiameter
    HubLength
    CentralBoreDiameter
    BackRegisterDiameter
    ToolSlotRadialStart
    ToolSlotRadialEnd
    ToolSlotWidth
    ToolSlotDepth
    MaximumSweepDiameter
    MinimumSweepDiameter

CUTTING_GEOMETRY:
    CuttingRadius
    CutterProjection
    ToolBitWidth
    ToolBitHeight
    InsertType
    InsertPocketAngle
    AxialRake
    RadialRake
    LeadAngle
    ClearanceAngle
    EdgeAxialOffset

FASTENERS:
    CutterClampScrewDiameter
    CutterClampScrewCount
    CutterClampThread
    BackplateBoltCircleDiameter
    BackplateBoltCount
    BackplateBoltDiameter

BALANCE:
    CounterweightEnabled
    CounterweightRadius
    CounterweightMassVolume
    CounterweightFastenerDiameter
    MaximumIntendedRPM

MATERIAL:
    BodyMaterial
    ToolHolderMaterial
    CounterweightMaterial

GEOMETRIC REFERENCES

Establish:

Datum A = spindle mounting face
Datum B = spindle rotational axis
Datum C = cutter-body rear register
Datum D = nominal cutting plane

All major geometry should reference these datums rather than arbitrary generated faces.

CRITICAL RELATIONSHIPS

The cutting edge shall define a plane normal to the spindle rotational axis.

The cutting plane offset shall be explicitly parameterized.

The radial cutting-edge position shall determine swept diameter:

    SweepDiameter = 2 * CuttingRadius

The cutter should allow enough radial adjustment to cover several small-workpiece widths without creating a grossly oversized rotating envelope.

Favor a thick, compact disk/puck body over a long cantilevered bar.

TOOL RETENTION

Provide a mechanically positive clamp.

Acceptable concepts include:

- HSS toolbit captured in machined slot with clamp screws
- carbide insert pocket with conventional insert screw/clamp
- replaceable cartridge bolted into the fly-cutter body

Do not rely on friction from a single radial set screw against a cylindrical cutter shank.

HSS should remain a supported option because custom edge geometry and very sharp finishing edges may be useful on aluminum, brass, mild steel, and other materials.

COUNTERBALANCE

Model an optional counterweight opposite the cutting edge.

Do not assume balancing makes high-speed operation acceptable.

The counterweight exists to reduce unnecessary rotating imbalance at conservative fly-cutting speeds.

Create a parameterized counterweight pocket or bolt-on weight rather than embedding a fixed balance solution into the primary body.

MANUFACTURABILITY

The body should be manufacturable using ordinary lathe operations plus limited drilling/milling:

- face
- turn OD
- bore/register
- drill/tap
- machine radial tool slot or insert pocket

Design toward eventual manufacture on the South Bend itself where practical.

Avoid decorative features.

Prefer dimensions and features which can be inspected using:

- micrometer
- caliper
- dial indicator
- test indicator
- surface plate where appropriate

FREECAD IMPLEMENTATION

Create:

1. Master parameter Spreadsheet.
2. Machine_Interface body.
3. Cutter_Body body.
4. Cutter_Cartridge or ToolBit body.
5. Optional Counterweight body.
6. Assembly/container linking all components.
7. Named datum objects.
8. Clearance-envelope object showing swept diameter.
9. Optional transparent lathe spindle/workpiece reference bodies.

Use expressions rather than duplicated literal dimensions.

Name sketches and features semantically.

Avoid topology-dependent references where reasonable.

VALIDATION GEOMETRY

Include construction geometry representing:

- spindle axis
- cutting plane
- maximum rotating envelope
- minimum rotating envelope
- workpiece plane
- nominal compound/cross-slide feed direction

Provide interference checks between:

- cutter body and workpiece fixture
- cutter body and compound/toolpost
- cutter body and chuck/backplate/spindle nose as applicable

DESIGN CHECKS

Before considering the design mature, verify:

- spindle interface is positively retained
- body registers concentrically
- cutter does not rely on chuck-jaw clamping
- cutting edge can be positioned close to the body
- clamp screws cannot enter the work envelope
- counterweight cannot release centrifugally
- maximum sweep is visibly represented
- cutting plane is measurable/trammable
- fasteners are accessible with the cutter removed from the machine
- no geometry requires destructive modification of the South Bend

OUTPUTS

Generate:

- FreeCAD source model
- parameter table
- exploded assembly view
- spindle-interface detail
- cutting-tool retention detail
- maximum rotating-envelope view
- dimensioned manufacturing drawings sufficient for prototype construction

Do not produce final manufacturing dimensions for the South Bend spindle interface until actual-machine measurements are supplied.
