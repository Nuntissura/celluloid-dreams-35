---
title: CD35 Current Specification Index
slug: spec-index
project: CD35
document_type: spec-index
status: current
maturity: concept
baseline_version: "0.3.0"
baseline_date: 2026-09-11
last_updated: 2026-09-11
---

# Celluloid Dreams 35 — Current Specification

**Baseline:** v0.3.0  
**Maturity:** Concept / module architecture definition

## System definition

CD35 is a modular, daylight-operated processor initially dedicated to **35 mm C-41 film**. The target is low-to-medium-volume commercial production with strong emphasis on operator efficiency, repairability, interchangeable service modules, and long-term access to replacement parts.

The machine should accept a 35 mm cassette in normal room light, keep exposed film light-tight until chemically safe, transport film through controlled wet stages, and deliver a dry processed negative without requiring a darkroom.

## Current architecture priority

The current engineering priority remains deliberately **not machine shape**. CD35 first defines and validates the service interfaces for:

1. dry-side transport drive;
2. removable wet transport racks;
3. thermal conditioning and temperature sensing;
4. fluid import, circulation, replenishment, extraction, and level management;
5. wet bath modules that receive those services.

Final chassis/enclosure form is deferred until these interfaces are stable, following `PBR-006`.

## Module vocabulary

| Class | Name | Boundary |
|---|---|---|
| `TDM` | Transport Drive Module | dry-side motor/gearbox/encoder and output coupling |
| `TRM` | Transport Rack Module | removable wet rollers, guides, shafts/gears and film-path geometry |
| `TSM` | Thermal Service Module | replaceable thermal conditioning, sensing, protection and optional heat-rejection interface |
| `FSM` | Fluid Service Module | pump/valve/filter/metering service hardware |
| `WBM` | Wet Bath Module | chemistry vessel with TRM, thermal, fluid and sensing receiving interfaces |

Level sensors, temperature probes, heaters, pumps, filters, metering hardware, and similar repeated service items may be standardized as replaceable **service cartridges** without becoming additional top-level module classes.

## Topic map

| Topic | File | Purpose |
|---|---|---|
| Scope and goals | [scope-and-goals.md](./scope-and-goals.md) | Product boundary, target use, non-goals |
| System architecture | [system-architecture.md](./system-architecture.md) | Top-level subsystem and service-boundary model |
| Module platform | [module-platform.md](./module-platform.md) | Standard mechanical/electrical/fluid/thermal/data module interfaces |
| Daylight intake | [daylight-intake.md](./daylight-intake.md) | Cassette insertion, light-tight acquisition, end handling |
| Film transport | [film-transport.md](./film-transport.md) | Film movement, TDM/TRM architecture, tension and drive standardization |
| Wet-process modules | [wet-process-modules.md](./wet-process-modules.md) | WBM chemistry vessels and receiving interfaces |
| Fluid handling | [fluid-handling.md](./fluid-handling.md) | Fluid import, circulation, replenishment, drain/extraction, level and leak architecture |
| Thermal control | [thermal-control.md](./thermal-control.md) | Thermal conditioning, conductive TSM architecture, sensing and protection |
| Crossovers and contamination | [crossover-contamination.md](./crossover-contamination.md) | Carryover control between process stages |
| Drying | [drying.md](./drying.md) | Water removal and controlled dry output |
| Controls and software | [controls-and-software.md](./controls-and-software.md) | State control, module identity, fault handling, logging |
| Serviceability | [serviceability.md](./serviceability.md) | Field replacement and repairability requirements |
| Safety and compliance | [safety-and-compliance.md](./safety-and-compliance.md) | Chemical, electrical, thermal, mechanical and leak safety |
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
9. Wet transport racks are separate service units from both the bath vessel and dry drive motor.
10. The preferred first thermal prototype is conductive WBM-to-TSM coupling combined with chemistry circulation.
11. A tempering-water bath/jacket remains a comparison/fallback thermal architecture rather than the default.
12. Cooling is part of the TSM thermal-conditioning domain; active cooling is added only if environmental testing demonstrates a requirement.
13. Level sensing uses standardized replaceable sensing interfaces/cartridges where needed; leak detection is wet-zone/chassis infrastructure unless evidence justifies another boundary.
14. Final machine shape is deferred until transport, thermal, fluid, and wet-module interfaces are validated.
15. Unverified chemistry timings, tolerances, dimensions, throughput, and selected component families remain TBD until supported by evidence.

## High-level process/service concept

```text
Cassette -> Intake -> WBM -> WBM -> WBM -> Wash/Rinse -> Dryer -> dry negative
                      |      |      |
                     TRM    TRM    TRM
                      |      |      |
                     TDM    TDM    TDM
                     TSM    TSM    TSM
                     FSM    FSM    FSM
```

The diagram represents service boundaries, not a frozen stage count or physical layout.

## Thermal direction

The first thermal prototype should use a deliberate conductive interface between the WBM and TSM, while solution circulation distributes heat through the chemistry. The prototype must measure warm-up, steady-state uniformity, recovery, interface redocking repeatability, and heat-rejection behavior before a shared multi-bath thermal spine is considered.

A secondary tempering-water bath/jacket remains the principal comparison architecture if conductive coupling cannot meet process requirements without excessive complexity.

## Promotion summary

### v0.3.0 — 2026-09-11

Refines transport, thermal, and fluid service architecture:

- adds `TRM` as the standardized removable wet Transport Rack Module;
- separates wet film-path hardware from both `TDM` dry drives and `WBM` bath vessels;
- redefines `TSM` as thermal conditioning rather than heating only;
- selects conductive WBM-to-TSM coupling plus chemistry circulation as the preferred first thermal prototype;
- retains a tempering-water bath/jacket as the principal comparison/fallback architecture;
- treats active cooling as evidence-driven optional heat rejection rather than a mandatory cooling module;
- adds standardized level-sensor/service-cartridge requirements;
- adds wet-zone containment and leak-detection requirements;
- keeps final machine shape deferred;
- archives the previous v0.2.0 baseline unchanged.

### v0.2.0 — 2026-09-11

Established the standardized repairable module platform with TDM, TSM, FSM and WBM service boundaries; commonization and off-the-shelf build rules; dedicated fluid handling; and deferred final machine shape.

### v0.1.0 — 2026-09-11

Initial structured concept specification establishing 35 mm-only scope, daylight operation, C-41 target, modular wet baths, serviceability intent, and verification-first open questions.