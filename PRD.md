# PRD: Skills Collection — Canonical Restructure

**Version**: 1.0
**Date**: 2026-02-20
**Status**: Approved

---

## 1. Overview

This project is a personal collection of Claude Code skills for research, strategy, writing, and communication. The current state is a flat directory of informal markdown files. This PRD formalises the project structure using the canonical Claude Code Agent Skills format, adding project documentation and progress-tracking infrastructure.

The goal is to make the skills discoverable, installable, and maintainable as a proper skills repository.

---

## 2. Goals and Non-Goals

### Goals

- Convert all existing skill files to canonical `skills/<name>/SKILL.md` format
- Add YAML frontmatter with `name` and `description` to every skill
- Write a README with a skills index, installation instructions, and usage examples
- Establish an append-only PROGRESS.md build journal
- Establish a CHANGELOG.md following the Keep-a-Changelog standard
- Record the key architectural decision via an ADR

### Non-Goals

- Do not publish to the Claude plugin marketplace in this phase
- Do not add CI/CD, linting, or automated validation in this phase
- Do not create new skills beyond the four already written
- Do not add `references/` or `scripts/` subdirectories unless a skill requires them

---

## 3. Users

**Primary user**: The skill author — a single developer using Claude Code who wants their skills available via slash command and auto-invocation.

**Secondary user**: Anyone cloning or forking this repository who wants to install the skills into their own Claude Code environment.

---

## 4. Feature Requirements

### Phase 1: Restructure (P0 — required)

- [ ] Create `skills/research/SKILL.md` from `research-skill.md`
- [ ] Create `skills/strategy-author/SKILL.md` from `strategy-author-skill.md`
- [ ] Create `skills/remove-ai-slop/SKILL.md` from `remove-ai-slop.md`
- [ ] Create `skills/strategic-persuasion/SKILL.md` from `strategic-persuasion-skill.md`
- [ ] Each SKILL.md must have YAML frontmatter with `name` and `description`
- [ ] Remove the original flat `.md` files after conversion

### Phase 2: Documentation (P0 — required)

- [ ] Write `README.md` with skills index table, installation guide, usage examples, and repo structure
- [ ] Write `PRD.md` (this document)
- [ ] Write `CHANGELOG.md` using Keep-a-Changelog format
- [ ] Write `PROGRESS.md` as an append-only session journal

### Phase 3: Architecture Records (P1 — important)

- [ ] Write `decisions/0001-adopt-skill-md-standard.md` recording the decision to adopt the canonical format

---

## 5. Success Criteria

- All four skills are invocable via `/skill-name` in Claude Code after installation to `~/.claude/skills/`
- A new contributor can clone the repo, follow the README, and have all skills working in under 5 minutes
- The `description` field of each skill is accurate enough that Claude auto-invokes it without an explicit slash command when context matches

---

## 6. Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| `remove-ai-slop.md` was incomplete | High | Low | Preserve what exists; note incompleteness in PROGRESS.md |
| Description fields too broad — spurious auto-invocation | Medium | Medium | Write precise, trigger-condition-specific descriptions |

---

## 7. Timeline

| Phase | Deliverable | Target |
|---|---|---|
| Phase 1 | 4 SKILL.md files created | 2026-02-20 |
| Phase 2 | README, PRD, CHANGELOG, PROGRESS | 2026-02-20 |
| Phase 3 | ADR written | 2026-02-20 |
