# Changelog

All notable changes to this project will be documented in this file.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

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
