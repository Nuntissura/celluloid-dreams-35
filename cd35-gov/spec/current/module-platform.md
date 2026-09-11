---
title: Standardized Module Platform
slug: module-platform
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.2.0"
topic_revision: 1
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - system-architecture
  - serviceability
supersedes: null
---

# Standardized Module Platform

## Purpose

Define the common module philosophy and interface boundaries used by transport, thermal, fluid-service, and wet-process subsystems.

This topic implements the cross-project modularity and repairability rules in `PBR-*`, especially `PBR-001` through `PBR-006` and `PBR-012` through `PBR-019`.

## Normative requirements

- **MOD-001** — Repeated machine functions SHALL use a defined module class rather than independently designed one-off assemblies unless an exception is justified under `PBR-003`.
- **MOD-002** — Each module class SHALL define mechanical mounting datums, retention method, service clearance, electrical interfaces, fluid interfaces, data interfaces, and safety interfaces that apply to that class.
- **MOD-003** — Module replacement SHALL NOT require modification of an adjacent module's wiring, plumbing, calibration data, or mechanical alignment unless the interface definition explicitly requires a shared calibration procedure.
- **MOD-004** — Standard module interfaces SHALL be independent of cosmetic enclosure shape and SHALL remain usable while the external product form is still unresolved.
- **MOD-005** — A module interface SHALL include a revision identifier, and incompatible interface revisions SHALL be distinguishable in documentation and, where practical, physically or electronically.
- **MOD-006** — Modules requiring controller compatibility SHALL expose a human-readable identity and SHOULD expose a machine-readable type/revision identity.
- **MOD-007** — Repeated electrical power/signal classes SHALL use common connectors and pinouts unless load, safety, wet-zone, or electromagnetic requirements justify differentiation.
- **MOD-008** — Repeated fluid-port classes SHALL use common coupling families while incompatible fluid roles SHALL be error-proofed against cross-connection.
- **MOD-009** — A field-replaceable module SHALL be removable using common hand tools or a documented tool supplied with the machine.
- **MOD-010** — Routine module replacement SHALL NOT require cutting tubing, desoldering wiring, destructive adhesive removal, or draining unrelated wet stages.
- **MOD-011** — Custom mechanical adapters MAY be used to connect off-the-shelf components to the platform, but the adapter SHALL be documented and SHALL NOT unnecessarily make the commercial component proprietary to CD35.
- **MOD-012** — A module class SHALL identify which internal subcomponents are expected to be replaceable independently and which are replaced only at module level.
- **MOD-013** — Interchangeability of a module class SHALL be validated with independently assembled examples before the interface is considered frozen.

## Initial module classes

| Class | Working name | Service boundary | Intended contents |
|---|---|---|---|
| `TDM` | Transport Drive Module | Dry-side motion source | motor, gearbox if required, encoder, output coupling, local protection/connector |
| `TSM` | Thermal Service Module | Replaceable thermal hardware | heater interface, temperature sensing interface, independent thermal protection; exact packaging TBD |
| `FSM` | Fluid Service Module | Dry/service-side fluid movement | pump/valve/filter or metering hardware, replaceable tubing/ports as applicable |
| `WBM` | Wet Bath Module | Chemistry vessel and local wet film path | tank, removable transport rack/guide, fluid ports, thermal receiving interface, drain geometry |

These class names define boundaries, not final dimensions or vendor parts.

## Interface layers

### Mechanical

A module interface should eventually define:

- reference datum surfaces;
- fastening/latching points;
- installation direction;
- allowable positional error;
- service envelope;
- mass/load limits;
- output-shaft or drive-coupling geometry where applicable.

### Electrical

The platform should minimize the number of connector families and power classes. Exact voltages, bus technology, and connector series remain TBD until loads and controls architecture are verified.

### Fluid

Fluid interfaces are defined in `fluid-handling.md`. The module platform requires role identification and service disconnectability but does not yet freeze a coupling vendor or size.

### Data and identity

Machine-readable module identification is desirable for incompatible module/revision detection. EEPROM, one-wire identity, NFC/RFID, controller-node identity, and keyed passive coding remain candidates.

## Validation

A module interface is not considered validated until tests demonstrate:

- repeatable mounting and removal;
- correct alignment after replacement;
- no unintended cross-connection;
- required electrical/fluid performance;
- safe fault behavior;
- replacement without damage to adjacent modules;
- successful use of a second independently assembled module.

## Open questions

- Common mechanical rail/datum system.
- Standard electrical voltage classes and connectors.
- Machine-readable module identity method.
- TDM output coupling geometry.
- TSM physical architecture.
- FSM pump/valve cartridge geometry.
- Maximum module replacement-time targets.