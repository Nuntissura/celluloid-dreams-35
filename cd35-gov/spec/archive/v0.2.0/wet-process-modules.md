---
title: Wet-Process Modules
slug: wet-process-modules
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.2.0"
topic_revision: 2
last_updated: 2026-09-11
owners:
  - unassigned
depends_on:
  - system-architecture
  - module-platform
  - film-transport
  - thermal-control
  - fluid-handling
supersedes: null
---

# Wet-Process Modules

## Purpose

Define the standardized `WBM` Wet Bath Module: the chemistry vessel, local wet film path, and receiving interfaces for transport, thermal, and fluid-service systems.

## Normative requirements

- **WET-001** — Wet-process stages SHALL use a standardized external `WBM` interface wherever stage-specific chemistry does not make that impractical.
- **WET-002** — A `WBM` SHALL provide defined mechanical docking datums and retention features to the processor platform.
- **WET-003** — A `WBM` SHALL expose fluid ports according to `fluid-handling.md` rather than relying on permanently attached cross-machine hoses.
- **WET-004** — A temperature-controlled `WBM` SHALL provide the defined receiving interface for replaceable thermal sensing/heating hardware.
- **WET-005** — Wet film guides, rollers, racks, or sprockets SHALL be removable for cleaning or replacement without discarding the bath vessel where practical.
- **WET-006** — A `WBM` intended for routine exchange SHALL be removable after isolation/disconnection without cutting tubing, desoldering wiring, or dismantling adjacent stages.
- **WET-007** — Pumps, motors, heater electronics, and other likely service-failure components SHOULD remain outside the bath vessel unless integration provides a documented process or safety advantage.
- **WET-008** — Wetted materials SHALL be validated for compatibility with the assigned process chemistry.
- **WET-009** — The vessel SHALL provide controlled complete or near-complete draining through the defined low-point fluid interface.
- **WET-010** — Internal wetted surfaces SHALL avoid unnecessary crevices, inaccessible dead volumes, and service geometries that make routine cleaning impractical.
- **WET-011** — External module identity SHALL indicate module type, interface revision, and assigned process role.
- **WET-012** — Standardized external interfaces SHALL NOT require every stage to have identical internal volume, film-path length, or thermal hardware; process-specific internal geometry MAY vary while preserving the service interface.
- **WET-013** — Incorrect placement of chemically incompatible or interface-incompatible wet modules SHOULD be detectable before processing begins.
- **WET-014** — Wet module design SHALL comply with `PBR-020` through `PBR-026`.

## Current design direction

The preferred `WBM` is intentionally as passive as practical:

```text
┌──────────────────────────────┐
│ WBM wet bath module          │
│                              │
│ removable wet transport rack │
│ chemistry vessel             │
│ fluid port block             │
│ thermal well/interface       │
│ low-point drain geometry     │
│ identity / stage marking     │
└──────────────────────────────┘
       ↑          ↑         ↑
      TDM        TSM       FSM
   dry drive   thermal   fluid service
```

This keeps the high-maintenance motor, pump, heater/sensor service hardware out of the vessel where feasible. The bath becomes cheaper to swap, clean, or replace.

## Standardization boundary

The goal is **common external interfaces**, not artificially identical process tanks. Developer, bleach, fixer, wash, and rinse may ultimately require different immersed path lengths, volumes, agitation, overflow behavior, or thermal capability. Those differences should be implemented behind a common chassis/service interface when practical.

## Validation

Wet-module validation should include:

- leak and drain testing;
- chemical compatibility;
- repeated docking/removal;
- transport-rack alignment after replacement;
- cleaning access;
- dead-volume assessment;
- module misplacement detection;
- thermal and fluid interface repeatability.

## Open questions

- Common external module envelope and datum system.
- Minimum practical working volume.
- Internal film-path cassette/rack standard.
- Whether wash/rinse stages use the identical WBM shell or a simplified compatible variant.
- Material and manufacturing process for prototype versus production bath vessels.
- Module identity implementation.