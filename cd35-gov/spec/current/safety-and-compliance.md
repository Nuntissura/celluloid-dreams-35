---
title: Safety and Compliance
slug: safety-and-compliance
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.3.0"
topic_revision: 2
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - system-architecture
  - thermal-control
  - controls-and-software
  - fluid-handling
supersedes: null
---

# Safety and Compliance

## Purpose

Define safety constraints for a machine combining photographic chemistry, heated liquids, electrical power, powered transport, and a light-tight enclosure.

## Normative requirements

- **SAF-001** — Electrical components SHALL be protected from foreseeable chemistry leaks, splashes, condensation, and wash water.
- **SAF-002** — Mains-voltage assemblies SHALL be enclosed and protected from normal operator access.
- **SAF-003** — Heated stages SHALL include over-temperature protection independent of normal software control.
- **SAF-004** — Powered transport SHALL be guarded against hazardous access during normal operation.
- **SAF-005** — Access panels or doors exposing hazardous moving parts or live electrical assemblies SHALL use appropriate interlocks or require a service procedure that removes the hazard.
- **SAF-006** — Fluid connections SHALL be arranged to reduce the probability of incompatible chemistry being accidentally mixed.
- **SAF-007** — Materials in the fluid path SHALL be assessed for chemical compatibility with the assigned process solutions.
- **SAF-008** — The machine SHALL provide a controlled response to leak detection where leakage could reach electrical or mechanically hazardous areas.
- **SAF-009** — Required ventilation and operator exposure controls SHALL be determined from the safety data and technical requirements of the selected chemistry.
- **SAF-010** — Applicable product-safety, electrical, EMC, environmental, and workplace requirements for the intended sales/use region SHALL be identified before production hardware is frozen.
- **SAF-011** — The wet section SHALL include secondary containment, drainage, or equivalent geometry capable of keeping foreseeable service leakage away from energized dry-side assemblies long enough for detection and controlled response.
- **SAF-012** — A low-liquid condition SHALL disable any heater, pump, or other function for which dry or partially dry operation creates a credible thermal, mechanical, or process hazard.
- **SAF-013** — Optional heat-rejection or cooling hardware SHALL fail in a manner that does not defeat independent over-temperature protection.
- **SAF-014** — A shared thermal backplane, if adopted, SHALL be analyzed for fault propagation so a single thermal-control failure cannot silently overheat multiple chemistry stages beyond their validated safe limits.

## Current design direction

Safety should be layered:

1. physical separation of wet and electrical zones;
2. wet-zone containment and deliberate drainage;
3. level and leak sensing where useful;
4. hardware protection such as fuses and thermal cut-outs;
5. door/cover interlocks;
6. software monitoring and diagnostics.

Software alarms are supplementary controls, not substitutes for basic physical protection.

A shallow service/containment tray beneath the wet modules is the preferred initial leak-management architecture. Exact volume, drainage, sensor placement, and chemical compatibility remain TBD.

## Open questions

- Intended first market and therefore regulatory framework.
- Mains architecture: direct mains subsystems versus centralized low-voltage power distribution.
- Leak-sensor placement and technology.
- Required emergency-stop behavior.
- Ventilation requirements for selected chemistry and installation environment.
- Waste-chemistry handling requirements.
- Required containment volume and whether containment is stage-local or common across the wet section.
