---
title: Fluid Handling and Service
slug: fluid-handling
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
  - module-platform
supersedes: null
---

# Fluid Handling and Service

## Purpose

Define standardized fluid import, circulation, replenishment, extraction, draining, isolation, level management, and service interfaces for CD35 wet stages.

## Normative requirements

- **FLD-001** — Routine fluid connections between a wet bath module and the processor SHALL use defined standardized port roles rather than ad-hoc hoses permanently attached across module boundaries.
- **FLD-002** — Each chemistry-bearing wet module SHALL provide an intentional low-point drain or extraction path capable of removing the working solution without tipping the processor.
- **FLD-003** — A wet module intended for routine removal SHALL be isolatable and disconnectable without cutting tubing or disturbing adjacent wet stages.
- **FLD-004** — Fluid connections intended for routine service SHOULD provide shutoff or non-spill behavior appropriate to the assigned chemistry and pressure regime.
- **FLD-005** — Fluid roles whose interchange could contaminate chemistry, damage equipment, or create a hazard SHALL be keyed, mechanically differentiated, electronically identified, or otherwise error-proofed.
- **FLD-006** — Wetted couplings, tubing, pump heads, seals, valves, filters, and fittings SHALL be validated for compatibility with the assigned chemistry before production selection is frozen.
- **FLD-007** — Replaceable fluid-service hardware SHOULD be located on the dry/service side of the bath boundary where performance and priming requirements permit.
- **FLD-008** — Repeated circulation or transfer functions SHALL use a standardized `FSM` service module or common pump/valve component family unless process requirements justify a different class.
- **FLD-009** — Replenishment metering SHALL be separable from bulk circulation so the metering method can be serviced or calibrated independently.
- **FLD-010** — Fluid paths requiring routine cleaning SHALL provide a documented drain and flush procedure that does not depend on uncontrolled siphoning.
- **FLD-011** — Hoses and flexible lines intended as service parts SHALL be individually replaceable and SHOULD use the smallest practical set of standardized diameters and termination types.
- **FLD-012** — Hidden routine-disconnect locations SHOULD drain or leak into visible containment rather than onto electrical assemblies or inaccessible structure.
- **FLD-013** — Service ports SHALL be labeled by function and module/stage identity at the connection point.
- **FLD-014** — The fluid subsystem SHALL define allowable pressure, vacuum, temperature, and flow ranges before a coupling, pump, or valve family is frozen.
- **FLD-015** — A fluid-service module SHALL be replaceable without requiring recalibration of unrelated process stages.
- **FLD-016** — Pumps and valves that are expected wear/failure items SHALL be replaceable independently of the wet bath tank where practical.
- **FLD-017** — Drain and waste routing SHALL prevent a normal service operation from mixing incompatible process solutions unintentionally.
- **FLD-018** — Fluid-system service SHALL comply with `PBR-020` through `PBR-026`.
- **FLD-019** — A stage whose pump, heater, process quality, or safety can be compromised by low liquid level SHALL provide a level-valid signal before those functions are enabled.
- **FLD-020** — A stage where overflow can damage equipment, mix chemistry, or create a safety risk SHALL provide either direct high-level detection or a validated passive overflow path with detectable containment.
- **FLD-021** — Repeated level sensing SHOULD use a standardized replaceable sensor cartridge or common sensor family with a documented WBM receiving interface.
- **FLD-022** — The wet section SHALL provide containment or drainage geometry such that foreseeable leakage is directed away from dry electrical assemblies and toward an observable or instrumented leak-detection area.
- **FLD-023** — Leak detection SHALL be treated as machine/chassis infrastructure rather than requiring a dedicated top-level process module unless later architecture provides a technical reason otherwise.

## Standard port roles

The initial interface vocabulary is:

| Port role | Function | Notes |
|---|---|---|
| `SUCTION` | solution leaves bath toward circulation/service hardware | location and anti-vortex geometry TBD |
| `RETURN` | conditioned/circulated solution returns to bath | return geometry must avoid harmful film disturbance |
| `DRAIN` | controlled complete or near-complete emptying | should originate at true low point |
| `REPL` | replenishment or make-up chemistry input | metered function |
| `OVERFLOW` | controlled overflow/level management where required | not all stages require it |
| `FILL` | bulk filling/service input where distinct from `RETURN` | may be combined if validation supports it |

The final product may combine compatible roles, but a combined port must be explicitly defined rather than assumed.

## Current design direction

The preferred architecture keeps the wet bath relatively passive and moves common failure/service components into dry-side `FSM` assemblies:

```text
WET BATH MODULE
  SUCTION o====[quick disconnect]====[FSM pump/filter]====o RETURN
      |
      +---- DRAIN o====[service coupling]====> waste/storage
      +---- REPL  o<===[metering cartridge]
      +---- level sensor cartridge / interface

wet-zone containment tray ----> leak sensor / visible drain area
```

For routine-disconnect chemistry lines, chemically resistant non-spill polypropylene coupling families are commercially available. CPC's NSH/NS4 families remain examples of the *component class* being considered, not selected CD35 parts. Their suitability still requires chemistry, seal, temperature, flow, pressure, cost, and availability validation.

Manufacturer references:

- https://www.cpcworldwide.com/General-Purpose/Products/Non-Spill/NSH
- https://www.cpcworldwide.com/General-Purpose/Products/Non-Spill/NS4

## Pump architecture

Do not force one pump technology into every role. The platform should standardize mounting, electrical interface, service access, and tubing/coupling interfaces while allowing validated pump cartridges for different duties.

Candidate duty split:

- continuous circulation: magnetically coupled centrifugal, diaphragm, or other low-contamination continuous-duty pump;
- replenishment: positive-displacement metering or peristaltic pump;
- drain/transfer: gravity first where practical, assisted transfer only where required.

These technologies remain candidates, not frozen selections.

## Level sensing direction

The machine should initially distinguish at least these logical conditions where applicable:

```text
LOW / NOT SAFE TO RUN
NORMAL / PROCESS VALID
HIGH / OVERFLOW RISK
```

This does not require three physical sensors. Float, conductive, capacitive, optical, pressure-derived, or other methods may satisfy the state model if validated against the selected chemistry, foam, deposits, temperature, and cleaning regime.

## Leak detection direction

A shallow wet-zone containment tray or equivalent drainage structure with one or more commodity liquid sensors is the preferred first architecture. The design goal is not to identify every droplet source automatically; it is to detect liquid where liquid should not normally accumulate and to keep it away from energized dry-side hardware.

## Interfaces

- `module-platform` defines FSM and service-cartridge commonization rules.
- `wet-process-modules` provides WBM fluid and level-sensor receiving interfaces.
- `thermal-control` relies on circulation where required for thermal uniformity.
- `controls-and-software` consumes level/leak state and commands pumps/valves.
- `safety-and-compliance` defines the protective response and containment expectations.

## Validation

Fluid-interface validation shall eventually include:

- leak testing at maximum expected pressure/vacuum;
- disconnect spillage and air inclusion where relevant;
- chemical compatibility soak testing;
- drain completeness;
- priming/restart behavior;
- pump flow repeatability;
- replenishment metering accuracy;
- hose and seal service life;
- low/normal/high level-state testing where applicable;
- level-sensor fouling and replacement testing;
- containment and leak-sensor fault testing;
- contamination and cross-connection fault testing;
- module removal/reinstallation repeatability.

## Open questions

- Coupling family, size, seal material, and role-keying strategy.
- Standard hose sizes.
- Gravity versus pumped drain strategy.
- Circulation pump technology and target flow.
- Filter requirement and micron rating per stage.
- Replenishment pump technology and calibration method.
- Level-sensor technology and WBM mounting standard.
- Leak-sensor technology, quantity, and containment geometry.
- Whether `FILL` and `RETURN` can share a port in the first prototype.