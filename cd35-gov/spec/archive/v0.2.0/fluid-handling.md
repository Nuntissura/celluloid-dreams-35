---
title: Fluid Handling and Service
slug: fluid-handling
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
  - module-platform
  - safety-and-compliance
supersedes: null
---

# Fluid Handling and Service

## Purpose

Define standardized fluid import, circulation, replenishment, extraction, draining, isolation, and service interfaces for CD35 wet stages.

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

The preferred architecture keeps the wet bath relatively passive and moves common failure/service components into dry-side `FSM` assemblies. A candidate arrangement is:

```text
WET BATH MODULE
  SUCTION o====[quick disconnect]====[FSM pump/filter]====o RETURN
      |
      +---- DRAIN o====[service coupling]====> waste/storage
      +---- REPL  o<===[metering module]
```

For routine-disconnect chemistry lines, chemically resistant non-spill polypropylene coupling families are commercially available. CPC's NSH/NS4 families are examples of the *component class* being considered, not selected CD35 parts. Their suitability still requires chemistry, seal, temperature, flow, pressure, cost, and availability validation.

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
- contamination and cross-connection fault testing;
- module removal/reinstallation repeatability.

## Open questions

- Coupling family, size, seal material, and role-keying strategy.
- Standard hose sizes.
- Gravity versus pumped drain strategy.
- Circulation pump technology and target flow.
- Filter requirement and micron rating per stage.
- Replenishment pump technology and calibration method.
- Leak detection strategy.
- Whether `FILL` and `RETURN` can share a port in the first prototype.