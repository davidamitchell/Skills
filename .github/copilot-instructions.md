# GitHub Copilot Instructions

This repository is a library of AI skills following the [Agent Skills open standard](https://agentskills.io). Each skill is a structured markdown file (`SKILL.md`) that instructs any AI assistant how to perform a specific task to a high standard.

## Repository conventions

### Structure

Every skill lives in its own directory at the root of the repo:

```
<skill-name>/
└── SKILL.md
```

No other files are required or expected in a skill directory. Do not create helper scripts, example files, or test fixtures inside skill directories.

### SKILL.md format

Every `SKILL.md` must have YAML frontmatter and five required sections:

```yaml
---
name: <skill-name>          # must match the directory name exactly
version: "1.0"              # start at 1.0 for new skills
description: <single precise sentence naming the task and when to trigger it>
---
```

Required sections (in order):

1. `## When Not to Use` — at least two concrete exclusion conditions; direct the reader to an alternative skill where one exists
2. `## Interaction Protocol` — clarifying questions to ask before starting; output style constraints
3. `## Inputs and Outputs` — `**Input**`, `**Output**`, and `**Composability**` lines; Composability must name at least one other skill in this library
4. One or more operational sections defining the actual behaviour
5. `## Failure Modes` — specific, observable failure conditions; name the mistake, not the category

### Writing style

- Write all instructions as imperatives: "List all items", not "You should list all items"
- Replace every vague verb — "handle", "manage", "deal with", "consider" — with a precise action
- No AI slop patterns: no formulaic transitions ("Furthermore", "In conclusion"), no symmetrical filler paragraphs, no safety-prefacing language
- No implementation-specific references: no CLI commands, repo paths, file paths, or tool-specific syntax — skills must work with any agent and any repo

### Skills are implementation-agnostic

This repo is consumed as a git submodule by other repositories. A skill that references one repo's CLI, paths, or tooling will break silently in any other context. If you find yourself writing a path like `Research/in-progress/` or a command like `python -m src.main` in a `SKILL.md`, stop — that content belongs in the consuming repo's prompt files, not in the skill.

## Adding a new skill

Follow the four-step process in [`skill-author/SKILL.md`](../skill-author/SKILL.md):

1. **Pre-draft related-skill scan** — check every existing skill for duplication, overlap, composition opportunities, and `description` ambiguity before drafting begins
2. **Draft** — author the `SKILL.md` using the required structure above
3. **Quality checklist** — run all checklist items in `skill-author` Step 3; do not commit until every item passes
4. **Post-draft related-skill audit** — return to every related skill from Step 1 and apply any required cross-reference updates, boundary clarifications, or `description` sharpening

**When adding a new skill also update:**

- `README.md` — add a row to the skills index table (alphabetical order by skill name) and add the directory to the repository structure tree
- `CHANGELOG.md` — add an entry under `[Unreleased] > Added`
- Any related skills whose Composability line, `## When Not to Use`, or `description` needs updating (identified in Step 4)

## Editing an existing skill

Run the post-draft related-skill audit (Step 4 of `skill-author`) after any substantive change to check whether adjacent skills need boundary or cross-reference updates. Update `CHANGELOG.md` under `[Unreleased] > Changed`.

## What not to do

- Do not create a new skill when extending an existing one is the right call — check for duplication first
- Do not leave any section empty or with placeholder content ("TBD", "See above")
- Do not add dependencies, build tools, linters, or test frameworks — this repo contains only markdown files
- Do not commit files other than `SKILL.md` inside skill directories (no examples, fixtures, or scripts)
