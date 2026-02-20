# ADR-0001: Adopt the Agent Skills Open Standard Directory Structure

**Date**: 2026-02-20
**Status**: Accepted

## Context

The Skills project started as a flat directory of informal markdown files (`research-skill.md`, `strategy-author-skill.md`, etc.). These files had inconsistent naming, inconsistent or absent YAML frontmatter, and no standard structure.

In December 2025, the Agent Skills format was released as an open standard (agentskills.io). Multiple AI coding tools have adopted it, including Claude Code and OpenAI Codex CLI. The standard specifies:

- Each skill lives in its own named directory
- The entrypoint file is always `SKILL.md`
- YAML frontmatter contains `name` and `description` (required) plus optional fields
- The `description` field is used by supporting tools for automatic skill selection

The format is designed to be vendor-neutral: a `SKILL.md` is a plain markdown file that can be pasted into any AI assistant's context, or discovered automatically by tools that implement the standard.

## Decision

Adopt the Agent Skills open standard structure for all skills in this repository:

```
skills/<skill-name>/SKILL.md
```

Convert all existing flat `.md` files to this structure. Add `name` and `description` YAML frontmatter to each skill. Remove the original flat files after conversion.

Document generic usage (paste into context) as the primary consumption method. List native tool installation as a secondary convenience, with examples for multiple tools — not assuming any single vendor.

## Consequences

**Positive**:
- Skills are usable with any AI assistant by copying SKILL.md content into context
- Compatible with all tools that implement the Agent Skills open standard
- Repository is self-documenting: directory names are skill names
- Structure is stable and human-readable independent of any vendor's tooling

**Negative**:
- The `remove-ai-slop.md` file was incomplete; converting it preserves the incompleteness
- Adds one level of nesting (`skills/<name>/`) compared to flat files

**Neutral**:
- YAML frontmatter fields beyond `name` and `description` are skill-specific and optional
- Tools that do not support native SKILL.md discovery still work — paste the content manually
