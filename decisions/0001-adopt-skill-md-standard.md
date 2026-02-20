# ADR-0001: Adopt Canonical SKILL.md Directory Structure

**Date**: 2026-02-20
**Status**: Accepted

## Context

The Skills project started as a flat directory of informal markdown files (`research-skill.md`, `strategy-author-skill.md`, etc.). These files had inconsistent naming, inconsistent or absent YAML frontmatter, and were not structured in a way that Claude Code's skill discovery mechanism could use them.

Claude Code requires skills to be in the format `<skill-name>/SKILL.md` (under `~/.claude/skills/`, `.claude/skills/`, or a plugin path). The metadata Claude uses for auto-invocation must be in the YAML frontmatter `description` field. Files that don't follow this structure cannot be discovered or invoked as skills.

Anthropic published the Agent Skills open standard in December 2025, and it has been adopted by multiple AI coding tools. The standard specifies:

- Each skill lives in its own named directory
- The entrypoint file is always `SKILL.md`
- YAML frontmatter contains `name` and `description` (required) plus optional fields
- The three-level discovery system (metadata → body → resources) keeps token use efficient

## Decision

Adopt the canonical Claude Code Agent Skills structure for all skills in this repository:

```
skills/<skill-name>/SKILL.md
```

Convert all existing flat `.md` files to this structure. Add proper `name` and `description` YAML frontmatter to each skill. Remove the original flat files after conversion.

## Consequences

**Positive**:
- Skills are directly installable to `~/.claude/skills/` and invocable via slash command
- Claude auto-invokes skills based on the `description` field without explicit user invocation
- Structure is compatible with the Claude Code plugin marketplace for future distribution
- Repository is self-documenting: directory names are skill names

**Negative**:
- Existing symlinks or references to the old flat filenames will break (none existed)
- The `remove-ai-slop.md` file was incomplete; converting it preserves the incompleteness

**Neutral**:
- YAML frontmatter fields beyond `name` and `description` are skill-specific and optional
- The `skills/` subdirectory adds one level of nesting to all skill paths
