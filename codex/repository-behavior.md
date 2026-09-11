---
title: CD35 Repository Behavior
project: CD35
document_type: governance
status: current
rule_prefix: REP
version: "1.0"
last_updated: 2026-09-11
---

# CD35 Repository Behavior

## Rules

- **REP-001** — The repository root SHALL keep `README.md` as the human project entry point and `codex.md` as the stable authority entry point.
- **REP-002** — Normative governance documents SHALL live under `codex/`; the root `codex.md` SHALL remain a concise bootstrap document rather than duplicating the full rule set.
- **REP-003** — The active engineering specification SHALL live under `cd35-gov/spec/current/` and superseded baseline snapshots SHALL live under `cd35-gov/spec/archive/<version>/`.
- **REP-004** — Repository paths for Markdown engineering documents SHOULD use lowercase kebab-case names except conventional root names such as `README.md`.
- **REP-005** — `cd35-gov/spec/current/` SHALL contain only the canonical active specification baseline, not drafts or abandoned alternatives.
- **REP-006** — Files under `cd35-gov/spec/archive/` SHALL be treated as immutable historical records after creation.
- **REP-007** — Draft concepts, experiments, calculations, and design explorations SHALL NOT become authoritative merely by being committed; they become requirements only through the specification workflow.
- **REP-008** — Material codex or specification changes SHALL be developed on a non-default branch and SHALL reach the default branch through a pull request.
- **REP-009** — Commits SHOULD be scoped so that one commit represents one understandable governance, specification, implementation, or evidence change where practical.
- **REP-010** — File moves or renames SHALL update authoritative relative links and references in the same change set.
- **REP-011** — Generated artifacts, exports, binaries, and temporary files SHOULD NOT be committed unless they are required project deliverables or reproducibility inputs.
- **REP-012** — Source engineering files and editable originals SHOULD be preferred over opaque exports when both represent the same project artifact.
- **REP-013** — Repository history on the default branch SHOULD be preserved; destructive history rewrites SHALL NOT be used as a routine way to correct published project records.
- **REP-014** — A material architecture change SHOULD identify the affected specification topics, codex rules, open questions, and validation work in its pull-request description.
- **REP-015** — When a path or document is designated as authoritative by the codex, duplicate shadow copies SHALL NOT be maintained elsewhere in the repository.

## Current repository model

```text
/
├── README.md
├── codex.md
├── codex/
│   ├── README.md
│   ├── authority.md
│   ├── repository-behavior.md
│   ├── spec-workflow.md
│   └── product-build-rules.md
└── cd35-gov/
    └── spec/
        ├── current/
        └── archive/
```