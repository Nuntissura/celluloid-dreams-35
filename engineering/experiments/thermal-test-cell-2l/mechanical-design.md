---
title: TTC-2L-A Mechanical Design
project: CD35
document_type: experiment-design
status: draft
revision: "0.1"
last_updated: 2026-09-11
---

# TTC-2L-A Mechanical Design

## Coordinate system

Use this coordinate system for all prototype drawings and sensor/port locations:

- `X`: 0–200 mm across bath width;
- `Y`: 0–75 mm from thermal-window wall toward the opposite wall;
- `Z`: 0–160 mm from bath floor upward.

The thermal window is in the `Y = 0` wall.

## TTC-MEC requirements

- **TTC-MEC-001** — The internal water chamber shall be `200 × 75 × 160 mm` for the first build.
- **TTC-MEC-002** — The nominal 2.00 L water line shall be marked at `Z = 133.3 mm`.
- **TTC-MEC-003** — The first bath body shall be transparent so circulation, bubbles, leaks and sensor placement can be observed directly.
- **TTC-MEC-004** — The bath body material is a test-fixture choice only and shall not be treated as a chemistry-compatibility decision.
- **TTC-MEC-005** — The WBM shall have a replaceable metal thermal window rather than an integral immersed electrical heater.
- **TTC-MEC-006** — The first thermal active opening shall be `160 × 100 mm`, positioned so it remains fully submerged at the nominal 2 L fill.
- **TTC-MEC-007** — The window plate shall overlap the active opening by at least 10 mm on all sides for gasket compression and fastener load transfer.
- **TTC-MEC-008** — The starting thermal-window coupon shall be approximately 0.5 mm stainless sheet; material and thickness are experimental variables.
- **TTC-MEC-009** — The thermal-window seal shall be mechanical and replaceable; permanent adhesive shall not be required to exchange the window coupon.
- **TTC-MEC-010** — The TSM contact plate shall dock against the dry side of the thermal window through an interchangeable thermal-interface layer.
- **TTC-MEC-011** — WBM redocking shall use hard mechanical datums independent of the thermal pad so pad compression does not define module position.
- **TTC-MEC-012** — Docking force shall be spring-controlled or otherwise repeatable rather than dependent only on operator hand force.
- **TTC-MEC-013** — The prototype shall permit at least ten WBM undock/redock cycles without replacing the thermal window, gasket or primary docking hardware.
- **TTC-MEC-014** — Any leak at the thermal-window seal shall have a gravity path into a containment tray before reaching the TSM electrical connections.

## Bath construction

### Starting construction

For the water-only fixture, use a simple transparent fabricated tank. A practical starting construction is:

- 6–8 mm clear cast acrylic or polycarbonate walls;
- thicker local reinforcement around the thermal-window opening;
- removable top sensor rail rather than a fully sealed lid;
- rigid base plate locating the vessel relative to the TSM.

The transparent polymer is intentionally a fixture material. It makes flow and leakage visible and can be replaced later without invalidating the thermal-interface concept.

### Internal volume

```text
internal width  = 200 mm
internal depth  =  75 mm
nominal fill    = 133.3 mm

V = 200 × 75 × 133.3 mm³
  ≈ 2,000,000 mm³
  ≈ 2.00 L
```

The remaining ~26.7 mm provides freeboard for circulation and disturbance tests.

## Thermal window

### Starting geometry

- active opening: `160 × 100 mm`;
- window coupon: target around `180 × 120 mm`;
- starting coupon thickness: `0.5 mm`;
- gasket: continuous perimeter gasket outside the active opening;
- retain with a bolted clamp frame rather than relying on adhesive bonding.

The central 160 × 100 mm region is the experimental heat-transfer area. At that area, nominal heat flux is approximately:

| Heater input | Average heat flux over 160 × 100 mm |
|---:|---:|
| 150 W | 9.4 kW/m² |
| 300 W | 18.8 kW/m² |
| 450 W | 28.1 kW/m² |

These are bench test conditions, not production heat-flux requirements.

## TSM thermal stack

Starting stack, wet to dry:

```text
water
  |
0.5 mm replaceable metal thermal window
  |
interchangeable interface layer
(dry contact / thin pad / benchmark compound)
  |
180 × 120 × 12 mm aluminium spreader/heater block
  |
replaceable heater elements
  |
insulating rear cover / guarded dry enclosure
```

### Spreader/heater block

Target first machining envelope: `180 × 120 × 12 mm` aluminium.

The block should support multiple replaceable heater elements rather than one permanently bonded heater. The preferred test implementation is three independently wired low-voltage heater positions so nominal power can be stepped without rebuilding the cell.

Target power states:

- ~150 W;
- ~300 W nominal;
- ~450 W maximum test condition.

Final heater diameter, length and bore dimensions shall be taken from sourced heater datasheets before machining. Do not reverse-engineer a heater dimension from an assumed catalogue pattern.

## Docking mechanism

### Datums

Use three independent location constraints:

1. flat base datum for vertical location;
2. one round locating pin for X/Y registration;
3. one slotted/diamond-style locator for rotation without overconstraint.

The thermal interface shall not be the locating datum.

### Clamping

Prototype target: four spring-loaded clamp points around the thermal interface, with a hard stop controlling final dock position.

Initial total clamp-force design space: roughly `400–800 N` over the interface. The exact value remains experimental; the important feature is repeatability between dock cycles.

Preferred bench arrangement:

- captive M6 clamp screws or equivalent;
- compression/Belleville springs;
- fixed compression distance or hard stop;
- witness marks or measured spring compression for repeatability.

Do not use a freehand clamp as the sole definition of interface pressure for the redocking test.

## Ports

Use removable prototype ports, not final CD35 coupling hardware.

Starting fluid connection size: approximately 8 mm ID hose.

Proposed locations:

| Function | Approximate location | Rationale |
|---|---|---|
| `SUCTION` | X≈180, Y≈10, Z≈20 mm | low and close to heated side |
| `RETURN` | X≈20, Y≈65, Z≈105 mm | opposite upper corner to force bulk sweep |
| service drain | low side wall near Z≈5–10 mm | simple emptying into container |

Port positions shall remain movable during testing. If the flow pattern creates dead zones or aeration, change port geometry before changing thermal architecture.

## Sensor support

Provide a removable top rail with sliding probe clamps so T1/T2/T3 positions can be changed without drilling the tank.

Starting measurement coordinates:

| Sensor | X | Y | Z | Function |
|---|---:|---:|---:|---|
| `T1` | 170 | 10 | 30 | near thermal interface |
| `T2` | 100 | 38 | 70 | bulk/control location |
| `T3` | 30 | 65 | 115 | upper far zone |

Coordinates are starting positions, not frozen acceptance positions.

## Containment and frame

Mount WBM, TSM and circulation hardware to a rigid bench base, preferably aluminium extrusion or a plate fixture. A removable drip tray shall cover the entire wet-side footprint and extend below the thermal-window interface.

The mains-powered PSU, laptop/logger and any exposed mains switching shall remain outside the containment footprint.