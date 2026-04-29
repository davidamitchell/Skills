# Changelog

All notable changes to this project will be documented in this file.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added
- `inline-citation/SKILL.md` — new skill for the APA-inspired inline linked citation format for web content; covers the `<a href="URL">Author (Year)</a>` canonical form, placement rules, author naming, year handling (including `n.d.`), multiple-citation separation, link requirements, optional reference list, edge-case table, anti-patterns, and a mandatory pre-output checklist
- `tdd/SKILL.md` — test-driven development skill enforcing Red-Green-Refactor discipline, testing pyramid balance (unit / integration / system), systematic test design principles from Meyer's testing research (oracles, partition testing, test independence, mutation sensitivity, non-redundancy), and a verification checklist
- `adr/SKILL.md` — skill for creating and maintaining Architecture Decision Records; captures context, decision, consequences, and alternatives in a standardised format with front matter, coded bullet identifiers, quality checklist, and failure modes
- `peer-reviewer/SKILL.md` — audit-only peer review skill for completed research items; checks logical coherence (Executive Summary conclusions supported by evidence), alternative explanations (competing hypotheses addressed or excluded), and cross-item integration (confidence levels calibrated to evidence; cross-references to related items where material)
- `research-question/SKILL.md` — pre-flight skill for validating and scoping a research question before investigation begins
- `research-reviewer/SKILL.md` — audit-only review skill for completed research items; checks citation discipline, speculation control, and writing quality
- `README.md`: added implementation-agnostic constraint to skill quality checklist and contributing section

### Changed

- `citation-discipline/SKILL.md`: updated Interaction Protocol question 1 to point to `inline-citation` for web content requiring hyperlinked `Author (Year)` anchors; updated Composability note to reference `inline-citation` as the format-specific companion for web content
- `research-reviewer/SKILL.md`: added Step 4 — Peer Review, applying `peer-reviewer/SKILL.md` checks
- `research-reviewer/SKILL.md`: updated output format to include per-check sub-results (logical-coherence-and-evidence-sufficiency, alternative-explanations, cross-item-integration) under `peer-reviewer:`
- `research-reviewer/SKILL.md`: confidence calibration criteria now explicit (High/Medium/Low) in Step 4 summary; updated composability note, scope note, `OVERALL` rule, and description to reflect all four skills
- `research/SKILL.md`: added §8.4 Peer-review pre-output check; confidence calibration criteria reference the Confidence Calibration table with explicit High/Medium/Low criteria; Section 8 preamble updated to reference all four pre-output checks
- `README.md`: added `peer-reviewer` to the skills index table and repository structure tree; updated `research-reviewer` description

- `citation-discipline/SKILL.md`: added Mandatory Pre-Output Checklist (acronym scan, citation URL/DOI check, web-search-synthesis prohibition, primary-source requirement, scope-match check, epistemic label audit); added Epistemic Label Boundary definition for `[fact]` vs `[inference]`; added two new failure modes: "Citing a scoped or secondary source for a claim about a different scope" and "Listing a citation by name or description only, without a URL or DOI".
- `speculation-control/SKILL.md`: added Mandatory Pre-Output Scan (evaluative/comparative terms scan and causal claims scan); added two new failure modes: "Evaluative or comparative judgment presented as a conclusion without a label" and "Causal claim stated as established fact without a primary source asserting the causal relationship".
- `remove-ai-slop/SKILL.md`: added Mandatory Pre-Commit Scan with five specific checks (enumeration-and-convergence, symmetrical contrast, near-verbatim repetition, over-explained causality, repeated sentence-opening pattern); added each pattern as an explicit failure mode entry.
- `research/SKILL.md`: added Section 8 Output Finalisation requiring citation-discipline pre-output checklist, speculation-control pre-output scan, and remove-ai-slop pre-commit scan to be run and passed before output is marked complete.
- `strategy-author/SKILL.md`: added Research-to-Diagnosis Translation process (critical constraint extraction, candidate ranking by centrality/tractability/irreversibility, symptom/cause separation, specificity test, evidence anchoring); added Contextual Adaptation section covering government/public sector, NZ SME, and regulated financial services; added required time horizon statement to Metrics and Milestones; added structured trade-offs table format (alternative → rejection reason → re-evaluation signal); added Diagnostic Precision Tests section (falsifiability test and constraint test); added Review Triggers section (time-based and event-based); added "Never diagnose a symptom as the core constraint" to Behavioral Constraints
### Added

- `feedback/SKILL.md` — structured critique of written work, arguments, decisions, or plans; findings grouped by category (Structure, Argument/Logic, Clarity, Accuracy, Completeness, Style) with priority classification and summary format
- `plain-language/SKILL.md` — plain-language rewriting skill; rewrites complex or technical text for non-expert audiences without losing accuracy or completeness; includes audience calibration, vocabulary substitution, sentence/paragraph restructuring, and accuracy safeguards
- `code-review/SKILL.md` — systematic multi-dimensional code review skill covering correctness, security, performance, maintainability, and style
- `swe/SKILL.md` — software engineering skill grounded in SOLID, Fielding's REST constraints, Gang of Four patterns, and Enterprise Integration Patterns
- `technical-writer/SKILL.md` — technical documentation writing skill covering READMEs, API references, guides, runbooks, and architecture documents
- `backlog-manager/SKILL.md` — command-driven outcome-focused backlog management skill
- `citation-discipline/SKILL.md` — claim–source binding and citation placement discipline skill
- `speculation-control/SKILL.md` — epistemic discipline and non-factual content labeling skill

### Changed

- `README.md`: added `feedback` and `plain-language` to the skills index table
- `README.md`: added `swe` to the skills index table and repository structure tree
- `README.md`: added `code-review` and `technical-writer` to the skills index table
- `README.md`: updated repository structure tree to include all new skill directories
- `README.md`: added `BehiSecc/awesome-claude-skills` and `obra/superpowers` to Related Resources following a scan of popular skills repositories
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
