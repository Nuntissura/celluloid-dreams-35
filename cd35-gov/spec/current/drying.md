---
title: Drying
slug: drying
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
  - crossover-contamination
supersedes: null
---

# Drying

## Purpose

Define the final drying subsystem that accepts washed/rinsed film and outputs a dry negative suitable for subsequent handling or scanning.

## Normative requirements

- **DRY-001** — The processor SHALL output film sufficiently dry for normal post-process handling under the defined operating environment.
- **DRY-002** — Drying SHALL avoid temperatures or mechanical loads that can damage film base or emulsion.
- **DRY-003** — Air contacting wet film SHOULD be filtered to reduce dust deposition.
- **DRY-004** — Dryer air temperature SHALL be monitored and controlled when active heating is used.
- **DRY-005** — Heater operation SHALL include independent over-temperature protection.
- **DRY-006** — Condensate or liquid carried into the dryer SHALL be prevented from reaching electrical components.
- **DRY-007** — Airflow components and filters SHALL be serviceable without exposing upstream chemistry modules to contamination.

## Current design direction

Candidate dryer architecture:

```text
wet film
   |
liquid-removal crossover
   |
filtered forced air
   |
controlled heating if required
   |
dry-film output
```

Drying time, air temperature, velocity, filtration class, and chamber length are not yet frozen.

## Open questions

- Heated versus primarily high-volume ambient air.
- Dryer geometry required for continuous line speed.
- Filter class and replacement interval.
- Humidity sensing and environmental compensation.
- Whether film exits as a hanging strip, controlled loop, or guided flat path.
