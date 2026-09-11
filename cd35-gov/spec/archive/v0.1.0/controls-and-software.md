---
title: Controls and Software
slug: controls-and-software
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
  - wet-process-modules
  - thermal-control
supersedes: null
---

# Controls and Software

## Purpose

Define the control system responsible for sequencing, module coordination, interlocks, process tracking, diagnostics, and operator interaction.

## Normative requirements

- **CTL-001** — The control system SHALL coordinate intake, transport, wet stages, thermal control, drying, and fault handling as one deterministic process sequence.
- **CTL-002** — Safety-critical interlocks SHALL fail to a defined safe state and SHALL NOT depend solely on a graphical user interface.
- **CTL-003** — The controller SHALL prevent a process start when required modules, temperatures, levels, covers, or interlocks are not in a valid state.
- **CTL-004** — The controller SHOULD identify installed process modules and detect an invalid module sequence where module identification is available.
- **CTL-005** — Process parameters SHALL be stored as explicit recipes/configuration rather than hidden constants in application logic.
- **CTL-006** — A roll or transport carrier SHALL be trackable through the process sufficiently to associate faults with affected film.
- **CTL-007** — The system SHALL record process-critical faults including transport stalls and temperature excursions.
- **CTL-008** — Firmware/software updates SHALL preserve a recoverable known-good configuration or provide a documented recovery path.
- **CTL-009** — Commodity or openly documented communication buses and interfaces SHOULD be preferred over undocumented proprietary protocols.
- **CTL-010** — Loss of the main user interface SHALL NOT disable essential thermal or mechanical protection functions.

## Current design direction

A distributed architecture is preferred over one custom board controlling every function. Candidate structure:

```text
operator UI / supervisory controller
              |
        machine control bus
    _________|___________
   |         |           |
intake   transport   wet/thermal nodes
```

Possible implementations include an industrial PLC, embedded controller network, or hybrid architecture. No controller family is frozen yet.

## Process data

A process record should eventually be able to associate at least:

- job/roll identifier;
- recipe version;
- start/end time;
- measured temperatures;
- transport faults;
- module identity/configuration;
- operator-visible warnings.

## Open questions

- PLC versus embedded MCU architecture.
- CAN, RS-485, Ethernet, or mixed bus.
- Touchscreen size and operator workflow.
- Local-only versus optional network logging.
- Recipe authorization and calibration permissions.
