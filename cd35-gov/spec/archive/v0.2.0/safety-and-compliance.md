---
title: Safety and Compliance
slug: safety-and-compliance
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.1.0"
topic_revision: 1
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - system-architecture
  - thermal-control
  - controls-and-software
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

## Current design direction

Safety should be layered:

1. physical separation of wet and electrical zones;
2. containment and drainage;
3. hardware protection such as fuses and thermal cut-outs;
4. door/cover interlocks;
5. software monitoring and diagnostics.

Software alarms are supplementary controls, not substitutes for basic physical protection.

## Open questions

- Intended first market and therefore regulatory framework.
- Mains architecture: direct mains subsystems versus centralized low-voltage power distribution.
- Leak-sensor placement and technology.
- Required emergency-stop behavior.
- Ventilation requirements for selected chemistry and installation environment.
- Waste-chemistry handling requirements.
