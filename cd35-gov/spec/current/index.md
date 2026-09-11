---
title: CD35 Current Specification Index
slug: spec-index
project: CD35
document_type: spec-index
status: current
maturity: concept
baseline_version: "0.1.0"
baseline_date: 2026-09-11
last_updated: 2026-09-11
---

# Celluloid Dreams 35 — Current Specification

**Baseline:** v0.1.0  
**Maturity:** Concept / architecture definition

## System definition

CD35 is a modular, daylight-operated processor initially dedicated to **35 mm C-41 film**. The target use case is low-to-medium-volume commercial production where operator time, maintainability, rapid chemistry service, and long-term repairability matter more than supporting every film format or process.

The machine should accept a 35 mm cassette in normal room light, keep exposed film light-tight until chemically safe, transport the film through a sequence of interchangeable process modules, and deliver a dry processed negative without requiring a darkroom.

## Topic map

| Topic | File | Purpose |
|---|---|---|
| Scope and goals | [scope-and-goals.md](./scope-and-goals.md) | Product boundary, target use, non-goals |
| System architecture | [system-architecture.md](./system-architecture.md) | Top-level subsystem model and interfaces |
| Daylight intake | [daylight-intake.md](./daylight-intake.md) | Cassette insertion, light-tight acquisition, end handling |
| Film transport | [film-transport.md](./film-transport.md) | Film movement, tension, drive standardization |
| Wet-process modules | [wet-process-modules.md](./wet-process-modules.md) | Interchangeable chemistry bath modules |
| Thermal control | [thermal-control.md](./thermal-control.md) | Temperature measurement, heating, uniformity, protection |
| Crossovers and contamination | [crossover-contamination.md](./crossover-contamination.md) | Carryover control between process stages |
| Drying | [drying.md](./drying.md) | Water removal and controlled dry output |
| Controls and software | [controls-and-software.md](./controls-and-software.md) | State control, module identity, fault handling, logging |
| Serviceability | [serviceability.md](./serviceability.md) | Replaceability, cleaning, standard components |
| Safety and compliance | [safety-and-compliance.md](./safety-and-compliance.md) | Chemical, electrical, thermal, mechanical safety |
| Open questions | [open-questions.md](./open-questions.md) | Decisions not yet sufficiently verified to freeze |

## Cross-topic constraints

1. The first CD35 machine is 35 mm only.
2. Normal operation must not require a darkroom.
3. The initial process target is C-41.
4. The architecture must favor production workflow over hobby-style manual batch handling.
5. Wet stages must be modular and serviceable.
6. Motors, sensors, pumps, heaters, and control components should be standardized and replaceable where feasible.
7. Chemical-contact components must be accessible for cleaning or replacement without dismantling unrelated machine assemblies.
8. Unverified chemistry timings, temperature tolerances, dimensions, and throughput figures remain TBD until tied to selected process chemistry and test evidence.

## High-level process concept

```text
35 mm cassette
      |
      v
DAYLIGHT / LIGHT-TIGHT INTAKE
      |
      v
DEVELOPER -> CROSSOVER -> BLEACH -> CROSSOVER -> FIX -> WASH -> FINAL RINSE -> DRY
      |
      v
processed dry negative
```

The diagram represents the current architectural direction, not a frozen tank count, bath geometry, or chemistry timing.

## Promotion summary

### v0.1.0 — 2026-09-11

Initial structured specification derived from the founding CD35 concept. Establishes:

- 35 mm-only initial scope;
- daylight operation;
- C-41 initial target;
- modular wet-bath architecture;
- standardized transport/motor intent;
- serviceability as a first-class requirement;
- explicit separation between requirements, design direction, and unresolved engineering questions.
