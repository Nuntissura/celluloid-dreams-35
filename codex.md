---
title: Celluloid Dreams 35 Project Authority
project: CD35
document_type: governance
authority_level: project
status: current
version: "1.0"
last_updated: 2026-09-11
---

# Celluloid Dreams 35 Project Authority

This file defines how the CD35 engineering specification is structured, changed, promoted, and archived.

## 1. Authority and precedence

When project documents conflict, use this precedence order:

1. `codex.md` — specification governance and repository authority.
2. `cd35-gov/spec/spec-current/index.md` — current specification baseline and topic map.
3. Topic files in `cd35-gov/spec/spec-current/` — authoritative requirements and design decisions for their topic.
4. Archived specifications — historical reference only.
5. Issues, pull-request discussion, notes, chat transcripts, sketches, and other working material — informative unless promoted into the current specification.

A design idea is not authoritative merely because it appears in discussion. It becomes part of the specification only when it is represented in `spec-current` and promoted according to this file.

## 2. Directory model

```text
cd35-gov/
└── spec/
    ├── spec-current/
    │   ├── index.md
    │   └── <topic>.md
    └── spec-archive/
        ├── README.md
        ├── v0.1.0/
        ├── v0.2.0/
        └── ...
```

### `spec-current`

`spec-current` is the single canonical active specification on the default branch.

Edits to `spec-current` on a feature branch are proposals until merged. Once merged, the resulting contents are authoritative.

### `spec-archive`

`spec-archive` contains full snapshots of earlier promoted specifications. Archived snapshots are immutable. Never edit an archived snapshot to correct wording or synchronize it with a newer design.

If an archived specification contains an error, correct the current specification and document the change in the new baseline.

## 3. Specification baseline versions

The specification uses semantic-style baseline versions:

- **MAJOR** — incompatible architecture, interface, or scope change.
- **MINOR** — new requirement, subsystem, interface, or materially changed behavior that remains within the same project architecture.
- **PATCH** — clarification, correction, typo, metadata change, or non-material refinement.

Examples:

- `v0.1.0` — first structured concept specification.
- `v0.2.0` — adds a defined cassette intake interface.
- `v0.2.1` — clarifies a sensor tolerance without changing architecture.
- `v1.0.0` — first engineering baseline considered sufficiently defined for implementation/prototype control.

The current baseline version is declared in `spec-current/index.md`.

## 4. Topic-file rule

The specification is intentionally split by topic. Do not create one monolithic specification document.

Each topic should have one primary Markdown file. Create a new topic file when a subject has its own requirements, interfaces, lifecycle, or engineering decisions.

Good topic boundaries include:

- scope and goals;
- system architecture;
- daylight cassette intake;
- film transport;
- wet-process modules;
- thermal control;
- crossover and contamination control;
- drying;
- controls and software;
- serviceability;
- safety and compliance;
- open engineering questions.

Avoid splitting a topic merely because a document is becoming long. Split when the engineering responsibility is meaningfully different.

## 5. Required YAML frontmatter

Every specification topic file must start with YAML frontmatter using at least these fields:

```yaml
---
title: Human-readable topic title
slug: stable-topic-slug
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
```

### Field meanings

- `title` — human-readable title.
- `slug` — stable lowercase identifier; do not change casually after publication.
- `project` — always `CD35` for this repository.
- `document_type` — `spec-topic` for topic files.
- `status` — `current`, `deprecated`, or `reserved` in the promoted specification. Draft/review state is represented by branch/PR state rather than by silently changing authority on `main`.
- `maturity` — recommended values: `concept`, `prototype`, `validated`, `production`.
- `last_promoted_in` — baseline version in which this topic was last materially promoted.
- `topic_revision` — monotonically increasing revision integer for that topic.
- `last_updated` — ISO date of the latest promoted edit.
- `owners` — responsible people or `unassigned`.
- `depends_on` — slugs of topic files whose interfaces or requirements this topic depends on.
- `supersedes` — prior topic slug if this file replaces a differently named topic; otherwise `null`.

Additional frontmatter fields may be added when useful, but the required fields above should remain stable.

## 6. Requirement identifiers

Normative requirements should use stable IDs so they can be referenced from design notes, tests, issues, and future CAD/electrical documentation.

Format:

```text
<TOPIC>-NNN
```

Examples:

- `SCP-001` — scope requirement.
- `SYS-004` — system architecture requirement.
- `INT-012` — intake requirement.
- `TRN-006` — transport requirement.
- `WET-015` — wet-module requirement.
- `THM-003` — thermal requirement.

Do not renumber existing requirement IDs merely to make a list visually continuous. Retired IDs stay retired.

Use normative wording deliberately:

- **MUST / SHALL** — required for conformance.
- **MUST NOT / SHALL NOT** — prohibited.
- **SHOULD** — preferred unless a documented reason justifies deviation.
- **MAY** — optional.

## 7. Topic-file structure

A topic file should normally contain, in this order:

1. Purpose.
2. Scope.
3. Normative requirements.
4. Current design direction.
5. Interfaces with other topics.
6. Validation / acceptance criteria when known.
7. Risks and failure modes.
8. Open questions.
9. Decision history when useful.

Do not present an unverified engineering assumption as a requirement or established fact. Mark it explicitly as a hypothesis or open question.

## 8. Creating a new specification topic

To add a topic:

1. Create a branch for the proposed specification change.
2. Add `<topic>.md` under `cd35-gov/spec/spec-current/`.
3. Add complete YAML frontmatter.
4. Assign a stable topic slug and requirement-ID prefix.
5. Add the topic to `spec-current/index.md`.
6. Document dependencies on other topics.
7. Add normative requirements only where the requirement is sufficiently defined to be testable or reviewable.
8. Put unresolved choices under `Open questions` rather than inventing precision.
9. Choose the baseline version that the change will promote to.
10. Review the complete spec for contradictions before merge.

## 9. Editing an existing topic

When a topic changes materially:

1. Increment `topic_revision`.
2. Set `last_promoted_in` to the target baseline version.
3. Update `last_updated`.
4. Preserve existing requirement IDs whenever the underlying requirement still represents the same obligation.
5. Add new IDs for genuinely new requirements.
6. Retire obsolete requirements explicitly instead of silently reusing their IDs for different meanings.
7. Update related topic files if an interface contract changed.
8. Update the current index summary and baseline notes.

## 10. Promotion procedure

A specification promotion is the act of making proposed specification changes authoritative on the default branch.

Before promoting baseline `vNEW` from current baseline `vOLD`:

1. Ensure the proposal branch contains all intended topic and index changes.
2. Review the changed requirements for internal contradictions and unresolved interface mismatches.
3. Create a complete, byte-for-byte snapshot of the **pre-promotion** `spec-current/` tree at:

   ```text
   cd35-gov/spec/spec-archive/vOLD/
   ```

4. Do not modify the copied snapshot after it is created.
5. Update `spec-current/index.md` to declare `vNEW`.
6. Ensure materially modified topic files declare `last_promoted_in: "NEW"` and increment their `topic_revision`.
7. Record a concise promotion summary in the index.
8. Merge the proposal.

The archive therefore records the specification that was replaced, not a rewritten approximation of it.

### Initial baseline exception

For the first baseline, there is no predecessor to archive. `v0.1.0` may therefore be created without an archive snapshot. The first archive is created when `v0.1.0` is superseded.

## 11. Archive rules

Archived specification directories:

- MUST be complete snapshots of `spec-current` at the time they ceased to be current;
- MUST use a version directory such as `v0.1.0`;
- MUST NOT be edited after archival;
- MUST NOT be used as the source of current requirements when a newer current specification exists;
- MAY be cited to explain historical design decisions.

Do not store drafts in `spec-archive`. Git history and proposal branches/PRs already preserve draft evolution.

## 12. Index rules

`spec-current/index.md` is the entry point to the active specification. It must contain:

- project name and code;
- current baseline version;
- baseline date;
- maturity;
- topic table with links;
- concise system definition;
- cross-topic constraints;
- unresolved high-level decisions;
- promotion summary/change notes.

The index should summarize and navigate. Detailed requirements belong in topic files.

## 13. Evidence and verification

CD35 follows a verification-first engineering rule:

- Do not convert a plausible assumption into a factual statement without verification.
- Manufacturer chemistry specifications, dimensional standards, component datasheets, measurements, prototypes, and controlled tests outrank recollection or analogy.
- When a value has not been verified, label it `TBD`, `target`, `estimate`, or `hypothesis` as appropriate.
- Record the provenance of safety-critical, chemistry-critical, dimensional, or timing values in the relevant topic.

## 14. Change discipline

Prefer small, reviewable specification changes.

A specification change should answer:

- What changed?
- Why did it change?
- Which requirements or interfaces are affected?
- What evidence supports the change?
- What remains unresolved?

Do not hide architecture changes inside wording cleanups.

## 15. Project vocabulary

Use these terms consistently unless the specification explicitly redefines them:

- **CD35** — Celluloid Dreams 35 project.
- **processor** — complete machine.
- **module** — replaceable subsystem with a defined mechanical/electrical/fluid interface.
- **wet module** — removable process-bath subsystem.
- **transport module** — subsystem that controls film movement through or between stages.
- **intake** — daylight cassette-loading and film-acquisition subsystem.
- **crossover** — transition between wet stages, including carryover control.
- **baseline** — a promoted, versioned specification state.
- **current specification** — the contents of `spec-current` on the default branch.
