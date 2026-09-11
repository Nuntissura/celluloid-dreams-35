---
title: Controls and Software
slug: controls-and-software
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
  - film-transport
  - wet-process-modules
  - thermal-control
  - fluid-handling
supersedes: null
---

# Controls and Software

## Purpose

Define the control system responsible for sequencing, module coordination, interlocks, process tracking, diagnostics, and operator interaction.

## Normative requirements

- **CTL-001** — The control system SHALL coordinate intake, transport, wet stages, thermal control, fluid handling, drying, and fault handling as one deterministic process sequence.
- **CTL-002** — Safety-critical interlocks SHALL fail to a defined safe state and SHALL NOT depend solely on a graphical user interface.
- **CTL-003** — The controller SHALL prevent a process start when required modules, temperatures, levels, covers, or interlocks are not in a valid state.
- **CTL-004** — The controller SHOULD identify installed process modules and detect an invalid module sequence where module identification is available.
- **CTL-005** — Process parameters SHALL be stored as explicit recipes/configuration rather than hidden constants in application logic.
- **CTL-006** — A roll or transport carrier SHALL be trackable through the process sufficiently to associate faults with affected film.
- **CTL-007** — The system SHALL record process-critical faults including transport stalls, invalid liquid levels, detected leaks, and temperature excursions.
- **CTL-008** — Firmware/software updates SHALL preserve a recoverable known-good configuration or provide a documented recovery path.
- **CTL-009** — Commodity or openly documented communication buses and interfaces SHOULD be preferred over undocumented proprietary protocols.
- **CTL-010** — Loss of the main user interface SHALL NOT disable essential thermal, fluid, or mechanical protection functions.
- **CTL-011** — Heater enable and circulation enable SHALL be inhibited when the associated stage reports an invalid low-level condition where operation could damage equipment or invalidate process control.
- **CTL-012** — A detected wet-zone leak SHALL cause a defined protective response appropriate to the affected subsystem, including disabling replenishment and other fluid addition where continued operation could worsen the leak.
- **CTL-013** — The controller SHALL distinguish requested heat input from requested heat rejection when the installed TSM supports both functions and SHALL prevent conflicting thermal outputs.
- **CTL-014** — Failure or absence of optional active cooling hardware SHALL NOT prevent operation when measured chemistry temperatures remain within the validated process window and no cooling-dependent safety limit is exceeded.
- **CTL-015** — Module and service-cartridge faults SHOULD identify the affected module class and location to support swap-first service.

## Current design direction

A distributed architecture is preferred over one custom board controlling every function. Candidate structure:

```text
operator UI / supervisory controller
              |
        machine control bus
    __________|________________
   |          |        |       |
intake    transport   wet/     safety/
                    thermal/    leak
                     fluid
```

Possible implementations include an industrial PLC, embedded controller network, or hybrid architecture. No controller family is frozen yet.

## Thermal state model

Where thermal conditioning supports both adding and rejecting heat, the controller should use a non-overlapping state model such as:

```text
HEAT
HOLD / DEAD BAND
REJECT HEAT
FAULT
```

Exact control logic, hysteresis, PID strategy, and cooling hardware remain TBD and must be derived from the selected chemistry and thermal prototype results.

## Fluid state model

Where applicable, each WBM should expose process-relevant state rather than forcing higher-level software to infer it from pump behavior:

```text
LEVEL INVALID / LOW
LEVEL VALID
HIGH / OVERFLOW RISK
LEAK DETECTED (machine or zone level)
```

The physical sensor count may differ from the logical state count.

## Process data

A process record should eventually be able to associate at least:

- job/roll identifier;
- recipe version;
- start/end time;
- measured temperatures;
- requested thermal state;
- transport faults;
- level/leak faults;
- module identity/configuration;
- operator-visible warnings.

## Open questions

- PLC versus embedded MCU architecture.
- CAN, RS-485, Ethernet, or mixed bus.
- Touchscreen size and operator workflow.
- Local-only versus optional network logging.
- Recipe authorization and calibration permissions.
- Which protective actions should be stage-local versus machine-wide after leak or level faults.