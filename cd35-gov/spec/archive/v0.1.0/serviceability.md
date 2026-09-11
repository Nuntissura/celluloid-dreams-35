---
title: Serviceability and Modularity
slug: serviceability
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.1.0"
topic_revision: 1
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - system-architecture
  - wet-process-modules
  - film-transport
supersedes: null
---

# Serviceability and Modularity

## Purpose

Define maintainability requirements intended to prevent CD35 from becoming dependent on scarce proprietary parts or specialist service procedures.

## Normative requirements

- **SRV-001** — Components that routinely contact processing chemistry SHALL be removable, cleanable, or replaceable without dismantling the complete processor.
- **SRV-002** — Repeated motors, pumps, sensors, heaters, and drive electronics SHOULD use standardized part families where practical.
- **SRV-003** — Routine replacement parts SHOULD be commercially available components with documented specifications rather than project-unique parts where no technical advantage justifies uniqueness.
- **SRV-004** — A failed module SHOULD be replaceable as a unit so production can resume before component-level repair is completed.
- **SRV-005** — Service connectors SHALL be keyed, labeled, or mechanically differentiated where an incorrect connection could damage the machine, contaminate chemistry, or create a safety hazard.
- **SRV-006** — Wear components SHALL be accessible for visual inspection.
- **SRV-007** — Calibration procedures for critical sensors SHALL be documented and executable without proprietary external service software where practical.
- **SRV-008** — The project SHALL maintain interface documentation sufficient to source or manufacture compatible replacement modules.
- **SRV-009** — Routine cleaning SHALL NOT require removal of unrelated electrical assemblies.

## Current design direction

The preferred machine model is a chassis containing standardized replaceable subsystems, for example:

- wet module;
- transport rack;
- motor/drive pod;
- crossover module;
- temperature-probe cartridge;
- pump cartridge;
- control node.

Module boundaries should follow actual service tasks rather than aesthetic enclosure boundaries.

## Design principle

> Nothing that routinely touches chemistry should require major machine disassembly to service.

This is a design goal, not permission to compromise guarding, light-tightness, or structural integrity.

## Open questions

- Maximum service time targets for each module type.
- Tool-free versus common-tool module removal.
- Spare-parts strategy for a production installation.
- Which components justify custom manufacture because commodity parts cannot meet chemical, dimensional, or reliability requirements.
