---
title: Standardized Module Platform
slug: module-platform
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
- **MOD-014** — Wet transport geometry SHALL be represented by a standardized `TRM` Transport Rack Module service boundary separate from the dry-side `TDM` drive source and the `WBM` bath vessel.
- **MOD-015** — Standardized sensing functions that do not justify a top-level module class MAY be implemented as documented replaceable service cartridges, provided their mechanical, electrical, calibration, and compatibility interfaces are defined.

## Initial module classes

| Class | Working name | Service boundary | Intended contents |
|---|---|---|---|
| `TDM` | Transport Drive Module | Dry-side motion source | motor, gearbox if required, encoder, output coupling, local protection/connector |
| `TRM` | Transport Rack Module | Wet film-path service unit | rollers, guides, sprockets if used, passive gears/shafts, rack frame, drive receiving interface |
| `TSM` | Thermal Service Module | Replaceable thermal-conditioning hardware | heat input, temperature sensing, independent thermal protection, and heat-rejection interface where required |
| `FSM` | Fluid Service Module | Dry/service-side fluid movement | pump/valve/filter or metering hardware, replaceable tubing/ports as applicable |
| `WBM` | Wet Bath Module | Chemistry vessel | tank, fluid ports, thermal receiving interface, drain geometry, TRM receiving interface |

These class names define boundaries, not final dimensions or vendor parts.

## Service hierarchy

Top-level modules should not proliferate merely because a replaceable component exists. Common wear or sensing functions can be standardized as submodules or service cartridges inside a module family.

Examples include:

- level-sensor cartridge;
- temperature-probe cartridge;
- heater cartridge;
- pump cartridge;
- filter cartridge;
- replenishment-metering cartridge;
- thermal cutoff/protection device.

A service cartridge still requires a documented interface when it is production-intended, but it does not automatically become a new top-level machine subsystem.

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

### Thermal

The `TSM` interface represents **thermal conditioning**, not only heating. The interface shall support the required heat input and temperature measurement functions and shall not preclude later heat rejection or cooling if environmental testing demonstrates that it is necessary.

### Data and identity

Machine-readable module identification is desirable for incompatible module/revision detection. EEPROM, one-wire identity, NFC/RFID, controller-node identity, and keyed passive coding remain candidates.

## Validation

A module interface is not considered validated until tests demonstrate:

- repeatable mounting and removal;
- correct alignment after replacement;
- no unintended cross-connection;
- required electrical/fluid/thermal performance;
- safe fault behavior;
- replacement without damage to adjacent modules;
- successful use of a second independently assembled module.

## Open questions

- Common mechanical rail/datum system.
- Standard electrical voltage classes and connectors.
- Machine-readable module identity method.
- TDM-to-TRM output coupling geometry.
- TRM rack datum and interchangeability standard.
- TSM conductive thermal-interface geometry and optional heat-rejection interface.
- FSM pump/valve cartridge geometry.
- Maximum module replacement-time targets.