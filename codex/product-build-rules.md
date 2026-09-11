---
title: CD35 Product Build Rules
project: CD35
document_type: governance
status: current
rule_prefix: PBR
version: "1.0"
last_updated: 2026-09-11
---

# CD35 Product Build Rules

These rules apply across the machine unless a rule explicitly allows a justified exception.

## Modularity and standardization

- **PBR-001** — CD35 SHALL be designed as replaceable functional modules with explicit mechanical, electrical, fluid, data, and service interfaces where applicable.
- **PBR-002** — Repeated functions SHALL converge on the same module or component family unless a documented technical requirement makes commonization impractical.
- **PBR-003** — A project-unique component SHALL require a documented reason showing why an available standard or off-the-shelf solution does not adequately meet the requirement.
- **PBR-004** — Standardization SHALL be based on function and service boundary, not on forcing physically or chemically incompatible tasks into one part.
- **PBR-005** — Module interfaces SHALL be versioned and documented sufficiently to permit independent replacement, redesign, or manufacture of a compatible module.
- **PBR-006** — The external machine shape and cosmetic enclosure SHALL NOT be allowed to freeze or distort critical transport, thermal, or fluid-service interfaces before those subsystems are validated.

## Off-the-shelf and lifecycle preference

- **PBR-007** — Commercially available components with published specifications SHALL be preferred over proprietary project-specific equivalents when performance, safety, chemical compatibility, and lifecycle needs can be met.
- **PBR-008** — Critical purchased components SHOULD have at least one practical alternate supplier, alternate compatible part, or documented redesign path before production maturity.
- **PBR-009** — Part selection SHALL consider replacement availability, datasheet quality, environmental and chemical ratings, electrical/mechanical derating, cost, and expected lifecycle rather than purchase price alone.
- **PBR-010** — Commodity motors, bearings, sensors, heaters, pumps, valves, power supplies, fasteners, connectors, and controllers SHOULD be used where the engineering requirements allow it.
- **PBR-011** — Custom electronics SHOULD use documented standard buses, connectors, and replaceable subassemblies rather than making routine service depend on one monolithic proprietary board.

## Repairability and field replacement

- **PBR-012** — A likely service failure SHALL be repairable by replacing the smallest practical field-replaceable unit without dismantling unrelated subsystems.
- **PBR-013** — A failed field-replaceable module SHOULD be exchangeable so production can resume before component-level repair of the failed module is completed.
- **PBR-014** — Routine service operations SHOULD use common hand tools; special tools require documented justification.
- **PBR-015** — Routine service parts SHALL NOT require destructive disassembly, permanent adhesive removal, or irreversible deformation unless a safety or chemical-sealing requirement justifies it.
- **PBR-016** — Frequently removed fasteners SHOULD be standardized to a small set of sizes and drive types and SHOULD be captive where loss into the machine is a credible hazard.
- **PBR-017** — Wear components and service indicators SHALL be accessible for inspection without major disassembly.
- **PBR-018** — Calibration of replaceable critical sensors SHALL be possible using documented procedures without vendor-only service software where practical.
- **PBR-019** — Every production-intended field-replaceable module SHALL have an interface definition, replacement procedure, and replaceable-part list.

## Wet/dry separation and chemical service

- **PBR-020** — Components that routinely contact process chemistry SHALL be removable, cleanable, or replaceable without exposing unrelated dry electronics to routine chemical service.
- **PBR-021** — Pumps, valves, sensors, heaters, and electrical connectors SHOULD be located on the dry/service side of a fluid boundary where doing so does not compromise process performance.
- **PBR-022** — Fluid connections intended for routine disconnection SHOULD use shutoff or non-spill coupling behavior appropriate to the chemical and pressure regime.
- **PBR-023** — Fluid connections whose accidental interchange could contaminate chemistry or create a hazard SHALL be keyed, mechanically differentiated, electronically identified, or otherwise error-proofed.
- **PBR-024** — Fluid systems SHALL provide intentional low-point drain or extraction paths; routine emptying SHALL NOT depend on tipping the processor or uncontrolled siphoning.
- **PBR-025** — Hoses, seals, wetted plastics, metals, and elastomers SHALL be validated against the assigned chemistry before the material choice is frozen.
- **PBR-026** — A wet module SHOULD be isolatable and removable without cutting tubing, desoldering wiring, or disturbing adjacent process stages.

## Electrical and control interfaces

- **PBR-027** — Repeated module power and signal classes SHALL use a common connector and pinout standard wherever incompatible loads do not require differentiation.
- **PBR-028** — Connectors that can be damaged or create a hazard if cross-mated SHALL be mechanically keyed or otherwise prevented from incorrect mating.
- **PBR-029** — Replaceable active modules SHOULD expose enough identity or configuration information for the controller to detect incompatible module types or interface revisions.
- **PBR-030** — Safety interlocks and independent protective devices SHALL remain effective after replacement of a normal control module and SHALL NOT rely solely on application software.

## Documentation and verification

- **PBR-031** — Each standardized module class SHALL define its service boundary, interfaces, replaceable subcomponents, expected failure modes, and validation tests.
- **PBR-032** — Interchangeability SHALL be tested using at least two independently assembled examples before a module interface is considered validated.
- **PBR-033** — A module SHALL NOT be declared interchangeable merely because connectors fit; mechanical datum, electrical behavior, fluid behavior, control compatibility, and safety behavior SHALL be verified as applicable.
- **PBR-034** — Custom parts essential to long-term repair SHOULD have manufacturable drawings or source design files retained in the repository or an explicitly managed project source location.
- **PBR-035** — Design reviews SHOULD actively search for unnecessary unique parts, hidden service dependencies, inaccessible wear items, and single-source components.

## Design intent

The desired result is not maximum modularity at any cost. The desired result is a machine whose high-failure, high-maintenance, chemistry-exposed, or lifecycle-sensitive functions can be replaced using stable interfaces and readily obtainable parts without compromising process control or safety.