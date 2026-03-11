# PROGRESS.md

Append-only build journal. Each entry records what was done, what changed, and what was decided. Do not edit past entries — append new ones at the bottom.

---

## 2026-02-20 — Session 1: Initial restructure

**Session goal**: Restructure flat skill files into the Agent Skills open standard format and add project documentation infrastructure.

**Completed**:

- Researched Agent Skills open standard format (SKILL.md, YAML frontmatter, three-level discovery system)
- Researched README best practices for skills projects
- Researched PRD format and append-only progress tracking conventions
- Created `skills/` directory structure with four subdirectories
- Converted `research-skill.md` → `skills/research/SKILL.md` with YAML frontmatter
- Converted `strategy-author-skill.md` → `skills/strategy-author/SKILL.md` with YAML frontmatter
- Converted `remove-ai-slop.md` → `skills/remove-ai-slop/SKILL.md` with YAML frontmatter
- Converted `strategic-persuasion-skill.md` → `skills/strategic-persuasion/SKILL.md` with YAML frontmatter
- Wrote `README.md` covering generic usage (paste into context) and native tool installation
- Created `PRD.md` covering goals, requirements (phased P0/P1), success criteria, and risks
- Created `CHANGELOG.md` following Keep-a-Changelog 1.0.0 format
- Created `PROGRESS.md` (this file)
- Created `decisions/0001-adopt-skill-md-standard.md` ADR
- Removed original flat `.md` skill files
- Removed all vendor-specific assumptions from documentation; repo is now tool-agnostic

**Notes**:

- `remove-ai-slop.md` was incomplete — the original file ended at the section header "# 2. Recursive Slop Removal Algorithm" with no body. The content that existed has been preserved verbatim.

**Next session**:

- Complete the missing algorithm body in `skills/remove-ai-slop/SKILL.md`
- Test skills by pasting SKILL.md content into various AI assistants to verify instructions are clear
- Consider adding `references/` subdirectories for skills that cite external frameworks

---

## 2026-02-20 — Session 2: Vendor-agnostic documentation pass

**Session goal**: Remove all vendor-specific assumptions so the repo is useful with any AI assistant.

**Completed**:

- Audited all documentation for Claude Code-specific language
- Rewrote `README.md`: primary usage is now paste-into-context (generic); native tool install is a secondary section listing Claude Code and OpenAI Codex CLI side by side; removed slash command examples
- Updated `PRD.md`: removed plugin marketplace reference; reframed users and success criteria around vendor-neutral consumption
- Updated `CHANGELOG.md`: replaced vendor-specific framing with open standard language; added Changed entry for this pass
- Updated `PROGRESS.md` (this entry): removed ~/.claude/ install step from next-session tasks
- Updated `decisions/0001-adopt-skill-md-standard.md`: reframed context and consequences around open standard and multi-vendor compatibility

**Blockers**: None.

**Next session**:

- Complete the missing algorithm body in `skills/remove-ai-slop/SKILL.md`
- Test skills by pasting SKILL.md content into at least two different AI assistants

---

## 2026-02-27 — Session 3: SKILL.md audit and consistency improvements

**Session goal**: Address Issue #5 — audit all SKILL.md files for consistency, clarity, operational usability, and responsible AI framing.

**Completed**:

- Audited all seven SKILL.md files against the issue requirements
- Added `version: "1.0"` frontmatter field to all skills (consistency)
- Added `## When Not to Use` section to every skill (operational clarity)
- Added `## Interaction Protocol` section to every skill (clarifying questions + output style)
- Added `## Inputs and Outputs` section to every skill (composable interfaces)
- Fixed `skills/remove-ai-slop/SKILL.md`: replaced non-standard frontmatter (`title`, `author`, `tags`, etc.) with canonical `name` and `description` fields; reframed purpose from AI-detection evasion to writing quality improvement; removed "Threat Model" adversarial framing and "Watermark Risk Reduction" section; completed the missing algorithm body from Session 1
- Reframed `skills/strategic-persuasion/SKILL.md`: replaced manipulative framing ("subconscious triggers", "lowering critical resistance", "intellectual dominance") with ethical persuasion framing; added explicit `## Ethical Use` section with clearly stated limits; renamed category from "Strategic Communications / Behavioral Engineering" to "Strategic Communications"
- Updated `CHANGELOG.md` with detailed entries for all changes
- Updated `PROGRESS.md` (this entry)

**Notes**:

- `remove-ai-slop` previously lacked the standard `name` and `description` frontmatter fields — now aligned with the Agent Skills open standard
- `strategic-persuasion` was the only skill raising responsible-use concerns; the core technique set (audience mapping, framing, lexical precision) is preserved — the manipulative framing and "behavioral engineering" positioning have been removed
- All other skills were structurally sound but lacked operational metadata

**Blockers**: None.

---

## 2026-03-02 — Session 4: Skill gap review and new skill additions

**Session goal**: Address Issue — review existing skills, identify gaps using awesome lists, and add the most valuable missing skills.

**Completed**:

- Reviewed all seven existing SKILL.md files for coverage and gaps
- Researched awesome lists related to skills: ComposioHQ/awesome-claude-skills, travisvn/awesome-claude-skills, anthropics/skills, agentskills.io, skillsmp.com
- Identified two high-value gaps not covered by existing skills: code review and technical writing
- Created `code-review/SKILL.md` — systematic review across correctness, security, performance, maintainability, and style; severity classification (`Critical` to `Info`); structured finding format with location, problem, consequence, and recommendation
- Created `technical-writer/SKILL.md` — audience-first technical documentation; document type templates (README, guide, API reference, runbook, architecture doc); writing standards for clarity, accuracy, completeness, and concision; review protocol for auditing existing docs
- Updated `README.md`: added both new skills to the index table; updated the repo structure tree; added Related Resources section linking to agentskills.io, anthropics/skills, and two awesome-claude-skills community lists
- Updated `CHANGELOG.md`: added entries for this session

**Notes**:

- Both new skills follow the established SKILL.md format: YAML frontmatter with `name`, `version`, and `description`; `When Not to Use`, `Interaction Protocol`, and `Inputs and Outputs` sections
- The `technical-writer` composability chain references `research`, `citation-discipline`, and `remove-ai-slop` — fitting into the existing skill graph
- The `code-review` composability chain references `research` (for domain context) and `strategy-author` (for translating findings into decisions)
- Tooling-specific skills (file formats, browser automation, iOS simulator) were out of scope — they require external dependencies not suited to a portable SKILL.md

**Blockers**: None.

**Next session**:

- Consider a `feedback` skill for structured, constructive critique of written work or decisions
- Consider a `plain-language` skill for simplifying complex content for non-expert audiences
- Test new skills by pasting SKILL.md content into an AI assistant with representative prompts

---

## 2026-03-02 — Session 5: Scan of related resources and new skill additions

**Session goal**: Address Issue — scan related resources and the latest popular skills repos on GitHub to identify what else can be added.

**Completed**:

- Reviewed all nine existing SKILL.md files for coverage gaps
- Scanned related resources: anthropics/skills, ComposioHQ/awesome-claude-skills, travisvn/awesome-claude-skills, agentskills.io; also reviewed BehiSecc/awesome-claude-skills and obra/superpowers (both found in this session's scan)
- Identified two skills deferred from Session 4 that are now clearly warranted: `feedback` and `plain-language`
- Created `feedback/SKILL.md` — structured critique of written work, arguments, decisions, or plans; findings grouped by six categories (Structure, Argument/Logic, Clarity, Accuracy, Completeness, Style); four-level priority classification (`Critical` to `Suggestion`); summary format with strengths and highest-leverage improvement
- Created `plain-language/SKILL.md` — rewrites complex or technical text so non-expert readers can understand it without losing accuracy; audience calibration step; plain language principles (vocabulary substitution, sentence and paragraph restructuring, document structure); accuracy safeguards to prevent meaning loss during simplification
- Updated `README.md`: added both skills to the index table; updated the repository structure tree; added `BehiSecc/awesome-claude-skills` and `obra/superpowers` to Related Resources
- Updated `CHANGELOG.md` with entries for this session
- Updated `PROGRESS.md` (this entry)

**Notes**:

- `feedback` composability chain: use after strategy-author, research, or technical-writer; use before remove-ai-slop
- `plain-language` composability chain: use after technical-writer or research; use alongside remove-ai-slop
- Tooling-specific skills (TDD runners, git automation, browser testing) were reviewed but remain out of scope — they require external tool integration and are not portable SKILL.md prompts
- BehiSecc/awesome-claude-skills and obra/superpowers were found in this scan and added to the Related Resources table

**Blockers**: None.

**Next session**:

- Test new skills by pasting SKILL.md content into an AI assistant with representative prompts
- Consider a `debugging` skill for structured fault isolation and diagnosis (would complement code-review)
- Consider a `decision-record` skill for writing structured architecture decision records

---

## 2026-03-07 — Session 7: Strategy skill gap closure

**Session goal**: Address Issue — implement remaining improvements to strategy-author/SKILL.md per the problem statement.

**Completed**:

- Audited `strategy-author/SKILL.md` against all seven requirements in the problem statement
- Confirmed that six of seven requirements were already implemented in Session 6 (fe28eab): Research-to-Diagnosis Translation, Contextual Adaptation, time horizon requirement, trade-offs table format, Diagnostic Precision Tests, Review Triggers, and symptom/cause behavioural constraint
- Identified one remaining gap: the ranking criteria for when multiple diagnostic candidates exist was missing from the Research-to-Diagnosis Translation section
- Added step 2 to Research-to-Diagnosis Translation: "Rank candidates if multiple exist — if more than one constraint or opportunity is plausible, rank by: (a) centrality to competitive position, (b) tractability within the decision horizon, (c) irreversibility if not addressed. The diagnosis is the highest-ranked item."
- Updated `CHANGELOG.md` to reflect the candidate-ranking addition

**Notes**:

- The ranking criteria (centrality, tractability, irreversibility) were specified verbatim in the problem statement and are now included in the skill

**Blockers**: None.

---

## 2026-03-08 — Session 8: Skill hardening after research document failures (#63–#66)

**Session goal**: Address four research document failures (Issues #63–#66, 2026-03-08). All four documents shared the same five failure patterns. Update the relevant skills to prevent recurrence.

**Completed**:

- Audited `citation-discipline/SKILL.md`, `speculation-control/SKILL.md`, `remove-ai-slop/SKILL.md`, and `research/SKILL.md` against the five observed failure patterns
- `citation-discipline/SKILL.md`: added Mandatory Pre-Output Checklist (six ordered steps: acronym scan, citation URL/DOI check, web-search-synthesis prohibition, primary-source requirement for external claims, scope-match check, epistemic label audit); added Epistemic Label Boundary definition for `[fact]` vs `[inference]`; added two new failure mode entries (scoped/secondary-source citation, name-only citation without URL/DOI)
- `speculation-control/SKILL.md`: added Mandatory Pre-Output Scan (two steps: evaluative/comparative terms scan and causal claims scan); added two new failure mode entries (unlabeled evaluative/comparative judgment, causal claim stated as fact without primary source)
- `remove-ai-slop/SKILL.md`: added Mandatory Pre-Commit Scan section with five specific checks (enumeration-and-convergence, symmetrical contrast, near-verbatim repetition, over-explained causality, repeated sentence-opening pattern); added each pattern as an explicit failure mode entry alongside existing entries
- `research/SKILL.md`: added Section 8 Output Finalisation requiring all three pre-output scans to pass before output is marked complete
- Updated `CHANGELOG.md` under [Unreleased]
- Updated `PROGRESS.md` (this entry)

**Root causes addressed**:

1. Acronym expansion failures → citation-discipline mandatory checklist step 1
2. Wrong/unverifiable citations → citation-discipline checklist steps 2–5
3. Unlabeled evaluative and causal claims → speculation-control mandatory scan
4. AI-slop prose patterns → remove-ai-slop mandatory pre-commit scan
5. Incorrect epistemic labels ([fact] vs [inference]) → citation-discipline epistemic label boundary definition and checklist step 6

**Blockers**: None.

---

## 2026-03-11 — Session 9: New skills and implementation-agnostic constraint

**Session goal**: Address PR #16 review — revert repo-specific CLI commands from `research/SKILL.md`, add `research-question` and `research-reviewer` skills, and prevent implementation-specific content from appearing in skills.

**Completed**:

- Fixed `research/SKILL.md` §0 Initialise: updated prior-work search line to include `reviewing` status alongside `completed`; no CLI commands, repo paths, or lifecycle state tables added — skill remains implementation-agnostic
- Created `research-question/SKILL.md` — standalone pre-flight skill for validating and scoping a research question before investigation begins; five-test quality framework (Specific, Answerable, Scoped, Motivated, Decomposable); question rewriting pattern; approach decomposition rules; READY/NEEDS REVISION readiness verdict format
- Created `research-reviewer/SKILL.md` — audit-only review skill for completed research items; applies `citation-discipline`, `speculation-control`, and `remove-ai-slop` in sequence; structured PASS/FAIL violation report format; scope notes for full vs lighter checking by section
- Updated `README.md`: added both new skills to the index table; added both new directories to the repository structure tree; added implementation-agnostic constraint to the skill quality checklist; replaced Contributing section with explicit prohibition against CLI commands, repo paths, and tool-specific syntax in SKILL.md files
- Updated `CHANGELOG.md`: added entries for all new additions under [Unreleased]

**Root cause addressed**:

PR #16 added `python -m src.main` CLI commands, `Research/in-progress/` file paths, and a lifecycle states table directly into `research/SKILL.md`. Skills are consumed as a git submodule across multiple repositories — embedding one repo's CLI couples the skill to that implementation and breaks silently elsewhere. The Contributing section and skill quality checklist now state this constraint explicitly.

**Blockers**: None.
