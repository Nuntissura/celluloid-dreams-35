---
title: Film Transport
slug: film-transport
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
  - system-architecture
  - module-platform
  - daylight-intake
supersedes: null
---

# Film Transport

## Purpose

Define how CD35 moves 35 mm film through dry and wet sections while controlling speed, tension, tracking, damage risk, and serviceability.

## Normative requirements

- **TRN-001** — Transport components SHALL be designed specifically for 35 mm film geometry.
- **TRN-002** — The film path SHALL avoid intentional contact with the image-bearing emulsion area wherever practical.
- **TRN-003** — Transport SHALL maintain controlled film tension and SHALL detect or limit abnormal tension before film damage occurs.
- **TRN-004** — Wet-stage transport speed SHALL be sufficiently stable to meet the selected chemistry residence-time tolerance.
- **TRN-005** — Repeated powered transport locations SHALL use the standardized `TDM` Transport Drive Module unless a documented exception is justified under `PBR-002` and `PBR-003`.
- **TRN-006** — Wet transport racks, guides, rollers, or sprockets SHALL be removable for cleaning and inspection without removing the associated motor from its service location where practical.
- **TRN-007** — 35 mm perforations MAY be used for position, speed, or fault sensing, but perforation-driven transport SHALL NOT be frozen as the primary drive method until wet-film damage risk is validated.
- **TRN-008** — The controller SHALL detect transport stall or material speed disagreement that can create damaging tension.
- **TRN-009** — The normal `TDM` service boundary SHOULD remain on the dry side of the chemistry boundary so motor and encoder replacement does not require chemical handling.
- **TRN-010** — A `TDM` SHALL provide closed-loop speed or position feedback through an encoder or equivalent verified feedback mechanism.
- **TRN-011** — The `TDM` output interface SHALL use a standardized mechanical coupling to the wet transport rack or stage drive.
- **TRN-012** — Replacement of a `TDM` SHOULD NOT require draining the associated wet bath.
- **TRN-013** — The transport drive interface SHALL tolerate the defined installation alignment error without imposing damaging axial or radial load on the film path.
- **TRN-014** — Transport torque/current limits or equivalent protection SHALL be defined so a jam does not simply convert motor capability into film damage.
- **TRN-015** — A transport rack SHALL be serviceable independently of the motor/encoder assembly.
- **TRN-016** — Repeated transport modules SHALL comply with `PBR-001` through `PBR-005` and `PBR-012` through `PBR-019`.

## `TDM` service boundary

The initial `TDM` concept contains:

```text
[TDM]
  off-the-shelf motor
  gearbox if required
  encoder / feedback
  standard electrical connector
  output shaft/coupling
  replaceable mounting adapter where required
```

The wet transport rack is intentionally outside the `TDM` service boundary:

```text
DRY SIDE                         WET / PROCESS SIDE

[TDM motor+encoder] ==coupler== [removable transport rack] -> film
```

This separation lets a failed motor or encoder be changed without removing chemistry and lets a contaminated rack be cleaned without disturbing the motor.

## Current design direction

Use one motor/gearbox/encoder family across as many driven locations as practical. A standardized adapter plate and output coupling can absorb vendor-specific mounting geometry so the machine-level interface stays stable if the purchased motor changes.

The preferred control concept is a shared master line-speed command with local closed-loop drive feedback. Stage drives may apply small torque/speed corrections to manage tension, but the machine shall not rely on uncontrolled speed mismatch between baths.

Perforation sensing remains attractive for deterministic film-motion verification even if the film is ultimately driven by friction rollers or a leader/carrier.

## Interfaces

- `module-platform` defines TDM mechanical/electrical service interfaces.
- Intake hands film to the transport subsystem.
- Wet bath modules carry passive or locally driven wet transport racks.
- Controls coordinate speed, tension protection, stall detection, and recovery.
- Crossovers preserve alignment while limiting chemical carryover.

## Validation

Transport validation should include:

- dry and wet scratch inspection;
- repeated 24/36-exposure roll transport;
- damaged-perforation samples;
- wet-film tension measurements;
- intentional stall/jam tests;
- drive-module swap and alignment repeatability;
- line-speed stability;
- restart/recovery behavior after interruption.

## Open questions

- Roller, sprocket, leader/carrier, or hybrid wet drive.
- Nominal line speed.
- Maximum permissible film tension.
- TDM motor type, gearbox ratio, encoder resolution, and output coupling.
- Dancer/tension sensing geometry.
- Automatic threading and jam recovery.
- Whether every wet stage needs a powered TDM or some stages can share a drive train without harming serviceability.