# Skills

A collection of AI skills for research, strategy, writing, and communication.
Each skill is a structured prompt file that instructs any AI assistant how to perform
a specific task to a high standard. Skills are format-compatible with the
[Agent Skills open standard](https://agentskills.io).

## Skills

| Skill | Description |
|---|---|
| [adr](adr/SKILL.md) | Creates and maintains Architecture Decision Records; captures context, decision, consequences, and alternatives for significant architectural choices |
| [backlog-manager](backlog-manager/SKILL.md) | Command-driven outcome-focused backlog in a single file; add, refine, and track work items by observable result |
| [citation-discipline](citation-discipline/SKILL.md) | Binds every factual claim to a verifiable source at the point of assertion; enforces citation placement, source quality, and precision |
| [code-review](code-review/SKILL.md) | Systematic multi-dimensional code review covering correctness, security, performance, and maintainability; produces prioritised, actionable findings |
| [feedback](feedback/SKILL.md) | Structured, evidence-grounded critique of written work, arguments, decisions, or plans; findings are specific, prioritised, and paired with concrete recommendations |
| [inline-citation](inline-citation/SKILL.md) | Formats hyperlinked inline citations as Author (Year) anchors placed immediately after the claim they support; covers placement, author naming, year, multiple citations, link requirements, and anti-patterns for web-published content |
| [peer-reviewer](peer-reviewer/SKILL.md) | Checks a completed research item for logical coherence, alternative explanations, and cross-item integration; audit-only, never edits |
| [plain-language](plain-language/SKILL.md) | Rewrites complex or technical text so a non-expert reader can understand it without losing accuracy or completeness |
| [research](research/SKILL.md) | Rigorous, evidence-driven research using recursive decomposition and verification loops |
| [research-question](research-question/SKILL.md) | Validates and scopes a research question before investigation begins; checks specificity, answerability, scope, motivation, and decomposability |
| [research-reviewer](research-reviewer/SKILL.md) | Audits a completed research item for citation discipline, speculation control, writing quality, and logical coherence; audit-only, never edits |
| [speculation-control](speculation-control/SKILL.md) | Enforces strict separation between evidence-based statements and speculative, interpretive, or subjective content |
| [strategy-author](strategy-author/SKILL.md) | High-rigour strategy documents grounded in Rumelt and Porter frameworks |
| [remove-ai-slop](remove-ai-slop/SKILL.md) | Eliminates AI detection signals from text — statistical, structural, and alignment artifacts |
| [strategic-persuasion](strategic-persuasion/SKILL.md) | Cognitive rhetoric and audience-targeted persuasive content construction |
| [technical-writer](technical-writer/SKILL.md) | Clear, accurate technical documentation for developers, operators, or end users; covers READMEs, API references, guides, runbooks, and architecture docs |
| [skill-author](skill-author/SKILL.md) | Authors a new SKILL.md file; scans existing skills for duplication and interoperability before drafting, then audits related skills for cross-references after drafting |
| [swe](swe/SKILL.md) | Software engineering grounded in SOLID principles, Fielding's REST constraints, Gang of Four design patterns, and Enterprise Integration Patterns; emphasises planning, design, and iterative improvement |
| [tdd](tdd/SKILL.md) | Test-driven development using Red-Green-Refactor; enforces test-first discipline, testing pyramid balance, and systematic test design principles for any feature, fix, or behaviour change |

## Using a skill

Each skill is a plain markdown file. There are two ways to use them.

### Any AI assistant (generic)

Copy the contents of a `SKILL.md` into your conversation as a system prompt or
prepend it to your message:

```
[paste contents of research/SKILL.md]

Now research: What are the second-order effects of LLM proliferation on knowledge work?
```

Or reference it via file attachment, context window upload, or however your tool
accepts external context.

### Tools with native SKILL.md support

Some AI coding tools discover and load skills automatically. Copy the skill
directory into your tool's configured skills location:

| Tool | Install path |
|---|---|
| Claude Code | `~/.claude/skills/<name>/` or `.claude/skills/<name>/` |
| OpenAI Codex CLI | `~/.codex/skills/<name>/` or `.codex/skills/<name>/` |

Example:
```bash
cp -r research ~/.claude/skills/research
```

Once installed, invoke by name or let the tool trigger the skill automatically
based on the `description` field in the frontmatter.

## Repository structure

```
Skills/
├── README.md                          # This file
├── PRD.md                             # Project requirements and goals
├── CHANGELOG.md                       # What changed and when
├── PROGRESS.md                        # Session-by-session build journal
├── decisions/                         # Architecture Decision Records
│   └── 0001-adopt-skill-md-standard.md
├── adr/
│   └── SKILL.md
├── backlog-manager/
│   └── SKILL.md
├── citation-discipline/
│   └── SKILL.md
├── code-review/
│   └── SKILL.md
├── feedback/
│   └── SKILL.md
├── inline-citation/
│   └── SKILL.md
├── peer-reviewer/
│   └── SKILL.md
├── plain-language/
│   └── SKILL.md
├── remove-ai-slop/
│   └── SKILL.md
├── research/
│   └── SKILL.md
├── research-question/
│   └── SKILL.md
├── research-reviewer/
│   └── SKILL.md
├── speculation-control/
│   └── SKILL.md
├── strategic-persuasion/
│   └── SKILL.md
├── strategy-author/
│   └── SKILL.md
├── technical-writer/
│   └── SKILL.md
├── skill-author/
│   └── SKILL.md
├── swe/
│   └── SKILL.md
└── tdd/
    └── SKILL.md
```

## Creating a new skill

Use the [`skill-author`](skill-author/SKILL.md) skill to guide the full authoring process — it covers the pre-draft related-skill scan, the required file structure, the quality checklist, and the post-draft audit of related skills for cross-references.

For a quick reference, the steps are:

1. Scan existing skills for overlap, duplication, and composition opportunities (see `skill-author` Step 1).
2. Create a directory: `mkdir my-skill`
3. Create `SKILL.md` with YAML frontmatter and a markdown body:

```yaml
---
name: my-skill
description: What this skill does and when to use it. Tools that support
  automatic skill selection use this field to decide when to load the skill.
---

# Skill instructions here...
```

4. Run the quality checklist in `skill-author` Step 3 before committing.
5. Audit related skills for required cross-references after the new skill passes (see `skill-author` Step 4).
6. Test by pasting the content into any AI assistant with a relevant prompt.

See the [Agent Skills open standard](https://agentskills.io) for the full specification.

### Skill quality checklist

Use this to evaluate a skill before adding it or after making changes.

**Frontmatter**
- [ ] `name` matches the directory name
- [ ] `version` is present
- [ ] `description` is a single, precise sentence naming the task and when to trigger the skill — vague descriptions cause spurious auto-invocation in tools that support automatic skill selection

**Sections** (all must be present)
- [ ] `## When Not to Use` — excludes clearly inappropriate contexts; at least two concrete exclusions
- [ ] `## Interaction Protocol` — lists clarifying questions and specifies output style
- [ ] `## Inputs and Outputs` — states input type, output type, and composability with other skills in this repo

**Instruction quality**
- [ ] Instructions are written as imperatives, not suggestions ("List all items" not "You should list all items")
- [ ] No vague verbs: "handle", "manage", "deal with", "consider" each replaced with a precise action
- [ ] Failure modes or stopping conditions are defined
- [ ] No AI slop patterns: no formulaic transitions ("Furthermore", "In conclusion"), no symmetrical filler paragraphs, no safety-prefacing language
- [ ] No implementation-specific references: no CLI commands, repo paths, file paths, or tool-specific syntax — skills must work with any agent and any repo

**Verification**
- [ ] Paste into an AI assistant with a realistic prompt and confirm the output matches the skill's stated intent

## Related resources

Broader collections of skills and prompts that may contain further inspiration:

| Resource | Description |
|---|---|
| [agentskills.io](https://agentskills.io) | The Agent Skills open standard this repo follows |
| [anthropics/skills](https://github.com/anthropics/skills) | Official skills from Anthropic: document processing, design, development, and communication |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | Curated list of community-built skills with categories for dev tools, data analysis, business, and more |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | Curated index of official and community skills with installation instructions |
| [BehiSecc/awesome-claude-skills](https://github.com/BehiSecc/awesome-claude-skills) | Large community skill list searchable by domain; dev tools, automation, data, security, and project management |
| [obra/superpowers](https://github.com/obra/superpowers) | Battle-tested skills library for Claude Code including TDD, debugging, brainstorm, and collaboration patterns |

## Contributing

Add new skills to the root of the repo as a named directory containing `SKILL.md`. Follow the format in "Creating a new skill" above. Update this README's index table and repository structure tree. Add a CHANGELOG entry.

**Skills must be implementation-agnostic.** Do not reference specific CLI commands, file paths, repo names, or tool-specific syntax in a SKILL.md. This repo is consumed as a git submodule by other repositories. A skill that references one repo's CLI will break silently when used in any other context. If you find yourself writing a path like `Research/in-progress/` or a command like `python -m src.main` in a SKILL.md, stop — that content belongs in the consuming repo's prompt files, not in the skill.
