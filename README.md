# Skills

A collection of AI skills for research, strategy, writing, and communication.
Each skill is a structured prompt file that instructs any AI assistant how to perform
a specific task to a high standard. Skills are format-compatible with the
[Agent Skills open standard](https://agentskills.io).

## Skills

| Skill | Description |
|---|---|
| [backlog-manager](skills/backlog-manager/SKILL.md) | Command-driven outcome-focused backlog in a single file; add, refine, and track work items by observable result |
| [research](skills/research/SKILL.md) | Rigorous, evidence-driven research using recursive decomposition and verification loops |
| [strategy-author](skills/strategy-author/SKILL.md) | High-rigour strategy documents grounded in Rumelt and Porter frameworks |
| [remove-ai-slop](skills/remove-ai-slop/SKILL.md) | Eliminates AI detection signals from text — statistical, structural, and alignment artifacts |
| [strategic-persuasion](skills/strategic-persuasion/SKILL.md) | Cognitive rhetoric and audience-targeted persuasive content construction |

## Using a skill

Each skill is a plain markdown file. There are two ways to use them.

### Any AI assistant (generic)

Copy the contents of a `SKILL.md` into your conversation as a system prompt or
prepend it to your message:

```
[paste contents of skills/research/SKILL.md]

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
cp -r skills/research ~/.claude/skills/research
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
└── skills/                            # Skill directories
    ├── backlog-manager/
    │   └── SKILL.md
    ├── research/
    │   └── SKILL.md
    ├── strategy-author/
    │   └── SKILL.md
    ├── remove-ai-slop/
    │   └── SKILL.md
    └── strategic-persuasion/
        └── SKILL.md
```

## Creating a new skill

1. Create a directory: `mkdir skills/my-skill`
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

## Contributing

Add new skills to `skills/`, following the SKILL.md format. Update this README's
index table and add a CHANGELOG entry.
