---
title: CD35 Codex Authority
project: CD35
document_type: governance
status: current
rule_prefix: AUTH
version: "1.0"
last_updated: 2026-09-11
---

# CD35 Codex Authority

## Rules

- **AUTH-001** — The normative files listed in `codex/README.md`, together with the root `codex.md` entry point, constitute the project codex and govern repository behavior, specification workflow, and cross-cutting product build constraints.
- **AUTH-002** — When project documents conflict, precedence SHALL be: codex authority and rules; current specification index; current specification topic files; archived specifications; issues, pull requests, notes, chat transcripts, sketches, and other working material.
- **AUTH-003** — Every normative codex rule SHALL have a stable rule ID using the prefix assigned to its codex document.
- **AUTH-004** — A published rule ID SHALL NOT be reused for a different obligation. Retired IDs remain retired; materially different obligations receive new IDs.
- **AUTH-005** — Material changes to codex rules SHALL be made on a branch and reviewed through a pull request before becoming authoritative on the default branch.
- **AUTH-006** — A specification MAY define a justified exception where a codex rule explicitly permits engineering judgment, but the exception SHALL cite the affected rule ID and document the technical reason. A specification SHALL NOT silently contradict the codex.
- **AUTH-007** — Safety requirements SHALL NOT be weakened solely to satisfy modularity, cost, interchangeability, or off-the-shelf-part preferences.
- **AUTH-008** — Unverified engineering assumptions SHALL be identified as `TBD`, `target`, `estimate`, `candidate`, or `hypothesis` as appropriate and SHALL NOT be represented as verified fact.
- **AUTH-009** — Manufacturer specifications, recognized standards, measurements, controlled tests, and validated prototypes SHALL outrank recollection, analogy, or plausible inference when establishing technical facts.
- **AUTH-010** — Project terminology and identifiers SHALL remain stable unless a deliberate migration is documented and all authoritative references are updated.

## Authority boundary

The codex defines *how CD35 is designed and governed*. The current specification defines *what the current CD35 baseline requires*. Detailed implementation choices belong in specifications and engineering artifacts unless they are intentionally elevated into a cross-project build rule.