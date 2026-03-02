# Skills

A collection of AI skills for research, strategy, writing, and communication.
Each skill is a structured prompt file that instructs any AI assistant how to perform
a specific task to a high standard. Skills are format-compatible with the
[Agent Skills open standard](https://agentskills.io).

## Skills

| Skill | Description |
|---|---|
| [backlog-manager](backlog-manager/SKILL.md) | Command-driven outcome-focused backlog in a single file; add, refine, and track work items by observable result |
| [citation-discipline](citation-discipline/SKILL.md) | Binds every factual claim to a verifiable source at the point of assertion; enforces citation placement, source quality, and precision |
| [code-review](code-review/SKILL.md) | Systematic multi-dimensional code review covering correctness, security, performance, and maintainability; produces prioritised, actionable findings |
| [research](research/SKILL.md) | Rigorous, evidence-driven research using recursive decomposition and verification loops |
| [speculation-control](speculation-control/SKILL.md) | Enforces strict separation between evidence-based statements and speculative, interpretive, or subjective content |
| [strategy-author](strategy-author/SKILL.md) | High-rigour strategy documents grounded in Rumelt and Porter frameworks |
| [remove-ai-slop](remove-ai-slop/SKILL.md) | Eliminates AI detection signals from text — statistical, structural, and alignment artifacts |
| [strategic-persuasion](strategic-persuasion/SKILL.md) | Cognitive rhetoric and audience-targeted persuasive content construction |
| [technical-writer](technical-writer/SKILL.md) | Clear, accurate technical documentation for developers, operators, or end users; covers READMEs, API references, guides, runbooks, and architecture docs |
| [swe](swe/SKILL.md) | Software engineering grounded in SOLID principles, Fielding's REST constraints, Gang of Four design patterns, and Enterprise Integration Patterns; emphasises planning, design, and iterative improvement |

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
├── backlog-manager/
│   └── SKILL.md
├── citation-discipline/
│   └── SKILL.md
├── code-review/
│   └── SKILL.md
├── remove-ai-slop/
│   └── SKILL.md
├── research/
│   └── SKILL.md
├── speculation-control/
│   └── SKILL.md
├── strategic-persuasion/
│   └── SKILL.md
├── strategy-author/
│   └── SKILL.md
├── technical-writer/
│   └── SKILL.md
└── swe/
    └── SKILL.md
```

## Creating a new skill

1. Create a directory: `mkdir my-skill`
2. Create `SKILL.md` with YAML frontmatter and a markdown body:

```yaml
---
name: my-skill
description: What this skill does and when to use it. Tools that support
  automatic skill selection use this field to decide when to load the skill.
---

# Skill instructions here...
```

3. Test by pasting the content into any AI assistant with a relevant prompt.

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

## Contributing

Add new skills to the root of the repo, following the SKILL.md format. Update this README's
index table and add a CHANGELOG entry.
