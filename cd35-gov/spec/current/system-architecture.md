---
title: System Architecture
slug: system-architecture
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
  - scope-and-goals
supersedes: null
---

# System Architecture

## Purpose

Define the top-level CD35 subsystem structure and the boundaries between replaceable modules.

## Normative requirements

- **SYS-001** — The processor SHALL be organized as replaceable functional subsystems with defined mechanical, electrical, and where applicable fluid interfaces.
- **SYS-002** — The exposed-film path SHALL remain light-tight from film acquisition until the process has reached a stage demonstrated to be safe for ambient-light exposure.
- **SYS-003** — The initial architecture SHALL provide functions for intake, development, downstream C-41 processing, washing/rinsing, drying, control, and fault handling.
- **SYS-004** — Routine service of one wet stage SHOULD NOT require dismantling unrelated wet stages.
- **SYS-005** — Module interfaces SHOULD use standardized connectors and mounting features wherever practical.
- **SYS-006** — The system SHALL enter a defined safe state on loss of control power, transport fault, over-temperature condition, or detected access to a light-sensitive path.

## Current design direction

```text
Cassette
  |
  v
[Intake] -> [Developer] -> [Crossover] -> [Bleach] -> [Crossover]
  -> [Fix] -> [Wash] -> [Final rinse] -> [Dryer] -> Output

                  ^
                  |
            [Control system]
```

Wet stages are expected to share a common module envelope where practical. Transport drive elements should likewise use a common serviceable motor/drive standard.

## Interfaces

The architecture depends on:

- `daylight-intake` for safe film acquisition;
- `film-transport` for continuous movement and tension control;
- `wet-process-modules` for chemistry containment and exchange;
- `controls-and-software` for coordination and interlocks.

## Open questions

- Continuous roller transport versus leader/carrier-assisted transport.
- Exact number and geometry of wet modules.
- Point in the process at which the enclosure may transition from light-tight to service-accessible.
- Whether all wet modules share one chassis rail or are independently docked.
