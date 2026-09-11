---
title: Wet-Process Modules
slug: wet-process-modules
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.3.0"
topic_revision: 3
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

Define the standardized `WBM` Wet Bath Module as the chemistry vessel and receiving structure for separately serviceable transport, thermal, fluid, and sensing functions.

## Normative requirements

- **WET-001** — Wet-process stages SHALL use a standardized external `WBM` interface wherever stage-specific chemistry does not make that impractical.
- **WET-002** — A `WBM` SHALL provide defined mechanical docking datums and retention features to the processor platform.
- **WET-003** — A `WBM` SHALL expose fluid ports according to `fluid-handling.md` rather than relying on permanently attached cross-machine hoses.
- **WET-004** — A temperature-controlled `WBM` SHALL provide a defined thermal receiving interface for the `TSM` architecture selected in `thermal-control.md`.
- **WET-005** — The wet film path SHALL be implemented as a removable `TRM` Transport Rack Module wherever practical rather than being permanently built into the WBM vessel.
- **WET-006** — A `WBM` intended for routine exchange SHALL be removable after isolation/disconnection without cutting tubing, desoldering wiring, or dismantling adjacent stages.
- **WET-007** — Pumps, motors, heater electronics, and other likely service-failure components SHOULD remain outside the bath vessel unless integration provides a documented process or safety advantage.
- **WET-008** — Wetted materials SHALL be validated for compatibility with the assigned process chemistry.
- **WET-009** — The vessel SHALL provide controlled complete or near-complete draining through the defined low-point fluid interface.
- **WET-010** — Internal wetted surfaces SHALL avoid unnecessary crevices, inaccessible dead volumes, and service geometries that make routine cleaning impractical.
- **WET-011** — External module identity SHALL indicate module type, interface revision, and assigned process role.
- **WET-012** — Standardized external interfaces SHALL NOT require every stage to have identical internal volume, film-path length, or thermal capability; process-specific internal geometry MAY vary while preserving the service interface.
- **WET-013** — Incorrect placement of chemically incompatible or interface-incompatible wet modules SHOULD be detectable before processing begins.
- **WET-014** — Wet module design SHALL comply with `PBR-020` through `PBR-026`.
- **WET-015** — A `WBM` that requires active temperature control SHALL provide a deliberate, repeatable thermal-contact surface or other defined thermal interface rather than relying on incidental heat transfer through an uncontrolled vessel wall.
- **WET-016** — A `WBM` SHALL provide a defined receiving interface for level sensing where low level, overflow, or loss of prime can create process, equipment, or safety risk.
- **WET-017** — Level sensing MAY be implemented as a standardized service cartridge rather than as a top-level module, but it SHALL be replaceable and testable independently of the bath vessel where practical.
- **WET-018** — Removing or replacing a `TRM` SHALL NOT require discarding or replacing the `WBM` vessel.

## Current design direction

The preferred `WBM` is intentionally passive:

```text
┌──────────────────────────────┐
│ WBM wet bath module          │
│                              │
│ TRM receiving datums         │
│ chemistry vessel             │
│ standardized fluid port block│
│ defined thermal face         │
│ level-sensor receiving point │
│ low-point drain geometry     │
│ identity / stage marking     │
└──────────────────────────────┘
      ↑       ↑       ↑       ↑
     TRM     TSM     FSM    sensing
```

The `WBM` is not the motor module, pump module, heater module, or transport rack. It is the chemically compatible vessel that presents stable interfaces to those serviceable systems.

## Thermal interface direction

For the preferred conductive prototype, the WBM should include a deliberate thermal-transfer feature such as a chemically compatible thermally conductive wall/insert/interface plate connected to the process solution and mechanically repeatable at the TSM docking surface.

The exact material stack, seal strategy, manufacturing method, and contact-pressure mechanism remain unverified and must be tested. A tempering-water jacket/bath remains a fallback architecture if conductive docking cannot meet thermal performance requirements.

## Standardization boundary

The goal is **common external interfaces**, not artificially identical process tanks. Developer, bleach, fixer, wash, and rinse may ultimately require different immersed path lengths, volumes, agitation, overflow behavior, or thermal capability. Those differences should be implemented behind a common chassis/service interface when practical.

Similarly, TRMs may have stage-specific internal path geometry while sharing a common mounting and drive interface.

## Validation

Wet-module validation should include:

- leak and drain testing;
- chemical compatibility;
- repeated docking/removal;
- TRM docking/alignment after replacement;
- cleaning access;
- dead-volume assessment;
- module misplacement detection;
- fluid interface repeatability;
- thermal-contact repeatability after redocking;
- level-sensor replacement and fault testing.

## Open questions

- Common external module envelope and datum system.
- Minimum practical working volume.
- TRM-to-WBM rack datum and retention standard.
- Thermal-face material and manufacturing method.
- Level-sensor technology and receiving geometry.
- Whether wash/rinse stages use the identical WBM shell or a simplified compatible variant.
- Material and manufacturing process for prototype versus production bath vessels.
- Module identity implementation.