---
title: System Architecture
slug: system-architecture
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
  - scope-and-goals
supersedes: null
---

# System Architecture

## Purpose

Define the top-level CD35 subsystem structure and the boundaries between standardized replaceable modules.

## Normative requirements

- **SYS-001** — The processor SHALL be organized as replaceable functional subsystems with defined mechanical, electrical, fluid, thermal, data, and service interfaces where applicable.
- **SYS-002** — The exposed-film path SHALL remain light-tight from film acquisition until the process has reached a stage demonstrated to be safe for ambient-light exposure.
- **SYS-003** — The initial architecture SHALL provide functions for intake, development, downstream C-41 processing, washing/rinsing, drying, control, and fault handling.
- **SYS-004** — Routine service of one wet stage SHOULD NOT require dismantling or draining unrelated wet stages.
- **SYS-005** — Repeated module interfaces SHALL use standardized connectors, mountings, and service boundaries according to `module-platform.md` and `PBR-*`.
- **SYS-006** — The system SHALL enter a defined safe state on loss of control power, transport fault, over-temperature condition, or detected access to a light-sensitive path.
- **SYS-007** — Critical transport, thermal, and fluid-service interfaces SHALL be defined before the final external machine shape is frozen.
- **SYS-008** — Likely service-failure components SHOULD be located in dry/service-accessible modules rather than integrated permanently into chemistry vessels where process performance permits.
- **SYS-009** — Wet bath modules SHALL interface to transport-rack, drive, thermal, and fluid-service subsystems through separately serviceable boundaries where practical.
- **SYS-010** — Architecture decisions SHALL follow the commodity-first and repairability constraints in `PBR-001` through `PBR-035`.
- **SYS-011** — Wet film-path hardware SHALL be represented by the `TRM` service boundary separately from the `WBM` vessel and `TDM` drive source.
- **SYS-012** — Thermal architecture SHALL treat heat addition, temperature measurement, protection, and optional heat rejection as one `TSM` service domain rather than defining cooling as a separate mandatory top-level module.
- **SYS-013** — Level sensing and leak detection SHALL use standardized service interfaces but SHALL NOT become separate top-level module classes unless later engineering evidence shows a distinct service boundary is beneficial.

## Current architecture

```text
                                      dry/service side
                         ┌──── TDM: transport drive
                         │
Cassette -> Intake -> [ WBM ] -> [ WBM ] -> [ WBM ] -> Wash/Rinse -> Dryer
                         │           │           │
                         ├──── TRM   ├──── TRM   ├──── TRM
                         ├──── TSM   ├──── TSM   ├──── TSM
                         └──── FSM   └──── FSM   └──── FSM

TDM = Transport Drive Module
TRM = Transport Rack Module
TSM = Thermal Service Module
FSM = Fluid Service Module
WBM = Wet Bath Module
```

The conceptual service split at one stage is:

```text
          [TDM]
            |
       drive coupling
            |
          [TRM]
            |
        film path
            |
   ┌─────────────────┐
   │       WBM       │
   │ chemistry vessel│
   └─────────────────┘
       |          |
      FSM        TSM
   circulation  thermal
```

The diagram defines service boundaries, not final module count or geometry.

## Thermal architecture direction

The preferred first prototype uses conductive coupling between a WBM thermal face and a dry-side TSM, combined with solution circulation for bulk temperature uniformity.

A tempering-water bath/jacket remains the principal comparison and fallback architecture. It is not preferred initially because it introduces a second fluid circuit and associated plumbing, thermal mass, containment, and service burden.

The TSM boundary includes the possibility of heat rejection, but active refrigeration is not presumed necessary. Environmental and thermal-load testing will determine whether natural, fan-assisted, or more active cooling is required.

## Design sequence

The current priority order is:

1. validate TDM and TRM mechanical interfaces and film transport behavior;
2. validate conductive WBM/TSM thermal coupling with representative circulation;
3. compare thermal performance against a tempering-water reference if required;
4. validate fluid import/extraction/circulation and FSM/port interface;
5. validate WBM docking, level sensing, and wet-zone containment around those interfaces;
6. integrate daylight intake, crossovers, and drying;
7. optimize chassis and final enclosure shape after critical subsystem interfaces are stable.

This sequence implements `PBR-006`: external shape is deliberately deferred.

## Interfaces

The architecture depends on:

- `module-platform` for common module rules;
- `film-transport` for TDM/TRM behavior;
- `thermal-control` for TSM behavior;
- `fluid-handling` for FSM, level sensing, leak routing, and fluid-port behavior;
- `wet-process-modules` for WBM behavior;
- `daylight-intake` for safe film acquisition;
- `controls-and-software` for coordination and interlocks.

## Open questions

- Primary wet-film transport mechanism.
- Standard mechanical rail/datum system.
- Exact WBM process geometry and count.
- TRM rack datum and drive-coupling standard.
- Conductive thermal-interface geometry and heat-spreader material.
- Whether any shared multi-stage thermal spine is justified after single-stage validation.
- Required heat-rejection hardware at maximum specified ambient temperature.
- FSM pump/coupling architecture.
- Point in the process at which the enclosure may transition from light-tight to ambient-service access.