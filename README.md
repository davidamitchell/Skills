# Skills

A collection of Claude Code skills for research, strategy, writing, and communication.

## Skills Index

| Skill | Description | Invoke with |
|---|---|---|
| [research](skills/research/SKILL.md) | Rigorous, evidence-driven research using recursive decomposition and verification loops | `/research` |
| [strategy-author](skills/strategy-author/SKILL.md) | High-rigour strategy documents grounded in Rumelt and Porter frameworks | `/strategy-author` |
| [remove-ai-slop](skills/remove-ai-slop/SKILL.md) | Eliminates AI detection signals from text — statistical, structural, and alignment artifacts | `/remove-ai-slop` |
| [strategic-persuasion](skills/strategic-persuasion/SKILL.md) | Cognitive rhetoric and audience-targeted persuasive content construction | `/strategic-persuasion` |

## Installation

### Personal (available across all projects)

```bash
cp -r skills/research ~/.claude/skills/research
cp -r skills/strategy-author ~/.claude/skills/strategy-author
cp -r skills/remove-ai-slop ~/.claude/skills/remove-ai-slop
cp -r skills/strategic-persuasion ~/.claude/skills/strategic-persuasion
```

### Project-level (current project only)

```bash
mkdir -p .claude/skills
cp -r skills/research .claude/skills/research
```

## Usage

Invoke a skill directly by name:

```
/research What are the second-order effects of LLM proliferation on knowledge work?
```

```
/strategy-author Diagnose the strategic position of a mid-market SaaS company losing ground to AI-native competitors.
```

```
/remove-ai-slop [paste text here]
```

Claude will also invoke skills automatically when your request matches the skill's description.

## Repository Structure

```
Skills/
├── README.md                          # This file
├── PRD.md                             # Project requirements and goals
├── CHANGELOG.md                       # What changed and when
├── PROGRESS.md                        # Session-by-session build journal
├── decisions/                         # Architecture Decision Records
│   └── 0001-adopt-skill-md-standard.md
└── skills/                            # Canonical skill directories
    ├── research/
    │   └── SKILL.md
    ├── strategy-author/
    │   └── SKILL.md
    ├── remove-ai-slop/
    │   └── SKILL.md
    └── strategic-persuasion/
        └── SKILL.md
```

## Creating a New Skill

1. Create a directory: `mkdir skills/my-skill`
2. Create `SKILL.md` with YAML frontmatter (`name`, `description`) and a markdown body
3. The `description` field is critical — it determines when Claude auto-invokes the skill
4. Install to `~/.claude/skills/` or `.claude/skills/` and test with `/my-skill <input>`

See [Anthropic's skill documentation](https://code.claude.com/docs/en/skills) for the full specification.

## Contributing

Add new skills to `skills/`, following the SKILL.md format. Update this README's index table and add a CHANGELOG entry.
