---
title: CD35 Current Specification Index
slug: spec-index
project: CD35
document_type: spec-index
status: current
maturity: concept
baseline_version: "0.2.0"
baseline_date: 2026-09-11
last_updated: 2026-09-11
---

# Celluloid Dreams 35 — Current Specification

**Baseline:** v0.2.0  
**Maturity:** Concept / module architecture definition

## System definition

CD35 is a modular, daylight-operated processor initially dedicated to **35 mm C-41 film**. The target is low-to-medium-volume commercial production with strong emphasis on operator efficiency, repairability, interchangeable service modules, and long-term access to replacement parts.

The machine should accept a 35 mm cassette in normal room light, keep exposed film light-tight until chemically safe, transport film through controlled wet stages, and deliver a dry processed negative without requiring a darkroom.

## Current architecture priority

The current engineering priority is deliberately **not machine shape**. CD35 first defines and validates the service interfaces for:

1. film transport;
2. heating and temperature sensing;
3. fluid import, circulation, replenishment, and extraction;
4. wet bath modules that receive those services.

Final chassis/enclosure form is deferred until these interfaces are stable, following `PBR-006`.

## Module vocabulary

| Class | Name | Boundary |
|---|---|---|
| `TDM` | Transport Drive Module | dry-side motor/gearbox/encoder and output coupling |
| `TSM` | Thermal Service Module | replaceable heating/sensing/protection hardware |
| `FSM` | Fluid Service Module | pump/valve/filter/metering service hardware |
| `WBM` | Wet Bath Module | chemistry vessel, local wet film path, receiving interfaces |

## Topic map

| Topic | File | Purpose |
|---|---|---|
| Scope and goals | [scope-and-goals.md](./scope-and-goals.md) | Product boundary, target use, non-goals |
| System architecture | [system-architecture.md](./system-architecture.md) | Top-level subsystem and service-boundary model |
| Module platform | [module-platform.md](./module-platform.md) | Standard mechanical/electrical/fluid/data module interfaces |
| Daylight intake | [daylight-intake.md](./daylight-intake.md) | Cassette insertion, light-tight acquisition, end handling |
| Film transport | [film-transport.md](./film-transport.md) | Film movement, TDM architecture, tension and drive standardization |
| Wet-process modules | [wet-process-modules.md](./wet-process-modules.md) | WBM chemistry vessels and receiving interfaces |
| Fluid handling | [fluid-handling.md](./fluid-handling.md) | Fluid import, circulation, replenishment, drain/extraction and FSM architecture |
| Thermal control | [thermal-control.md](./thermal-control.md) | Heating, sensing, TSM architecture and protection |
| Crossovers and contamination | [crossover-contamination.md](./crossover-contamination.md) | Carryover control between process stages |
| Drying | [drying.md](./drying.md) | Water removal and controlled dry output |
| Controls and software | [controls-and-software.md](./controls-and-software.md) | State control, module identity, fault handling, logging |
| Serviceability | [serviceability.md](./serviceability.md) | Field replacement and repairability requirements |
| Safety and compliance | [safety-and-compliance.md](./safety-and-compliance.md) | Chemical, electrical, thermal, mechanical safety |
| Open questions | [open-questions.md](./open-questions.md) | Decisions not sufficiently verified to freeze |

## Cross-topic constraints

1. The first CD35 machine is 35 mm only.
2. Normal operation must not require a darkroom.
3. The initial process target is C-41.
4. Production workflow takes priority over hobby-style batch handling.
5. Repeated functions must converge on standardized modules or part families unless a documented technical reason prevents it.
6. Off-the-shelf components with documented specifications are preferred where they satisfy performance, safety, chemistry, and lifecycle needs.
7. Wet bath vessels should be as passive and serviceable as process performance permits.
8. Likely failure/service components should live in dry-side replaceable modules where practical.
9. Final machine shape is deferred until transport, thermal, fluid, and wet-module interfaces are validated.
10. Unverified chemistry timings, tolerances, dimensions, throughput, and selected component families remain TBD until supported by evidence.

## High-level process/service concept

```text
Cassette -> Intake -> WBM -> WBM -> WBM -> Wash/Rinse -> Dryer -> dry negative
                      |      |      |
                     TDM    TDM    TDM
                     TSM    TSM    TSM
                     FSM    FSM    FSM
```

The diagram represents service boundaries, not a frozen stage count or physical layout.

## Promotion summary

### v0.2.0 — 2026-09-11

Establishes the standardized repairable module platform:

- creates `TDM`, `TSM`, `FSM`, and `WBM` service boundaries;
- makes commonization and off-the-shelf component selection project build rules;
- separates wet bath vessels from likely-failure transport, thermal, and fluid hardware where practical;
- adds a dedicated fluid-handling specification;
- defines a standardized module-platform specification;
- explicitly defers external machine shape until critical module interfaces are validated;
- restructures project governance into rule-ID-based codex documents;
- archives the previous v0.1.0 baseline unchanged.

### v0.1.0 — 2026-09-11

Initial structured concept specification establishing 35 mm-only scope, daylight operation, C-41 target, modular wet baths, serviceability intent, and verification-first open questions.