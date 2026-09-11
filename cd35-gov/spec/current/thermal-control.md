---
title: Thermal Control
slug: thermal-control
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
  - wet-process-modules
  - controls-and-software
supersedes: null
---

# Thermal Control

## Purpose

Define how CD35 measures, controls, verifies, and protects process temperature.

## Normative requirements

- **THM-001** — Process temperature setpoints and tolerances SHALL be derived from the selected chemistry manufacturer's current technical specification and validated in CD35 testing before they are frozen.
- **THM-002** — The developer stage SHALL use closed-loop temperature control.
- **THM-003** — Temperature sensing SHALL measure the working solution or a validated proxy representative of the working solution temperature.
- **THM-004** — The system SHALL prevent processing when a chemistry-critical stage is outside its permitted temperature window.
- **THM-005** — Active heating SHALL include an independent over-temperature protection path that does not rely solely on normal control software.
- **THM-006** — Temperature sensors SHALL be replaceable and calibratable or verifiable against a reference.
- **THM-007** — Circulation or equivalent mixing SHALL be sufficient to prevent unacceptable thermal stratification within temperature-critical baths.
- **THM-008** — The controller SHALL log detected temperature faults during a roll's process cycle.

## Current design direction

Use industrial RTD sensing such as PT100/PT1000-class probes or an equivalent verified technology, with PID or similarly controlled heating. A second independent sensor in the developer module is a candidate for plausibility checking and fault detection.

The developer is expected to require tighter thermal control than downstream stages; identical mechanical wet modules do not imply identical heating hardware.

## Validation

Validation should measure:

- absolute sensor error against a traceable or known reference;
- temperature uniformity at multiple bath locations;
- warm-up time;
- overshoot after startup and replenishment;
- recovery after film and fluid loading;
- behavior after sensor failure or heater-control failure.

## Open questions

- Final sensor technology and connector standard.
- Required absolute accuracy and stability after chemistry selection.
- Heater wattage and placement.
- Whether developer uses dual independent sensors in production hardware.
- Whether heating is per module or via a shared thermal loop.
