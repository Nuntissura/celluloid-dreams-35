---
title: Scope and Goals
slug: scope-and-goals
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.1.0"
topic_revision: 1
last_updated: 2026-09-11
owners:
  - unassigned
depends_on: []
supersedes: null
---

# Scope and Goals

## Purpose

Define what the first CD35 machine is intended to do and what is deliberately outside its initial scope.

## Normative requirements

- **SCP-001** — The first CD35 processor SHALL support 35 mm photographic film only.
- **SCP-002** — Normal operator use SHALL NOT require a darkroom or changing bag.
- **SCP-003** — The initial process target SHALL be C-41 color-negative processing.
- **SCP-004** — The machine SHALL be designed for repeatable commercial production use rather than occasional hobby batch processing.
- **SCP-005** — The architecture SHALL prioritize low operator handling time, serviceability, and replaceable modules.
- **SCP-006** — The design SHALL NOT require support for 120, 220, sheet film, APS, E-6, or black-and-white processing in the first implementation.
- **SCP-007** — Unverified performance values SHALL be identified as targets, estimates, hypotheses, or TBD rather than presented as established requirements.

## Current design direction

The intended user is a photo store or small lab processing a meaningful but not industrial-scale daily volume of 35 mm film. The system should automate the work after cassette insertion and minimize manual film handling.

## Non-goals for v0.x

- universal film-format support;
- automatic scanning;
- automatic sleeving or cutting;
- support for every C-41 chemistry family without validation;
- maximum possible rolls per hour;
- decorative or enthusiast-oriented operation at the expense of throughput and serviceability.

## Open questions

- Target daily roll volume.
- Target continuous throughput.
- Maximum acceptable operator seconds per roll.
- Whether the first prototype must be countertop, floor-standing, or either.
- Target manufacturing cost and retail price.
