---
title: Thermal Control
slug: thermal-control
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.3.0"
topic_revision: 3
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - module-platform
  - controls-and-software
supersedes: null
---

# Thermal Control

## Purpose

Define how CD35 measures, controls, verifies, protects, services, adds, and rejects heat for process chemistry.

## Normative requirements

- **THM-001** — Process temperature setpoints and tolerances SHALL be derived from the selected chemistry manufacturer's current technical specification and validated in CD35 testing before they are frozen.
- **THM-002** — The developer stage SHALL use closed-loop temperature control.
- **THM-003** — Temperature sensing SHALL measure the working solution or a validated proxy representative of working-solution temperature.
- **THM-004** — The system SHALL prevent processing when a chemistry-critical stage is outside its permitted temperature window.
- **THM-005** — Active heating SHALL include an independent over-temperature protection path that does not rely solely on normal application software.
- **THM-006** — Temperature sensors SHALL be replaceable and calibratable or verifiable against a reference.
- **THM-007** — Circulation or equivalent mixing SHALL be sufficient to prevent unacceptable thermal stratification within temperature-critical baths.
- **THM-008** — The controller SHALL log detected temperature faults during a roll's process cycle.
- **THM-009** — Repeated temperature-sensing and thermal-conditioning functions SHALL use standardized `TSM` Thermal Service Module interfaces or common service cartridges unless process requirements justify a different implementation.
- **THM-010** — Replaceable temperature sensors SHOULD be removable from the service side without opening unrelated electrical assemblies.
- **THM-011** — Heating elements SHOULD be replaceable independently of the wet bath vessel where a validated design can provide the required thermal performance.
- **THM-012** — Thermal service interfaces SHALL define power class, sensor type, connector/pinout, independent thermal-protection behavior, mounting geometry, and thermal-contact geometry before the interface is frozen.
- **THM-013** — A higher-power heater SHALL NOT be made electrically interchangeable with a lower-rated interface unless the controller and wiring are explicitly rated to detect and support it safely.
- **THM-014** — Thermal-module replacement SHALL NOT require recalibration of unrelated baths.
- **THM-015** — Temperature-critical modules SHOULD provide a second independent means of detecting implausible or unsafe temperature when the added complexity materially reduces film-loss or safety risk.
- **THM-016** — Thermal service components SHALL comply with `PBR-007` through `PBR-010`, `PBR-012` through `PBR-019`, and `PBR-030`.
- **THM-017** — The `TSM` interface SHALL represent thermal conditioning rather than heating only and SHALL NOT preclude controlled heat rejection if ambient conditions or process heat loads require it.
- **THM-018** — Active refrigeration, thermoelectric cooling, or another powered cooling method SHALL NOT be required by architecture alone; such hardware SHALL be added only when operating-environment and thermal-load testing demonstrates that passive or fan-assisted heat rejection is insufficient.
- **THM-019** — The preferred first thermal prototype SHALL transfer heat conductively through a defined WBM thermal interface while chemistry circulation provides bulk-solution mixing, unless early testing demonstrates that this architecture cannot meet the required uniformity, recovery, or serviceability targets.
- **THM-020** — The thermal-contact interface between a WBM and TSM SHALL be designed for repeatable contact after module removal/reinstallation and SHALL avoid relying on uncontrolled contact through an arbitrary plastic tank wall.
- **THM-021** — A secondary tempering-water bath or jacket MAY be used as a comparison or fallback architecture, but it SHALL be treated as an additional fluid subsystem with its own containment, drainage, service, and leak risks.
- **THM-022** — A shared thermal backplane or thermal spine MAY serve multiple WBMs only after single-stage testing demonstrates acceptable control authority and after cross-stage thermal coupling effects are characterized.

## `TSM` design direction

The preferred architecture separates the wet chemistry vessel from replaceable thermal hardware while keeping the heat-transfer path deliberate and testable.

### Preferred prototype: conductive thermal interface

```text
WBM / CHEMISTRY
~~~~~~~~~~~~~~~~~~~~~~~~
| circulation / mixing |
|                     |
| chemistry            |
|_____________________|
| defined thermal face |
=======================   <- repeatable thermal interface
| heat spreader / TSM  |
| heater cartridge(s)  |
| sensor / protection  |
=======================
          |
          +---- optional heat-rejection path if later required
```

The concept is **conduction plus circulation**, not conduction alone. The thermal surface transfers energy into or out of the bath; the fluid system distributes that energy through the working solution.

Advantages if validated:

- no secondary tempering-water circuit;
- no immersed electrical heater body required;
- WBM can remain largely passive;
- heater, sensor, and protective devices remain dry-side service items;
- TSM can use commodity heater/sensor components behind a standardized interface;
- the same thermal interface can support later fan/radiator or other heat-rejection hardware if required.

The exact thermal-face material, thickness, contact pressure, heat spreader, interface compound/pad if any, and heater geometry remain TBD.

### Comparison architecture: tempering-water bath or jacket

```text
thermal water / heat-transfer fluid
┌───────────────────────────────┐
│       ┌───────────────┐       │
│       │ process chem  │       │
│       │     WBM       │       │
│       └───────────────┘       │
│ heater / circulation / sensor │
└───────────────────────────────┘
```

This approach may provide excellent uniformity and naturally supports heat addition/removal, but it creates a second fluid system with added thermal mass, plumbing, leak containment, cleaning, warm-up, and service requirements. It remains the principal comparison/fallback architecture rather than the preferred first prototype.

### Alternative: chemistry-side external heat exchanger

An external recirculating chemistry heat exchanger remains a fallback if conductive coupling cannot provide sufficient heat transfer or temperature uniformity. This architecture adds wetted volume, seals, plumbing, and cleaning burden and therefore requires a demonstrated performance advantage before selection.

## Heat rejection and cooling

The processor target temperature is expected to be above normal room temperature, so the first heat-rejection strategy should use the available temperature difference to ambient rather than assume refrigeration.

Candidate heat-rejection sequence:

```text
WBM thermal face
      |
      v
TSM / heat spreader
      |
      v
heat sink or radiator
      |
      v
controlled airflow
      |
      v
room air
```

This is a candidate implementation, not a frozen fan/radiator requirement. Environmental tests will determine whether natural convection, fan-assisted cooling, or more active cooling is necessary.

## Sensor direction

Industrial RTD sensing such as PT100/PT1000-class probes or an equivalent verified technology remains the preferred candidate because replaceable probes, documented tolerances, and standard instrumentation are widely available. Exact sensor class, wiring method, and connector remain TBD.

## Interfaces

- `module-platform` defines the TSM service boundary and commonization rules.
- `wet-process-modules` provides the WBM receiving thermal surface/interface.
- `fluid-handling` provides chemistry circulation used to distribute thermal energy.
- `controls-and-software` commands thermal state and handles faults/interlocks.

## Prototype sequence

Thermal development should begin with a single representative WBM containing water or another safe test fluid:

1. defined conductive thermal face;
2. candidate TSM heater and sensor;
3. representative FSM circulation loop;
4. multiple independent temperature probes distributed through the bath;
5. controlled tests for warm-up, steady-state uniformity, replenishment disturbance, recovery, heat rejection, and module redocking.

Only after single-stage behavior is understood should a shared multi-bath thermal backplane be evaluated.

## Validation

Validation shall eventually measure:

- absolute sensor error against a known reference;
- sensor-to-sensor plausibility if dual sensing is used;
- temperature uniformity at multiple bath locations;
- warm-up time;
- overshoot after startup and replenishment;
- recovery after film and fluid loading;
- thermal lag from heater command to working solution;
- conductive interface repeatability after WBM removal/reinstallation;
- heater removal/replacement repeatability;
- sensor replacement and calibration repeatability;
- heat-rejection capacity across the specified ambient-temperature range;
- sensor-open, sensor-short, stuck-heater, blocked-circulation, and control-failure behavior.

## Open questions

- Thermal-face material, geometry, attachment, and contact-pressure method.
- Final sensor technology and connector standard.
- Required absolute accuracy and stability after chemistry selection.
- Heater wattage/power classes.
- Whether developer uses dual independent sensors in production hardware.
- Whether downstream baths need active heating, shared thermal coupling, monitoring only, or another arrangement.
- Standard TSM mechanical envelope.
- Whether fan-assisted heat rejection is required at the defined maximum ambient temperature.
- Whether the tempering-water architecture materially outperforms conductive coupling enough to justify its second fluid circuit.