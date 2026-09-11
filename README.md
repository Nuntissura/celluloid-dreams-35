# Celluloid Dreams 35

**Project code:** CD35

Celluloid Dreams 35 is an open engineering project for a modern, modular, daylight-operated 35 mm film processing machine.

The initial target is a low-to-medium-volume **35 mm C-41 production processor** designed around standardized, field-replaceable modules and readily replaceable parts rather than proprietary monolithic assemblies.

## Current engineering focus

Machine shape is deliberately deferred. The current priority is validating standardized service interfaces for:

- **TDM** — Transport Drive Module: dry-side motor/gearbox/encoder and drive coupling;
- **TSM** — Thermal Service Module: replaceable heating, sensing, and thermal protection;
- **FSM** — Fluid Service Module: circulation, transfer, replenishment, drain/service hardware;
- **WBM** — Wet Bath Module: chemistry vessel and local wet film path receiving TDM/TSM/FSM services.

The design rule is simple: repeated functions converge on common modules or part families, and a unique part requires a technical reason.

## Core design intent

- 35 mm film only for the first machine.
- Daylight loading with a light-tight exposed-film path.
- Production-oriented workflow rather than hobby batch processing.
- Commodity/off-the-shelf motors, pumps, sensors, heaters, valves, connectors, and controls where technically appropriate.
- Standardized module interfaces so failed assemblies can be exchanged before component-level repair.
- Wet bath vessels kept as passive and serviceable as process performance permits.
- Fast, controlled fluid filling/draining using serviceable and error-resistant connections.
- Chemistry-contact components accessible for cleaning or replacement.
- No dependence on obsolete proprietary electronics or vendor-only service software where avoidable.

## Repository structure

```text
/
├── README.md
├── codex.md
├── codex/
│   ├── README.md
│   ├── authority.md
│   ├── repository-behavior.md
│   ├── spec-workflow.md
│   └── product-build-rules.md
└── cd35-gov/
    └── spec/
        ├── current/
        │   ├── index.md
        │   └── <topic>.md
        └── archive/
            └── <version>/
```

[`codex.md`](./codex.md) is the stable project-authority entry point. Normative codex rules live under [`codex/`](./codex/) and have stable IDs such as `AUTH-*`, `REP-*`, `WF-*`, and `PBR-*`.

[`cd35-gov/spec/current/index.md`](./cd35-gov/spec/current/index.md) is the canonical active engineering specification. `cd35-gov/spec/archive/` contains immutable snapshots of superseded baselines.

## Current project phase

The project is in **concept / module architecture definition**. Transport mechanism, chemistry selection, dimensions, throughput, bath volumes, coupling families, pump types, heater architecture, and controller platform are not yet frozen. Values become requirements only after evidence and validation.