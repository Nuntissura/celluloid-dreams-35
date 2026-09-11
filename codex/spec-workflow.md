---
title: CD35 Specification Workflow
project: CD35
document_type: governance
status: current
rule_prefix: WF
version: "1.0"
last_updated: 2026-09-11
---

# CD35 Specification Workflow

## Rules

- **WF-001** — The engineering specification SHALL be split into topic files rather than maintained as one monolithic document.
- **WF-002** — Every current specification topic file SHALL begin with YAML frontmatter containing at least `title`, `slug`, `project`, `document_type`, `status`, `maturity`, `last_promoted_in`, `topic_revision`, `last_updated`, `owners`, `depends_on`, and `supersedes`.
- **WF-003** — Normative product requirements SHALL use stable requirement IDs in the form `<TOPIC>-NNN`; published IDs SHALL NOT be renumbered or reused for different obligations.
- **WF-004** — Normative wording SHALL use `SHALL`/`MUST` for required behavior, `SHALL NOT`/`MUST NOT` for prohibitions, `SHOULD` for preferred behavior with allowable justification, and `MAY` for optional behavior.
- **WF-005** — A new topic SHALL receive a stable slug, a unique requirement-ID prefix, declared dependencies, and an entry in `cd35-gov/spec/current/index.md` before promotion.
- **WF-006** — A materially changed topic SHALL increment `topic_revision`, update `last_updated`, and set `last_promoted_in` to the target baseline version.
- **WF-007** — A requirement that no longer applies SHALL be retired explicitly rather than silently assigning its ID to new behavior.
- **WF-008** — Specification baselines SHALL use semantic-style versions: MAJOR for incompatible architecture or scope changes, MINOR for material new or changed behavior within the architecture, and PATCH for non-material corrections or clarifications.
- **WF-009** — Before promoting `vNEW`, the complete pre-promotion `current/` tree for `vOLD` SHALL be copied byte-for-byte to `cd35-gov/spec/archive/vOLD/` unless no predecessor exists.
- **WF-010** — An archived baseline SHALL NOT be modified after archival. Corrections SHALL be made only in a later current baseline.
- **WF-011** — Every baseline promotion SHALL update `current/index.md` with the new version, date, topic map when changed, and a concise promotion summary.
- **WF-012** — Unresolved architecture decisions SHALL remain in `open-questions.md` or an explicitly marked open-question section rather than being converted into false precision.
- **WF-013** — Safety-critical, chemistry-critical, dimensional, timing, compatibility, and performance values SHALL cite or record their evidence source before being frozen as verified requirements.
- **WF-014** — A wording-only or cleanup change SHALL NOT conceal a material architecture or interface change; material changes require the corresponding baseline classification and topic revision.
- **WF-015** — Material specification promotions SHALL be proposed on a branch, reviewed as a pull request, and merged before the new baseline becomes authoritative.
- **WF-016** — Draft/review state SHALL be represented by branch and pull-request state; files in `current/` on the default branch are authoritative regardless of informal discussion elsewhere.
- **WF-017** — When a specification intentionally departs from a `SHOULD` codex build rule, the specification SHALL cite the rule ID and document the engineering justification.
- **WF-018** — Topic files SHOULD separate normative requirements, current design direction, interfaces, validation criteria, risks/failure modes, and open questions so hypotheses are not mistaken for requirements.
- **WF-019** — The current index SHALL summarize and navigate; detailed subsystem requirements SHALL remain in their topic files.
- **WF-020** — Before promotion, affected topic files SHALL be checked for contradictory interface assumptions and stale open questions.

## Required frontmatter template

```yaml
---
title: Human-readable topic title
slug: stable-topic-slug
project: CD35
document_type: spec-topic
status: current
maturity: concept
last_promoted_in: "0.2.0"
topic_revision: 1
last_updated: 2026-09-11
owners:
  - unassigned
depends_on: []
supersedes: null
---
```

## Normal topic structure

1. Purpose
2. Scope
3. Normative requirements
4. Current design direction
5. Interfaces
6. Validation / acceptance criteria
7. Risks and failure modes
8. Open questions
9. Decision history when useful

This structure is recommended rather than mandatory when another structure communicates the engineering topic more clearly.