---
name: skill-author
version: "1.0"
description: Authors a new SKILL.md file from scratch; scans the existing skill library
  for related skills before drafting to prevent duplication and ensure interoperability,
  then audits those related skills after drafting to add any required cross-references.
  Use when creating a new skill or auditing an existing one for library fit.
---

# Skill: Skill Authoring

## When Not to Use

- When the task is to edit or extend an existing skill rather than create a new one — edit the file directly and run only the post-draft related-skill review (Step 4)
- When the task is to use a skill, not document one — load the target skill instead
- When a quick prompt template is needed rather than a reusable, composable skill — a skill imposes structural requirements that add overhead not warranted for one-off prompts

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. What is the name and intended purpose of the new skill?
2. Are there existing skills in the library that address the same or an adjacent domain?
3. What other skills should the new skill compose with?

**Output style**:

- Produce a complete `SKILL.md` file with YAML frontmatter and all required sections
- Use imperatives throughout ("List all items", not "You should list all items")
- Replace every vague verb ("handle", "manage", "consider") with a precise action before finalising

---

## Inputs and Outputs

**Input**: A description of the skill's purpose and the skills already in the library  
**Output**: A complete `SKILL.md` file ready to commit, plus a list of related-skill changes required for cross-referencing  
**Composability**: Use `research` before this skill to investigate whether the capability already exists; use `technical-writer` after this skill if the prose needs polish for a non-technical audience; use `feedback` to critique a draft before finalising

---

## Step 1 — Pre-Draft Related-Skill Scan

Before writing a single line of the new skill, scan the existing skill library for skills that overlap with, compose with, or could be confused with the proposed new skill.

For each existing skill, ask:

1. **Duplication check**: Does this existing skill already cover the proposed capability, either fully or substantially? If yes, extend the existing skill rather than creating a new one.
2. **Overlap check**: Does this existing skill cover a subset or adjacent domain that the new skill will touch? Document the boundary — what does each skill do and not do?
3. **Composition check**: Will users naturally want to run this new skill alongside the existing skill? If yes, the new skill's Composability line must reference it, and the existing skill may need a reciprocal reference.
4. **Confusion check**: Could the description of the new skill cause a tool to auto-invoke it when the existing skill was intended? If yes, sharpen the `description` frontmatter field of one or both skills to eliminate the ambiguity.

Record the findings. Resolve duplication and ambiguity before proceeding to Step 2.

---

## Step 2 — Draft the New Skill

Author the `SKILL.md` file using the required structure below. Every section must contain substantive content — no stubs, placeholders, or "TBD" entries.

### Required Frontmatter

```yaml
---
name: <skill-name>
version: "1.0"
description: <single precise sentence: what the skill does and when to trigger it>
---
```

- `name` must match the directory name exactly
- `version` starts at `"1.0"` for new skills
- `description` must be a single sentence naming the task and the trigger condition; vague descriptions cause spurious auto-invocation in tools that support automatic skill selection

### Required Sections

Every skill must contain all five sections in this order:

#### `## When Not to Use`

List at least two concrete exclusion conditions. Each exclusion must name a specific situation — not a generic disclaimer. Direct the reader to an alternative skill where one exists.

#### `## Interaction Protocol`

Specify:
- Clarifying questions to ask before starting (numbered list)
- Output style constraints (bullet list)

#### `## Inputs and Outputs`

Three lines in this format:

```
**Input**: <what the skill consumes>
**Output**: <what the skill produces>
**Composability**: <which skills in this library this skill composes with, and in what direction>
```

The Composability line must name at least one related skill identified in Step 1.

#### Operational sections

One or more sections that define the actual behaviour: rules, algorithms, decision tables, checklists, formats. These vary by skill.

#### `## Failure Modes`

List the specific, observable ways the skill produces wrong output. Each failure mode must be concrete — name the mistake, not the general category of mistake.

---

## Step 3 — Quality Checklist

Run every item before marking the draft complete. Do not proceed to Step 4 until all items pass.

**Frontmatter**
- [ ] `name` matches the directory name
- [ ] `version` is present
- [ ] `description` is a single, precise sentence naming the task and when to trigger the skill

**Sections** (all must be present)
- [ ] `## When Not to Use` — at least two concrete exclusions
- [ ] `## Interaction Protocol` — clarifying questions and output style specified
- [ ] `## Inputs and Outputs` — input type, output type, and Composability line present; Composability names at least one related skill

**Instruction quality**
- [ ] All instructions written as imperatives
- [ ] No vague verbs: "handle", "manage", "deal with", "consider" each replaced with a precise action
- [ ] Failure modes are defined and specific
- [ ] No AI slop patterns: no formulaic transitions, no symmetrical filler paragraphs, no safety-prefacing language
- [ ] No implementation-specific references: no CLI commands, repo paths, file paths, or tool-specific syntax

**Duplication and boundary**
- [ ] No existing skill already covers this capability
- [ ] The boundary between this skill and any adjacent skill is explicitly stated in at least one of the two skills' `## When Not to Use` or `## Inputs and Outputs` sections

---

## Step 4 — Post-Draft Related-Skill Audit

After the new skill passes the quality checklist, return to every related skill identified in Step 1 and audit it for required updates.

For each related skill, check:

1. **Cross-reference**: Does the related skill's Composability line, Interaction Protocol, or a relevant operational section need to mention the new skill? Add the reference if it would help a user discover the correct skill or understand the boundary.
2. **Boundary clarification**: Does the related skill's `## When Not to Use` need to redirect users to the new skill for cases now covered by the new skill?
3. **Description sharpening**: Does the related skill's `description` frontmatter need updating to exclude the new skill's domain and prevent auto-invocation conflicts?

Apply all required changes to related skills as part of the same authoring task. Do not mark the new skill complete while related-skill updates are outstanding.

---

## Failure Modes

- Creating a new skill that duplicates an existing one because the pre-draft scan was skipped or incomplete
- Writing a Composability line that lists skills the new skill does not actually interact with — lists must reflect real composition paths
- Omitting the post-draft audit so related skills are left without cross-references, causing users to miss the correct skill
- Using the `description` frontmatter as a marketing summary rather than a trigger condition — this causes spurious or missed auto-invocation
- Leaving sections with placeholder content ("TBD", "See above") — every section must contain substantive content before the skill is committed
- Referencing implementation-specific details (paths, CLI commands, tool names) that break when the skill is used in a different repository or environment
