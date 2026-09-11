---
title: Thermal Control
slug: thermal-control
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.2.0"
topic_revision: 2
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

Define how CD35 measures, controls, verifies, protects, and services process temperature.

## Normative requirements

- **THM-001** — Process temperature setpoints and tolerances SHALL be derived from the selected chemistry manufacturer's current technical specification and validated in CD35 testing before they are frozen.
- **THM-002** — The developer stage SHALL use closed-loop temperature control.
- **THM-003** — Temperature sensing SHALL measure the working solution or a validated proxy representative of working-solution temperature.
- **THM-004** — The system SHALL prevent processing when a chemistry-critical stage is outside its permitted temperature window.
- **THM-005** — Active heating SHALL include an independent over-temperature protection path that does not rely solely on normal application software.
- **THM-006** — Temperature sensors SHALL be replaceable and calibratable or verifiable against a reference.
- **THM-007** — Circulation or equivalent mixing SHALL be sufficient to prevent unacceptable thermal stratification within temperature-critical baths.
- **THM-008** — The controller SHALL log detected temperature faults during a roll's process cycle.
- **THM-009** — Repeated temperature-sensing and heating functions SHALL use standardized `TSM` Thermal Service Module interfaces or common service cartridges unless process requirements justify a different implementation.
- **THM-010** — Replaceable temperature sensors SHOULD be removable from the service side without opening unrelated electrical assemblies.
- **THM-011** — Heating elements SHOULD be replaceable independently of the wet bath vessel where a validated design can provide the required thermal performance.
- **THM-012** — Thermal service interfaces SHALL define power class, sensor type, connector/pinout, independent thermal-protection behavior, and mounting geometry before the interface is frozen.
- **THM-013** — A higher-power heater SHALL NOT be made electrically interchangeable with a lower-rated interface unless the controller and wiring are explicitly rated to detect and support it safely.
- **THM-014** — Thermal-module replacement SHALL NOT require recalibration of unrelated baths.
- **THM-015** — Temperature-critical modules SHOULD provide a second independent means of detecting implausible or unsafe temperature when the added complexity materially reduces film-loss or safety risk.
- **THM-016** — Thermal service components SHALL comply with `PBR-007` through `PBR-010`, `PBR-012` through `PBR-019`, and `PBR-030`.

## `TSM` design direction

The preferred architecture separates the wet vessel from replaceable heating and sensing hardware as far as thermal performance permits.

A strong candidate is a **dry-well thermal interface**:

```text
SERVICE SIDE                 WET BATH

[heater cartridge] ---> | sealed thermal well | ~ chemistry
[temp probe]       ---> | sealed sensor well  | ~ chemistry
```

Advantages if validated:

- heater and sensor can be replaced without exposing their electrical bodies to chemistry;
- the wet bath can remain a simpler passive vessel;
- service does not require cutting wiring or draining unrelated stages;
- multiple bath modules can share the same heater/sensor cartridge families.

This is a candidate architecture, not a frozen requirement. Thermal lag, heat flux, temperature uniformity, cleanability, well-material compatibility, and failure behavior must be tested.

An external circulation heat exchanger is the main alternative if dry-well heating cannot meet uniformity or recovery requirements efficiently.

## Sensor direction

Industrial RTD sensing such as PT100/PT1000-class probes or an equivalent verified technology remains the preferred candidate because replaceable probes, documented tolerances, and standard instrumentation are widely available. Exact sensor class, wiring method, and connector remain TBD.

## Validation

Validation shall eventually measure:

- absolute sensor error against a known reference;
- sensor-to-sensor plausibility if dual sensing is used;
- temperature uniformity at multiple bath locations;
- warm-up time;
- overshoot after startup and replenishment;
- recovery after film and fluid loading;
- dry-well or heat-exchanger thermal lag;
- heater removal/replacement repeatability;
- sensor replacement and calibration repeatability;
- sensor-open, sensor-short, stuck-heater, and control-failure behavior.

## Open questions

- Dry-well heater versus external recirculating heat exchanger.
- Final sensor technology and connector standard.
- Required absolute accuracy and stability after chemistry selection.
- Heater wattage/power classes.
- Whether developer uses dual independent sensors in production hardware.
- Whether downstream baths need active heating or only monitoring.
- Standard TSM mechanical envelope and service access.