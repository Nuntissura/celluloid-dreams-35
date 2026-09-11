---
title: Film Transport
slug: film-transport
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.3.0"
topic_revision: 3
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

Define how CD35 moves 35 mm film through dry and wet sections while controlling speed, tension, tracking, damage risk, cleaning, and serviceability.

## Normative requirements

- **TRN-001** — Transport components SHALL be designed specifically for 35 mm film geometry.
- **TRN-002** — The film path SHALL avoid intentional contact with the image-bearing emulsion area wherever practical.
- **TRN-003** — Transport SHALL maintain controlled film tension and SHALL detect or limit abnormal tension before film damage occurs.
- **TRN-004** — Wet-stage transport speed SHALL be sufficiently stable to meet the selected chemistry residence-time tolerance.
- **TRN-005** — Repeated powered transport locations SHALL use the standardized `TDM` Transport Drive Module unless a documented exception is justified under `PBR-002` and `PBR-003`.
- **TRN-006** — Wet transport rollers, guides, sprockets, shafts, and passive gears SHALL be grouped into a removable `TRM` Transport Rack Module wherever practical.
- **TRN-007** — 35 mm perforations MAY be used for position, speed, or fault sensing, but perforation-driven transport SHALL NOT be frozen as the primary drive method until wet-film damage risk is validated.
- **TRN-008** — The controller SHALL detect transport stall or material speed disagreement that can create damaging tension.
- **TRN-009** — The normal `TDM` service boundary SHOULD remain on the dry side of the chemistry boundary so motor and encoder replacement does not require chemical handling.
- **TRN-010** — A `TDM` SHALL provide closed-loop speed or position feedback through an encoder or equivalent verified feedback mechanism.
- **TRN-011** — The `TDM` output interface SHALL use a standardized mechanical coupling to the `TRM`.
- **TRN-012** — Replacement of a `TDM` SHOULD NOT require draining the associated wet bath.
- **TRN-013** — The TDM-to-TRM drive interface SHALL tolerate the defined installation alignment error without imposing damaging axial or radial load on the film path.
- **TRN-014** — Transport torque/current limits or equivalent protection SHALL be defined so a jam does not simply convert motor capability into film damage.
- **TRN-015** — A `TRM` SHALL be serviceable independently of the motor/encoder assembly and SHOULD be removable independently of the `WBM` vessel after any required chemistry-safe service preparation.
- **TRN-016** — Repeated transport modules SHALL comply with `PBR-001` through `PBR-005` and `PBR-012` through `PBR-019`.
- **TRN-017** — A `TRM` SHALL define a common receiving datum, retention method, and drive-coupling interface so independently assembled racks can be exchanged without stage-specific realignment procedures where practical.
- **TRN-018** — A `TRM` SHOULD contain no powered electrical component in the wet service boundary unless testing demonstrates a clear performance or safety reason for integration.
- **TRN-019** — Wear components within a `TRM`, including rollers, bearings/bushings, gears, guides, or sprockets if used, SHOULD be individually replaceable where doing so is practical and materially improves service life.
- **TRN-020** — Removing a `TRM` for cleaning or inspection SHALL NOT require removing the associated `TDM` from its dry-side service position.

## Transport service boundaries

### `TDM` — Transport Drive Module

```text
[TDM]
  off-the-shelf motor
  gearbox if required
  encoder / feedback
  standard electrical connector
  output shaft/coupling
  replaceable mounting adapter where required
```

### `TRM` — Transport Rack Module

```text
[TRM]
  rack/frame
  wet rollers and guides
  passive gears/shafts
  sprockets if selected
  film-path geometry
  standardized drive receiver
  standardized WBM/chassis datums
```

The intended separation is:

```text
DRY SIDE                         WET / PROCESS SIDE

[TDM motor+encoder] ==coupler== [TRM rollers/gears/guides]
                                      |
                                      v
                                  [WBM bath]
```

A failed motor can therefore be exchanged without handling chemistry. A dirty or worn transport rack can be removed for cleaning or repair without replacing the bath vessel.

## Current design direction

Use one motor/gearbox/encoder family across as many powered locations as practical. A standardized adapter plate and output coupling can absorb vendor-specific mounting geometry so the machine-level interface stays stable if the purchased motor changes.

Likewise, the wet film path should be implemented as an exchangeable rack rather than permanently built into the WBM shell. The `TRM` may differ internally between process stages if residence-time geometry requires it, but its mounting and drive interfaces should remain common where practical.

The preferred control concept is a shared master line-speed command with local closed-loop drive feedback. Stage drives may apply small torque/speed corrections to manage tension, but the machine shall not rely on uncontrolled speed mismatch between baths.

Perforation sensing remains attractive for deterministic film-motion verification even if the film is ultimately driven by friction rollers or a leader/carrier.

## Interfaces

- `module-platform` defines TDM/TRM mechanical and electrical service boundaries.
- Intake hands film to the transport subsystem.
- `WBM` provides the wet-bath receiving geometry around the TRM.
- Controls coordinate speed, tension protection, stall detection, and recovery.
- Crossovers preserve alignment while limiting chemical carryover.

## Validation

Transport validation should include:

- dry and wet scratch inspection;
- repeated 24/36-exposure roll transport;
- damaged-perforation samples;
- wet-film tension measurements;
- intentional stall/jam tests;
- TDM swap and alignment repeatability;
- TRM swap and film-path alignment repeatability;
- repeated TRM removal/cleaning/reinstallation;
- line-speed stability;
- restart/recovery behavior after interruption.

## Open questions

- Roller, sprocket, leader/carrier, or hybrid wet drive.
- Nominal line speed.
- Maximum permissible film tension.
- TDM motor type, gearbox ratio, encoder resolution, and output coupling.
- TRM datum, retention, roller/bearing materials, and stage-specific geometry rules.
- Dancer/tension sensing geometry.
- Automatic threading and jam recovery.
- Whether every wet stage needs a powered TDM or some stages can share a drive train without harming serviceability.