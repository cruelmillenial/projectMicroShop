ARTIFACT: PREPARAMETRIC_COMPOUND_SLIDE_AUXILIARY_SPINDLE
PURPOSE: Codex / FreeCAD MCP Bridge handoff seed
STATUS: Pre-parametric modular accessory concept

OBJECTIVE

Develop a modular auxiliary high-speed spindle carrier for a South Bend 9x36 lathe.

Initial payload may be a Dremel or similar rotary tool.

The design shall not be intrinsically Dremel-specific.

The longer-term architecture shall support replacement of the initial rotary tool with a compact purpose-built high-speed spindle such as an ER11 spindle motor, pencil grinder, flexible-shaft handpiece, or comparable device.

Primary intended operations include:

- light external grinding
- internal grinding
- high-speed small-diameter drilling
- polishing
- deburring
- engraving
- limited light milling where appropriate
- small abrasive or rotary-tool operations

The normal configuration places the auxiliary spindle on or above the compound/toolpost system so carriage, cross-slide, and compound motion control the cutter.

ARCHITECTURAL PRINCIPLE

Separate the system into:

A. MACHINE INTERFACE
B. HEIGHT / POSITION ADAPTER
C. UNIVERSAL SPINDLE CARRIER
D. TOOL-SPECIFIC PROFILE ADAPTER

Conceptually:

    [auxiliary spindle]
           |
    [profile adapter]
           |
    [split clamp/carrier]
           |
    [height/orientation adapter]
           |
    [compound/QCTP interface]

The machine interface and tool profile shall be independently replaceable.

MACHINE INTERFACE OPTIONS

Support at least conceptual variants for:

- existing toolpost stud
- QCTP holder/dovetail interface
- reversible compound-top mounting plate
- future direct cross-slide accessory plate

Do not require drilling, grinding, or permanently modifying the original South Bend compound.

Use existing attachment geometry wherever practical.

Before finalizing:

Measure the actual lathe.

Required machine measurements may include:

- spindle centerline above compound reference surface
- toolpost stud diameter/thread
- toolpost stud position
- available compound-top footprint
- QCTP geometry if present
- cross-slide travel envelope
- compound rotation envelope
- chuck clearance
- tailstock interference envelope

PRIMARY PARAMETERS

MASTER:
    AuxiliarySpindleType
    MountInterfaceType
    Orientation
    SpindleAxisHeight
    SpindleAxisLateralOffset
    SpindleAxisAxialOffset

MACHINE_INTERFACE:
    ToolpostStudDiameter
    ToolpostStudThread
    ToolpostStudLength
    MountPlateLength
    MountPlateWidth
    MountPlateThickness
    QCTPDovetailWidth
    QCTPDovetailAngle
    QCTPReferenceHeight

CARRIER:
    CarrierLength
    CarrierWidth
    CarrierHeight
    ClampBoreDiameter
    ClampLength
    ClampWallThickness
    ClampGap
    ClampBoltDiameter
    ClampBoltCount
    ClampBoltSpacing

PROFILE_ADAPTER:
    ToolBodyDiameter
    ToolBodyLength
    ToolNoseDiameter
    ToolNoseThread
    PreferredClampingRegionStart
    PreferredClampingRegionLength
    ToolVentClearance
    SwitchClearance
    BrushCapClearance
    CableClearance

POSITIONING:
    HeightAdjustmentMinimum
    HeightAdjustmentMaximum
    LateralAdjustmentRange
    AxialAdjustmentRange
    AngularAdjustmentEnabled
    AngularAdjustmentMinimum
    AngularAdjustmentMaximum

FASTENERS:
    MountBoltDiameter
    ClampBoltDiameter
    AdjustmentBoltDiameter

REFERENCE DATUMS

Datum A = machine mounting surface
Datum B = main lathe spindle axis
Datum C = auxiliary spindle axis
Datum D = nominal auxiliary-tool tip plane
Datum E = compound longitudinal direction

The most important controlled relationship is:

    AuxiliarySpindleAxisHeight relative to MainSpindleAxis

The system shall allow the auxiliary spindle axis to be deliberately placed:

- exactly on center
- above center
- below center

depending upon operation.

Do not bury center-height corrections in arbitrary sketches.

Make them explicit parameters.

SPINDLE CLAMPING

Preferred carrier geometry is a rigid split clamp surrounding an approved cylindrical mechanical region of the spindle/tool.

Do not indiscriminately crush a consumer rotary-tool plastic housing.

If the initial Dremel provides a threaded nose or designed mounting collar, investigate using that interface or combining it with a secondary body support.

The carrier must resist:

- spindle torque reaction
- radial grinding force
- axial drilling force
- vibration

without depending entirely on friction against fragile plastic.

TOOL PROFILE ABSTRACTION

Create the rotary-tool envelope as a separate replaceable component.

Initial profile:

    DREMEL_PROFILE_A

Future profiles may include:

    ER11_SPINDLE_PROFILE
    PENCIL_GRINDER_PROFILE
    FLEX_SHAFT_PROFILE

Changing the payload should not require editing the machine-interface body.

ORIENTATION

The first implementation should prioritize an auxiliary spindle axis parallel to the main lathe spindle axis.

This supports:

- external cylindrical grinding
- internal grinding
- coaxial drilling
- polishing

Provide architecture for later variants allowing:

- spindle axis perpendicular to main spindle
- adjustable angular orientation

Do not introduce angular adjustment into the MVP if it materially compromises stiffness.

STIFFNESS

Keep:

- clamp short
- tool projection short
- center height low enough to avoid unnecessary pedestal leverage
- interface footprint broad
- bolted joints preloaded

Avoid thin printed cantilever brackets for grinding loads.

3D printed components may be used for:

- cable guides
- guards
- test fit
- dust nozzles
- nonstructural profile adapters

Structural carrier components should be designed for metal unless analysis supports another material.

SERVICEABILITY

The spindle must be removable without removing the entire lathe mounting interface.

Wear components and profile adapters should be replaceable separately.

Fasteners must remain tool-accessible.

Cable routing must avoid:

- chuck
- workpiece
- leadscrew
- carriage handwheels
- ways
- spindle cooling openings

GRINDING CONTAMINATION

Model provisions for a removable source-capture nozzle or rigid debris shield.

Grinding abrasive must not be allowed to freely contaminate the South Bend ways.

Any guard design shall be rigid or positively retained and unable to enter rotating machinery.

Do not create loose cloth or flexible covers near the chuck/workpiece.

OPTIONAL DUST-CAPTURE INTERFACE PARAMETERS

    VacuumNozzleEnabled
    NozzleDiameter
    NozzleOffset
    NozzleAngle
    ShieldEnabled
    ShieldThickness

FREECAD IMPLEMENTATION

Create:

1. Parameters Spreadsheet.
2. Machine_Interface body.
3. Height_Position_Adapter body.
4. Universal_Carrier body.
5. Tool_Profile body.
6. Clamp hardware references.
7. Main lathe spindle-axis datum.
8. Auxiliary spindle-axis datum.
9. Tool rotational envelope.
10. Chuck/workpiece exclusion envelope.
11. Cable exclusion envelope.
12. Optional dust-capture component.

Use semantic object names.

Drive dimensions from Spreadsheet expressions.

Avoid geometry based on generated-face references where practical.

CONFIGURATIONS

Create at least these named configurations:

CONFIG_A:
    Dremel
    parallel to main spindle
    compound/toolpost mounted
    center-height adjustable

CONFIG_B:
    generic ER11 auxiliary spindle
    parallel to main spindle
    same machine interface

CONFIG_C:
    placeholder perpendicular-spindle architecture
    not necessarily production-ready

VALIDATION

Verify:

- carrier does not interfere with chuck throughout intended carriage travel
- spindle axis can be brought to lathe spindle center height
- adjustment cannot slip under light grinding force
- clamping does not obstruct spindle ventilation
- cutter access is practical
- spindle removal is straightforward
- no permanent machine modification is required
- rotating-tool envelope is visible in CAD
- cable path remains outside rotating envelope
- design can accept a future ER11 spindle without replacing the South Bend interface

OUTPUTS

Generate:

- FreeCAD assembly/model
- parameter table
- Dremel profile placeholder
- generic ER11 profile placeholder
- compound/toolpost interface drawing
- carrier drawing
- spindle-axis alignment drawing
- exploded assembly
- interference-envelope view

Do not finalize Dremel-specific body geometry until the actual rotary tool model and dimensions are supplied.
