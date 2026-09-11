---
title: Film Transport
slug: film-transport
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
  - daylight-intake
supersedes: null
---

# Film Transport

## Purpose

Define how CD35 moves 35 mm film through dry and wet sections while controlling speed, tension, tracking, and surface damage risk.

## Normative requirements

- **TRN-001** — Transport components SHALL be designed specifically for 35 mm film geometry.
- **TRN-002** — The film path SHALL avoid intentional contact with the image-bearing emulsion area wherever practical.
- **TRN-003** — Transport SHALL maintain controlled film tension and SHALL detect or limit abnormal tension before film damage occurs.
- **TRN-004** — Wet-stage transport speed SHALL be sufficiently stable to meet the selected chemistry residence-time tolerance.
- **TRN-005** — Repeated drive locations SHOULD use a standardized motor/drive module.
- **TRN-006** — Replaceable transport racks or guides SHOULD be removable for cleaning without draining or dismantling unrelated stages where practical.
- **TRN-007** — 35 mm perforations MAY be used for position, speed, or fault sensing, but perforation-driven transport SHALL NOT be frozen as the primary drive method until wet-film damage risk is validated.
- **TRN-008** — The controller SHALL detect transport stall or material speed disagreement that can create damaging tension.

## Current design direction

Candidate architecture uses closed-loop drive modules with a shared line-speed command and local feedback. Perforations are a valuable deterministic sensing feature, but film-edge sprocket engagement versus friction/leader-assisted drive remains open.

A reusable transport leader or carrier is a candidate method for taking mechanical load away from the customer's film during initial acquisition and threading.

## Interfaces

- Intake hands film to the transport subsystem.
- Wet modules provide removable transport geometry through each bath.
- Controls coordinate motor speed and fault response.
- Crossovers must preserve film alignment while controlling liquid carryover.

## Open questions

- Roller transport, sprocket transport, carrier/leader transport, or hybrid.
- Nominal line speed.
- Maximum permissible film tension.
- Encoder resolution and speed-control tolerance.
- Dancer/tension-sensor geometry.
- Automatic threading and recovery after a jam.
