ARTIFACT: PREPARAMETRIC_TM010_CYLINDRICAL_RESONANT_CAVITY
PURPOSE: Codex / FreeCAD MCP Bridge handoff seed
STATUS: First RF manufacturing demonstrator
TARGET: Approximately 2.45 GHz TM010 cylindrical cavity
MACHINE BASIS: South Bend 9x36 lathe plus appropriate workholding/drilling/milling accessories

MISSION

Develop a simple cylindrical microwave resonant cavity that can be manufactured primarily on a South Bend 9x36 lathe and subsequently characterized with a vector network analyzer.

The purpose is not initially to produce a commercial RF component.

The purpose is to establish an end-to-end capability loop:

    electromagnetic target
        ->
    parametric cavity geometry
        ->
    machining
        ->
    dimensional inspection
        ->
    VNA measurement
        ->
    comparison with prediction
        ->
    geometry correction

Select a geometry whose electromagnetically critical surfaces are predominantly surfaces of revolution so that the South Bend lathe performs the most important machining.

BASELINE MODE

Use a cylindrical pillbox cavity operating nominally in the TM010 mode.

For an ideal empty cylindrical cavity:

    f_TM010 = x01 * c / (2 * pi * a)

where:

    x01 approximately 2.40482556
    c = speed of light
    a = cavity internal radius

For a target of approximately 2.45 GHz, the ideal unloaded cavity diameter is approximately:

    INTERNAL DIAMETER ~= 93.67 mm
                      ~= 3.688 in

Treat this only as the theoretical initial value.

Actual resonance will shift due to:

- finite conductivity
- end geometry
- seams
- coupling probes
- tuning hardware
- corner radii
- plating
- machining error
- temperature
- any dielectric material introduced

Therefore the CAD shall make target frequency and internal diameter explicit parameters rather than frozen dimensions.

INITIAL PHYSICAL ARCHITECTURE

Use a two-piece cavity:

A. MAIN CAVITY BODY
B. REMOVABLE END CAP

Preferred body concept:

    round stock
       |
    faced end
       |
    precision cylindrical bore
       |
    integral closed back wall

The second end is closed with a removable precision-registering cap.

Conceptual section:

        removable cap
      __________________
     |__________________|
     |                  |
     |                  |
     |    RF CAVITY     |
     |                  |
     |                  |
     |__________________|
       integral bottom

Use a male/female locating register or spigot at the cap interface so cavity concentricity and seam position are controlled by turned geometry rather than by clearance screws.

The retaining screws should clamp the cap.

They should not be responsible for locating it.

NOMINAL STARTING DIMENSIONS

Use these only as first-article design values:

    TargetFrequency = 2.45 GHz
    CavityID ~= 93.67 mm
    CavityRadius ~= 46.83 mm
    CavityDepth ~= 35-50 mm initial design region

Choose a nominal depth in this range after checking modal spacing and practical coupling geometry.

The cavity depth is to remain independently parameterized.

Do not encode the false assumption that TM010 frequency is controlled equally by diameter and depth.

The diameter is the principal ideal TM010 frequency-setting dimension.

PARAMETER GROUPS

RF_TARGET:
    TargetFrequency
    TargetMode
    SpeedOfLight
    TM010Root
    CalculatedIdealRadius
    CalculatedIdealDiameter

CAVITY:
    CavityInnerDiameter
    CavityDepth
    BottomWallThickness
    SideWallThickness
    OuterDiameter
    ExternalLength
    InternalCornerRadius
    ExternalCornerRadius

CAP:
    CapThickness
    CapOuterDiameter
    RegisterDiameter
    RegisterDepth
    RegisterClearance
    SealLandWidth
    BoltCircleDiameter
    BoltCount
    BoltDiameter

COUPLING:
    InputCouplerEnabled
    OutputCouplerEnabled
    InputRadialPosition
    OutputRadialPosition
    ProbeDiameter
    ProbePenetration
    ProbeOrientation
    ConnectorType

TUNING:
    TuningFeatureEnabled
    TuningScrewDiameter
    TuningScrewPosition
    MaximumTuningPenetration
    LockNutThickness

MATERIAL:
    BodyMaterial
    CapMaterial
    Conductivity
    SurfaceFinishTarget
    PlatingEnabled
    PlatingMaterial
    PlatingThickness

METROLOGY:
    BoreTolerance
    RegisterTolerance
    CapFlatnessTarget
    SurfaceFinishTarget
    ConcentricityTarget

REFERENCE DATUMS

Datum A = cavity rotational axis
Datum B = integral cavity-bottom RF surface
Datum C = cap mating face
Datum D = cap internal RF surface
Datum E = cavity cylindrical RF wall

The electromagnetic cavity volume shall be explicitly represented as its own solid or reference volume.

This will eventually permit export to electromagnetic simulation tools.

MATERIAL STRATEGY

Support at least:

PROTOTYPE:
    6061 aluminum or comparable machinable conductive alloy

HIGHER-CONDUCTIVITY ARTICLE:
    C101/C110 copper or other appropriate high-conductivity copper

OPTIONAL FINISH:
    copper, silver, or other RF-relevant plating where justified

Do not assume expensive raw material automatically creates a high-Q cavity.

Geometry, surface condition, seams, coupling, material conductivity, and measurement all matter.

For the first machining demonstrator, machinability and dimensional control may justify aluminum before progressing to copper.

CAP INTERFACE

The end cap is a critical RF and mechanical feature.

Model:

- precision locating register
- broad conductive mating land
- symmetric screw preload
- minimal uncontrolled seam gap

Provide sufficient wall thickness around tapped holes.

The register should establish radial alignment.

The mating face should establish axial position.

Avoid relying upon bolt clearance holes for alignment.

COUPLING

Provide two weakly coupled VNA ports if practical.

Suggested architecture:

- two coaxial connectors
- electrically small probes or loops entering the cavity
- independently parameterized probe penetration

The exact coupling geometry is experimental and shall remain replaceable.

Treat the connectors and probes as modules rather than permanent cavity-body geometry.

Connector holes need not be RF-critical turned surfaces.

They may be produced using:

- lathe faceplate/off-axis fixture
- milling attachment
- compound-mounted auxiliary spindle
- drill press
- other controlled secondary operation

The principal cavity bore, bottom, cap face, and cap register should remain lathe-generated.

TUNING

Provide an optional fine-tuning feature.

Possible MVP:

    threaded conductive tuning screw entering the cavity at a controlled location

Requirements:

- penetration parameterized
- lockable after adjustment
- removable for baseline measurements
- represented in the electromagnetic volume
- positioned where useful without making the first article unnecessarily complicated

Do not depend upon the tuning screw to compensate for grossly incorrect cavity machining.

MACHINING STRATEGY

Design around operations suitable for a 9x36 South Bend:

MAIN BODY:
    face stock
    turn OD/reference surfaces
    bore cavity ID
    finish bore
    face internal bottom if tooling permits
    machine cap register
    drill/tap cap-retention pattern using appropriate secondary fixture

CAP:
    face both sides
    turn OD
    turn register/spigot
    establish controlled internal RF face
    drill clearance pattern
    machine connector/coupler features as secondary operations

Critical geometry should be achievable without requiring a large vertical milling machine.

Stock OD must remain comfortably within the South Bend swing and chuck/workholding capability.

WORKHOLDING

The model should anticipate realistic machining sequence and datum transfer.

Avoid requiring the finished RF bore to be gripped destructively.

Consider:

- soft jaws
- 4-jaw chuck
- faceplate
- expanding/internal mandrel where appropriate
- sacrificial gripping allowance
- external chucking boss removed in final operation

Provide optional sacrificial machining stock parametrically.

FREECAD IMPLEMENTATION

Create:

1. RF_Parameters Spreadsheet.
2. Cavity_Body.
3. End_Cap.
4. Cavity_RF_Volume.
5. Input_Coupler placeholder.
6. Output_Coupler placeholder.
7. Optional Tuning_Screw.
8. Assembly.
9. Machining_Stock reference body.
10. Inspection datums.

Calculate IdealDiameter from TargetFrequency using an expression wherever FreeCAD expression functionality permits.

Keep:

    TargetFrequency

as the primary RF design input.

Allow:

    CavityInnerDiameterCorrection

as an empirical correction parameter so measured first-article behavior can feed back into later versions.

Suggested relation conceptually:

    ActualCADDiameter =
        IdealTM010Diameter
        + DiameterCorrection

Do not silently overwrite theoretical values with empirical ones.

Preserve both.

SIMULATION PREPARATION

Make the RF cavity volume exportable independently as STEP or another appropriate neutral solid.

The RF volume should include:

- internal cavity cylinder
- probe intrusion
- tuning-screw intrusion
- meaningful fillets/radii if included in the manufactured article

Do not clutter the simulation volume with external cosmetic geometry.

METROLOGY PLAN

Make these dimensions easy to identify on drawings:

- cavity ID
- cavity depth
- end-cap internal face position
- register diameter
- register depth
- cap mating-face flatness
- bore cylindricity/roundness where measurable
- probe penetration
- tuning-screw penetration

Record actual manufactured dimensions separately from nominal CAD values.

RF VALIDATION

Eventually compare:

    Predicted resonant frequency
    CAD-derived resonant frequency
    Measured resonant frequency

and, where instrumentation permits:

    loaded Q
    estimated unloaded Q
    S11
    S21
    coupling strength
    resonance bandwidth

The first success criterion is not exceptional Q.

The first success criterion is:

    "A resonance predicted from geometry appears approximately where expected, is repeatably measured, and moves in the predicted direction when a controlled geometric parameter changes."

VERSIONING

Use explicit article/version labels:

    TM010_2450_A0 = theoretical CAD
    TM010_2450_A1 = first manufactured article
    TM010_2450_A2 = geometry corrected from measurement

Preserve measured deviations and VNA results as engineering data associated with each revision.

Do not simply modify the master model until it matches the experiment without recording the correction.

DELIVERABLES

Generate:

- complete FreeCAD model
- RF parameter spreadsheet
- cavity body drawing
- end-cap drawing
- exploded assembly
- cross-sectional RF geometry drawing
- machining-sequence reference
- nominal inspection sheet
- separate RF-volume export body
- table distinguishing theoretical, nominal CAD, and eventually measured dimensions

MVP DEFINITION

MVP is complete when:

1. The cavity body and cap are fully constrained parametrically.
2. Target frequency drives theoretical bore diameter.
3. The geometry is feasible on the South Bend 9x36.
4. Critical RF surfaces are primarily generated by turning/boring/facing.
5. The cap registers repeatably.
6. At least one practical VNA coupling scheme is represented.
7. The RF volume can be exported separately.
8. The design can accept measured frequency/error data without architectural redesign.

Do not optimize for commercial aerospace qualification, maximum Q, exotic plating, or production volume during the MVP.

First establish the closed loop:

    PARAMETRIC DESIGN
        ->
    PHYSICAL ARTICLE
        ->
    METROLOGY
        ->
    RF MEASUREMENT
        ->
    MODEL CORRECTION
