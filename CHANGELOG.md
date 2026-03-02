# Changelog

All notable changes to this project will be documented in this file.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added

- `swe/SKILL.md` — software engineering skill grounded in SOLID, Fielding's REST constraints, Gang of Four patterns, and Enterprise Integration Patterns
- `technical-writer/SKILL.md` — technical documentation writing skill covering READMEs, API references, guides, runbooks, and architecture documents
- `backlog-manager/SKILL.md` — command-driven outcome-focused backlog management skill
- `citation-discipline/SKILL.md` — claim–source binding and citation placement discipline skill
- `speculation-control/SKILL.md` — epistemic discipline and non-factual content labeling skill

### Changed

- `README.md`: added `swe` to the skills index table and repository structure tree
- `README.md`: added `code-review` and `technical-writer` to the skills index table
- `README.md`: updated repository structure tree to include the two new skill directories
- `README.md`: added Related Resources section linking to agentskills.io, anthropics/skills, and two awesome-claude-skills lists
- `README.md`: expanded "Creating a new skill" section with a skill quality checklist covering frontmatter, required sections, instruction quality, and verification
- All SKILL.md files: added `version: "1.0"` frontmatter field for consistency
- All SKILL.md files: added `## When Not to Use` section to each skill for operational clarity
- All SKILL.md files: added `## Interaction Protocol` section defining clarifying questions and output style
- All SKILL.md files: added `## Inputs and Outputs` section defining composable interfaces
- `remove-ai-slop/SKILL.md`: replaced non-standard frontmatter with canonical `name` and `description` fields; reframed purpose from AI-detection evasion to writing quality improvement; removed adversarial framing and watermark-circumvention section; set version to `1.0`
- `strategic-persuasion/SKILL.md`: reframed manipulative language to ethical persuasion framing; added `## Ethical Use` section defining boundaries; set version to `1.0`

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
