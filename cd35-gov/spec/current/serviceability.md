---
title: Serviceability and Modularity
slug: serviceability
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
  - system-architecture
  - module-platform
  - wet-process-modules
  - film-transport
  - thermal-control
  - fluid-handling
supersedes: null
---

# Serviceability and Modularity

## Purpose

Define product-level maintainability requirements that apply the `PBR-*` build rules to the CD35 processor.

## Normative requirements

- **SRV-001** — Components that routinely contact processing chemistry SHALL be removable, cleanable, or replaceable without dismantling the complete processor.
- **SRV-002** — Repeated motors, pumps, sensors, heaters, valves, connectors, rollers, bearings/bushings, and drive electronics SHALL use standardized part or module families unless a documented requirement justifies divergence.
- **SRV-003** — Routine replacement parts SHOULD be commercially available components with documented specifications rather than project-unique parts where no technical advantage justifies uniqueness.
- **SRV-004** — A failed field-replaceable module SHOULD be exchangeable so production can resume before component-level repair is completed.
- **SRV-005** — Service connectors SHALL be keyed, labeled, or mechanically differentiated where an incorrect connection could damage the machine, contaminate chemistry, or create a safety hazard.
- **SRV-006** — Wear components SHALL be accessible for visual inspection.
- **SRV-007** — Calibration procedures for critical sensors SHALL be documented and executable without proprietary external service software where practical.
- **SRV-008** — The project SHALL maintain interface documentation sufficient to source, repair, redesign, or manufacture compatible replacement modules.
- **SRV-009** — Routine cleaning SHALL NOT require removal of unrelated electrical assemblies.
- **SRV-010** — Each field-replaceable production module SHALL carry a human-readable module type and interface revision.
- **SRV-011** — Module replacement procedures SHALL identify required tools, isolation steps, calibration/check steps, and expected post-replacement verification.
- **SRV-012** — Service-critical custom adapters or manufactured parts SHOULD have drawings or source design files retained with the project.
- **SRV-013** — Mean-time-to-repair targets SHALL be defined for TDM, TRM, TSM, FSM, and WBM replacement before production maturity.
- **SRV-014** — No service procedure SHALL intentionally defeat a required safety interlock without an explicitly documented maintenance mode and hazard control.
- **SRV-015** — A `TRM` SHALL be removable for cleaning, inspection, or exchange without removing the associated dry-side `TDM`.
- **SRV-016** — Standardized service cartridges such as temperature probes, level sensors, heater cartridges, pump cartridges, and filters SHOULD be replaceable without replacing their parent WBM, TSM, or FSM when the component is a likely wear/failure item and independent replacement is practical.

## Standard field-replaceable units

The current service model recognizes at least:

- `TDM` — Transport Drive Module;
- `TRM` — Transport Rack Module;
- `TSM` — Thermal Service Module;
- `FSM` — Fluid Service Module;
- `WBM` — Wet Bath Module;
- crossover assembly;
- temperature-probe cartridge;
- level-sensor cartridge;
- heater cartridge where independently replaceable;
- pump or replenishment-metering cartridge where independently replaceable;
- filter cartridge;
- control node where independently replaceable.

## Design principle

> A likely failure should be replaceable at its natural service boundary without making the rest of the machine part of the repair.

This principle is subordinate to safety and process integrity but should drive mechanical layout and interface design.

## Validation

Serviceability tests should record:

- replacement time;
- tools required;
- spill volume or chemical exposure;
- need for recalibration;
- alignment repeatability;
- connector/coupling error opportunities;
- whether adjacent modules are disturbed;
- whether a spare module actually restores operation.

TRM tests should additionally verify that cleaning/replacement does not disturb TDM alignment and that independently assembled racks return the film path to the specified datum.

## Open questions

- Replacement-time targets for each module class and service cartridge.
- Which interfaces can be tool-free versus common-tool.
- Recommended on-site spare module/cartridge set.
- Which custom parts are justified because commodity options cannot meet chemistry, geometry, reliability, or safety requirements.