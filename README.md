# Celluloid Dreams 35

**Project code:** CD35

Celluloid Dreams 35 is an open engineering project for a modern, modular, daylight-operated 35 mm film processing machine.

The initial target is a low-to-medium-volume **35 mm C-41 production processor** that does not require a darkroom and is designed around standardized, field-replaceable modules rather than proprietary monolithic assemblies.

## Core design intent

- 35 mm film only for the first machine.
- Daylight loading: the operator inserts a film cassette; exposed film remains inside a light-tight path until it is safe to expose.
- Production-oriented workflow rather than hobby batch processing.
- Interchangeable wet-process modules for developer, bleach, fixer, wash, and final rinse functions.
- Standardized transport and motor modules.
- Precision temperature sensing and control where the chemistry requires it.
- Fast draining and chemistry changes using serviceable fluid connections.
- Components that routinely contact chemistry must be easy to remove, clean, replace, or exchange.
- Commodity motors, sensors, pumps, heaters, and control hardware should be preferred where technically appropriate.
- The machine should be repairable without dependence on obsolete proprietary electronics.

## Repository structure

```text
/
├── README.md
├── codex.md
└── cd35-gov/
    └── spec/
        ├── spec-current/
        │   ├── index.md
        │   └── <topic>.md
        └── spec-archive/
            └── <version>/
```

`cd35-gov/spec/spec-current/` is the canonical active specification.

`cd35-gov/spec/spec-archive/` contains immutable snapshots of previously promoted specifications.

The rules for creating, changing, promoting, and archiving specifications are defined in [`codex.md`](./codex.md). That file is the project authority for specification governance.

## Current project phase

The project is in **concept / architecture definition**. Dimensions, throughput, chemistry volumes, transport geometry, component selection, and regulatory requirements are not yet frozen.

The current specification should therefore distinguish clearly between:

- accepted requirements;
- current design direction;
- hypotheses requiring validation;
- unresolved engineering questions.
