---
title: Open Engineering Questions
slug: open-questions
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
  - scope-and-goals
  - system-architecture
supersedes: null
---

# Open Engineering Questions

## Purpose

Maintain high-level decisions that are intentionally unresolved. This file prevents guesses from silently becoming architecture.

## Priority A — architecture blockers

### OQ-001 — Film acquisition method

How should CD35 acquire film from a fully rewound 35 mm cassette inside the daylight intake?

Candidates:

- internal leader extractor;
- controlled cassette opening;
- hybrid mechanism.

Required evidence: success rate across representative cassette types, scratch inspection, jam recovery, and operator workflow testing.

### OQ-002 — Primary film transport method

Which method gives the best combination of low scratching, reliable wet transport, simple threading, and controlled tension?

Candidates:

- roller/friction transport;
- perforation/sprocket transport;
- reusable leader/carrier;
- hybrid.

### OQ-003 — Wet-module geometry

What common bath volume, depth, width, and docking geometry produces useful residence time without making the processor unnecessarily large or chemically wasteful?

### OQ-004 — Chemistry system

Which commercially supported C-41 chemistry will be the reference process for the first prototype?

This choice is required before freezing bath temperatures, residence times, replenishment, wash sequence, and compatible materials.

## Priority B — performance definition

### OQ-005 — Production target

Define:

- rolls/day target;
- sustained rolls/hour target;
- maximum operator time per roll;
- warm-up time target;
- acceptable chemistry working volume.

### OQ-006 — Transport speed and path length

Once the chemistry process is selected, determine the line speed and immersed path length required for each stage.

### OQ-007 — Carryover limits

Measure acceptable liquid carryover at each process transition and determine which crossovers require squeegees, drip zones, air assist, or another method.

### OQ-008 — Drying architecture

Determine airflow, temperature, path length, filtration, and humidity requirements for reliable spot-free output at design line speed.

## Priority C — platform and service decisions

### OQ-009 — Control platform

Compare PLC, distributed microcontroller, and hybrid approaches for cost, deterministic behavior, repairability, safety integration, and long-term component availability.

### OQ-010 — Module identity

Determine whether module identity should use passive EEPROM, NFC/RFID, keyed hardware coding, controller-node identity, or a combination.

### OQ-011 — Fluid connection standard

Identify a chemically compatible, low-cost, serviceable drain/fill/replenishment coupling family. Prototype taps are acceptable before production connection hardware is selected.

### OQ-012 — Product envelope

Determine whether the first production-oriented prototype should be countertop, under-counter, floor-standing, or modular across multiple physical units.

## Resolution rule

An open question is removed from this file only when its decision is incorporated into the relevant topic specification with supporting evidence or an explicit design rationale. If the decision creates a normative obligation, it must receive a stable requirement ID in that topic.
