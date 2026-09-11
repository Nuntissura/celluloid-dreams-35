---
title: Wet-Process Modules
slug: wet-process-modules
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
  - film-transport
supersedes: null
---

# Wet-Process Modules

## Purpose

Define the interchangeable bath modules that contain processing chemistry, circulation, sensing, drainage, and the local film path.

## Normative requirements

- **WET-001** — Wet-process stages SHALL use a standardized replaceable module architecture wherever stage-specific chemistry does not make that impractical.
- **WET-002** — A wet module SHALL provide a defined mechanical docking interface to the processor chassis.
- **WET-003** — A wet module SHALL provide a controlled means to drain or extract its working solution without tipping or removing the full machine.
- **WET-004** — Routine chemistry replacement SHALL be possible without dismantling unrelated processor assemblies.
- **WET-005** — Each chemistry-bearing module SHALL provide temperature measurement appropriate to its process requirement.
- **WET-006** — Modules requiring active heating SHALL provide a standardized heater/control interface or contain a replaceable local heater subsystem.
- **WET-007** — Modules requiring circulation SHALL provide a serviceable circulation path and pump interface.
- **WET-008** — Chemical-contact materials SHALL be selected and validated for compatibility with the chemistry assigned to that module.
- **WET-009** — Fluid drain and service connections SHOULD minimize uncontrolled spills and accidental cross-connection.
- **WET-010** — The design SHOULD permit rapid exchange of a complete wet module for cleaning, chemistry change, troubleshooting, or service.
- **WET-011** — The system SHOULD be capable of identifying the installed module or its assigned process role so incorrect stage placement can be detected.

## Current design direction

A common wet-module standard is preferred over unique developer, bleach, fixer, and rinse tank hardware. Differences should be configuration-driven where possible.

Candidate module features:

```text
┌─────────────────────────────┐
│ standardized wet module     │
│                             │
│ removable transport rack    │
│ working bath                │
│ temperature sensor          │
│ level sensing               │
│ circulation / filtration    │
│ heater where required       │
│ drain / service coupling    │
│ replenishment connection    │
│ module identity             │
└─────────────────────────────┘
```

A simple tap may be acceptable for an early prototype. A keyed dry-break or similarly spill-resistant coupling is the preferred production direction if testing supports it.

## Interfaces

- Chassis: mounting, alignment, service access.
- Transport: removable rack/guide geometry and drive coupling.
- Controls: temperature, level, identity, pump/heater control.
- Fluid service: fill, drain, replenishment, overflow where required.

## Open questions

- Working volume per module.
- Common module dimensions.
- Integrated versus external circulation pump.
- Whether wash modules should use the same physical cartridge standard as chemistry modules.
- Replenishment strategy and replenishment-rate measurement.
- Filter type and service interval.
- Best dry-break coupling family for chemistry compatibility and cost.
