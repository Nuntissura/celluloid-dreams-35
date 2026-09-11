---
title: System Architecture
slug: system-architecture
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
  - scope-and-goals
supersedes: null
---

# System Architecture

## Purpose

Define the top-level CD35 subsystem structure and the boundaries between standardized replaceable modules.

## Normative requirements

- **SYS-001** — The processor SHALL be organized as replaceable functional subsystems with defined mechanical, electrical, fluid, data, and service interfaces where applicable.
- **SYS-002** — The exposed-film path SHALL remain light-tight from film acquisition until the process has reached a stage demonstrated to be safe for ambient-light exposure.
- **SYS-003** — The initial architecture SHALL provide functions for intake, development, downstream C-41 processing, washing/rinsing, drying, control, and fault handling.
- **SYS-004** — Routine service of one wet stage SHOULD NOT require dismantling or draining unrelated wet stages.
- **SYS-005** — Repeated module interfaces SHALL use standardized connectors, mountings, and service boundaries according to `module-platform.md` and `PBR-*`.
- **SYS-006** — The system SHALL enter a defined safe state on loss of control power, transport fault, over-temperature condition, or detected access to a light-sensitive path.
- **SYS-007** — Critical transport, thermal, and fluid-service interfaces SHALL be defined before the final external machine shape is frozen.
- **SYS-008** — Likely service-failure components SHOULD be located in dry/service-accessible modules rather than integrated permanently into chemistry vessels where process performance permits.
- **SYS-009** — Wet bath modules SHALL interface to transport, thermal, and fluid-service subsystems through separately serviceable boundaries where practical.
- **SYS-010** — Architecture decisions SHALL follow the commodity-first and repairability constraints in `PBR-001` through `PBR-035`.

## Current design direction

The current architecture separates the **wet bath** from the high-service hardware around it:

```text
                         ┌──── TDM: transport drive
                         │
Cassette -> Intake -> [ WBM ] -> [ WBM ] -> [ WBM ] -> Wash/Rinse -> Dryer
                         │           │           │
                         ├──── TSM   ├──── TSM   ├──── TSM
                         │           │           │
                         └──── FSM   └──── FSM   └──── FSM

TDM = Transport Drive Module
TSM = Thermal Service Module
FSM = Fluid Service Module
WBM = Wet Bath Module
```

The diagram defines service boundaries, not final module count or geometry.

## Design sequence

The current priority order is:

1. validate film transport and TDM interface;
2. validate thermal sensing/heating and TSM interface;
3. validate fluid import/extraction/circulation and FSM/port interface;
4. validate WBM docking around those interfaces;
5. integrate daylight intake, crossovers, and drying;
6. optimize chassis and final enclosure shape after critical subsystem interfaces are stable.

This sequence implements `PBR-006`: external shape is deliberately deferred.

## Interfaces

The architecture depends on:

- `module-platform` for common module rules;
- `film-transport` for film movement and TDM behavior;
- `thermal-control` for TSM behavior;
- `fluid-handling` for FSM and fluid-port behavior;
- `wet-process-modules` for WBM behavior;
- `daylight-intake` for safe film acquisition;
- `controls-and-software` for coordination and interlocks.

## Open questions

- Primary wet-film transport mechanism.
- Standard mechanical rail/datum system.
- Exact WBM process geometry and count.
- TSM dry-well versus external heat-exchanger architecture.
- FSM pump/coupling architecture.
- Point in the process at which the enclosure may transition from light-tight to ambient-service access.