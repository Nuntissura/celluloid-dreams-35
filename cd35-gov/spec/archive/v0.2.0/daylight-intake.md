---
title: Daylight Intake
slug: daylight-intake
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

# Daylight Intake

## Purpose

Define the subsystem that accepts a 35 mm cassette in room light and transfers the exposed film into the processor without requiring a darkroom.

## Normative requirements

- **INT-001** — The operator SHALL be able to insert a 35 mm cassette in normal room light.
- **INT-002** — The intake SHALL provide a light-tight chamber before any operation that can expose unprocessed film.
- **INT-003** — The machine SHALL prevent film acquisition while the intake chamber is not confirmed closed and light-tight.
- **INT-004** — The intake SHALL accommodate a fully rewound cassette without requiring the operator to leave the film leader protruding.
- **INT-005** — The acquisition mechanism SHALL minimize contact with image-bearing film surfaces.
- **INT-006** — The intake SHALL detect or otherwise reliably determine completion of film extraction before separating film from the cassette spool.
- **INT-007** — A jam or power loss SHALL NOT intentionally expose unprocessed film to ambient light.
- **INT-008** — Cassette opening, leader retrieval, spool separation, and film attachment methods remain implementation choices until validated by prototype testing.

## Current design direction

Candidate sequence:

```text
insert cassette
      |
close and interlock chamber
      |
acquire film / leader internally
      |
attach film to transport path
      |
pull film from cassette
      |
detect end
      |
separate from spool
      |
process
```

The intake should be treated as an exchangeable subsystem so multiple acquisition mechanisms can be prototyped without redesigning the wet-processing chassis.

## Risks and failure modes

- Film leader cannot be retrieved.
- Cassette shell is dented or non-standard.
- Film is torn or partially rewound.
- Film end remains strongly taped or attached to spool.
- Static, scratching, or excessive film tension during extraction.
- Door/light seal failure.

## Open questions

- Mechanical leader extractor versus cassette-opening mechanism.
- Whether the cassette remains intact after processing intake.
- Best method for detecting film end and spool attachment.
- Whether DX coding should be read for process metadata.
