---
title: Open Engineering Questions
slug: open-questions
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
  - scope-and-goals
  - system-architecture
  - module-platform
supersedes: null
---

# Open Engineering Questions

## Purpose

Maintain decisions that are intentionally unresolved so plausible guesses do not silently become architecture.

## Priority A — current architecture blockers

### OQ-001 — Film acquisition method

How should CD35 acquire film from a fully rewound 35 mm cassette inside the daylight intake?

Candidates: internal leader extractor, controlled cassette opening, or hybrid.

### OQ-002 — Primary film transport method

Which wet-film mechanism gives the best combination of low scratching, reliable transport, simple threading, tension control, and recoverable jams?

Candidates: roller/friction, perforation/sprocket, reusable leader/carrier, or hybrid.

### OQ-003 — WBM external interface and process geometry

What common docking datum, port locations, transport coupling location, and thermal interface allow process-specific bath geometry without creating unique chassis connections for every stage?

### OQ-004 — Reference chemistry system

Which commercially supported C-41 chemistry will be the reference process for the first prototype?

This choice is required before freezing bath temperatures, residence times, replenishment, wash sequence, materials, and throughput.

### OQ-013 — TDM standard

Select the motor/gearbox/encoder class and define the machine-level output coupling, mounting datum, electrical connector, power class, and feedback interface.

Required evidence: speed stability, wet transport load, stall behavior, replacement repeatability, availability, and alternate sourcing.

### OQ-014 — TSM architecture

Determine whether the first thermal architecture uses dry-well heater/sensor cartridges, an external recirculating heat exchanger, or another serviceable method.

Required evidence: uniformity, warm-up/recovery, thermal lag, chemical isolation, service replacement, and independent over-temperature protection.

### OQ-015 — FSM and fluid-port architecture

Select the circulation/transfer pump approach and routine-disconnect fluid coupling class. Define role keying, hose sizes, drain behavior, replenishment interface, and service isolation.

Required evidence: chemical compatibility, leak/spill behavior, flow, priming, drain completeness, service replacement, and supply availability.

### OQ-016 — Common electrical/data interface

Define power classes, connector families, module identity, and control/data bus for TDM/TSM/FSM modules without creating unnecessary proprietary electronics.

## Priority B — performance definition

### OQ-005 — Production target

Define rolls/day, sustained rolls/hour, maximum operator time per roll, warm-up time, and acceptable chemistry working volume.

### OQ-006 — Transport speed and path length

Once reference chemistry is selected, determine line speed and immersed path length for each stage.

### OQ-007 — Carryover limits

Measure acceptable liquid carryover at each transition and determine crossover requirements.

### OQ-008 — Drying architecture

Determine airflow, temperature, path length, filtration, and humidity requirements for reliable spot-free output.

### OQ-017 — Service targets

Define maximum replacement-time and post-replacement verification targets for TDM, TSM, FSM, WBM, wet transport racks, and common sensors/pumps.

## Priority C — later platform decisions

### OQ-009 — Control platform

Compare PLC, distributed microcontroller, and hybrid approaches for cost, deterministic behavior, repairability, safety integration, and long-term availability.

### OQ-010 — Module identity

Determine whether module identity uses passive EEPROM, NFC/RFID, keyed hardware coding, controller-node identity, or a combination.

### OQ-011 — Fluid coupling family

Select a chemically compatible, low-cost, serviceable coupling family after chemistry and pressure/flow ranges are known. Non-spill polypropylene quick-disconnect families are current candidates; selection remains unverified.

### OQ-012 — Product envelope — DEFERRED

Countertop, under-counter, floor-standing, or multi-unit form factor is intentionally deferred under `PBR-006` until transport, thermal, fluid, and WBM interfaces are substantially validated.

## Resolution rule

An open question is removed only when its decision is incorporated into the relevant topic specification with supporting evidence or explicit rationale. A decision that creates a normative obligation receives a stable requirement ID in that topic.