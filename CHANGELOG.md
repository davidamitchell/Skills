# Changelog

All notable changes to this project will be documented in this file.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Changed

- `research/SKILL.md`: expanded composability instructions to detail citation-discipline and speculation-control integration points; added Constraint Parameter section (full/bounded/rapid modes with per-mode evidence sufficiency criteria); added Source Prioritisation Heuristic; added Confidence Calibration table (high/medium/low) with per-finding labelling requirement; added Output Calibration section mapping constraint mode to synthesis depth; added Tool Awareness note referencing AGENTS.md § MCP Configuration; updated Section 2 evidence sufficiency criteria to reference the constraint parameter table
- `strategy-author/SKILL.md`: added Research-to-Diagnosis Translation process (critical constraint extraction, symptom/cause separation, specificity test, evidence anchoring); added Contextual Adaptation section covering government/public sector, NZ SME, and regulated financial services; added required time horizon statement to Metrics and Milestones; added structured trade-offs table format (alternative → rejection reason → re-evaluation signal); added Diagnostic Precision Tests section (falsifiability test and constraint test); added Review Triggers section (time-based and event-based); added "Never diagnose a symptom as the core constraint" to Behavioral Constraints

## [1.0.0] - 2026-02-20

### Changed

- Documentation rewritten to be vendor-agnostic; no longer assumes Claude Code
- README primary usage is now: paste SKILL.md content into any AI assistant's context
- Native tool install section now lists multiple vendors (Claude Code, OpenAI Codex CLI) side by side
- PRD, PROGRESS, and ADR updated to reflect open-standard framing

### Added

- Canonical `skills/` directory structure following the Agent Skills open standard
- `skills/research/SKILL.md` — evidence-driven recursive research skill
- `skills/strategy-author/SKILL.md` — Rumelt/Porter high-rigour strategy skill
- `skills/remove-ai-slop/SKILL.md` — AI signal suppression and humanization skill
- `skills/strategic-persuasion/SKILL.md` — cognitive rhetoric and persuasion skill
- `README.md` with skills index, generic usage instructions, native tool install table, and repo structure
- `PRD.md` with project requirements, goals, and success criteria
- `PROGRESS.md` append-only build journal
- `decisions/0001-adopt-skill-md-standard.md` architecture decision record

### Removed

- Flat `research-skill.md` (converted to `skills/research/SKILL.md`)
- Flat `strategy-author-skill.md` (converted to `skills/strategy-author/SKILL.md`)
- Flat `remove-ai-slop.md` (converted to `skills/remove-ai-slop/SKILL.md`)
- Flat `strategic-persuasion-skill.md` (converted to `skills/strategic-persuasion/SKILL.md`)

[Unreleased]: https://github.com/davidamitchell/Skills/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/davidamitchell/Skills/releases/tag/v1.0.0
