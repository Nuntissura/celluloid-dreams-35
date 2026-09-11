---
title: Crossovers and Contamination Control
slug: crossover-contamination
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
  - film-transport
  - wet-process-modules
supersedes: null
---

# Crossovers and Contamination Control

## Purpose

Define transitions between wet stages and control of chemistry carryover, dripping, film tracking, and service contamination.

## Normative requirements

- **XOV-001** — Each transition between incompatible wet stages SHALL include a defined carryover-control method.
- **XOV-002** — Crossover components that contact chemistry or wet film SHALL be removable or readily accessible for cleaning.
- **XOV-003** — Crossover geometry SHALL preserve film tracking without introducing damaging edge load or surface contact.
- **XOV-004** — Carryover limits SHALL be derived from selected chemistry requirements and validated experimentally before being frozen.
- **XOV-005** — Drainage from crossover components SHALL not intentionally return incompatible carryover to an upstream chemistry bath.
- **XOV-006** — Crossover service SHALL be possible without disassembling the complete transport path.

## Current design direction

A standardized crossover module is preferred. Candidate functions include:

- soft squeegee or controlled nip;
- gravity drip zone;
- air knife or low-pressure air assist;
- dedicated drain path;
- replaceable guides.

No specific squeegee material, pressure, or air velocity is frozen until scratch, residue, and carryover testing is performed.

## Risks and failure modes

- Developer carryover changing downstream bath activity.
- Reverse contamination during maintenance.
- Squeegee damage or deposits scratching film.
- Droplets transported into dryer or electronics.
- Excess nip pressure marking softened emulsion.

## Open questions

- Which transitions require active squeegeeing versus drip-only control.
- Acceptable carryover volume per meter of film.
- Whether air knives create drying marks before final wash/rinse.
- Drain routing and waste classification.
