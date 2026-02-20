# PRD: Skills Collection — Canonical Restructure

**Version**: 1.0
**Date**: 2026-02-20
**Status**: Approved

---

## 1. Overview

This project is a personal collection of AI skills for research, strategy, writing, and communication. The current state is a flat directory of informal markdown files. This PRD formalises the project structure using the Agent Skills open standard format, adding project documentation and progress-tracking infrastructure.

The goal is to make the skills usable with any AI assistant, and natively discoverable by tools that support the Agent Skills format.

---

## 2. Goals and Non-Goals

### Goals

- Convert all existing skill files to canonical `skills/<name>/SKILL.md` format
- Add YAML frontmatter with `name` and `description` to every skill
- Write a README covering generic usage (paste into context) and native tool installation
- Establish an append-only PROGRESS.md build journal
- Establish a CHANGELOG.md following the Keep-a-Changelog standard
- Record the key architectural decision via an ADR
- Ensure no vendor-specific assumptions in documentation

### Non-Goals

- Do not target any single AI vendor or tool in this phase
- Do not add CI/CD, linting, or automated validation in this phase
- Do not create new skills beyond the four already written
- Do not add `references/` or `scripts/` subdirectories unless a skill requires them

---

## 3. Users

**Primary user**: The skill author — someone using one or more AI assistants who wants reusable, high-quality skill prompts available across tools.

**Secondary user**: Anyone cloning or forking this repository who wants to load these skills into their own AI assistant workflow, regardless of vendor.

---

## 4. Feature Requirements

### Phase 1: Restructure (P0 — required)

- [x] Create `skills/research/SKILL.md` from `research-skill.md`
- [x] Create `skills/strategy-author/SKILL.md` from `strategy-author-skill.md`
- [x] Create `skills/remove-ai-slop/SKILL.md` from `remove-ai-slop.md`
- [x] Create `skills/strategic-persuasion/SKILL.md` from `strategic-persuasion-skill.md`
- [x] Each SKILL.md must have YAML frontmatter with `name` and `description`
- [x] Remove the original flat `.md` files after conversion

### Phase 2: Documentation (P0 — required)

- [x] Write `README.md` with skills index, generic usage instructions, native tool install table, and repo structure
- [x] Write `PRD.md` (this document)
- [x] Write `CHANGELOG.md` using Keep-a-Changelog format
- [x] Write `PROGRESS.md` as an append-only session journal

### Phase 3: Architecture Records (P1 — important)

- [x] Write `decisions/0001-adopt-skill-md-standard.md` recording the decision to adopt the open standard format

---

## 5. Success Criteria

- A user can load any skill into any AI assistant by copying the SKILL.md content into their context
- A user with a tool that supports the Agent Skills format can install a skill and invoke it natively
- A new contributor can clone the repo and use a skill within 5 minutes regardless of which AI tool they use
- Documentation makes no assumption about which AI vendor or tool the user is using

---

## 6. Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| `remove-ai-slop` algorithm body was never written | High | Low | Preserve what exists; note incompleteness in PROGRESS.md |
| Description fields too broad — spurious auto-invocation in native tools | Medium | Medium | Write precise, trigger-condition-specific descriptions |
| Agent Skills standard evolves; format becomes outdated | Low | Medium | Pin to known-good format; review on major standard updates |

---

## 7. Timeline

| Phase | Deliverable | Target |
|---|---|---|
| Phase 1 | 4 SKILL.md files created | 2026-02-20 |
| Phase 2 | README, PRD, CHANGELOG, PROGRESS | 2026-02-20 |
| Phase 3 | ADR written | 2026-02-20 |
