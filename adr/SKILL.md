---
name: adr
version: "1.0"
description: Creates and maintains Architecture Decision Records (ADRs) — structured
  documents that capture the context, decision, consequences, and alternatives for
  significant architectural choices. Use when recording a new technical decision,
  updating the status of an existing ADR, or reviewing the ADR log for consistency
  and completeness.
---

# Skill: Architecture Decision Records

## When Not to Use

- When the decision is a minor implementation detail that does not constrain future work or require team alignment — routine choices belong in code comments or inline documentation, not ADRs
- When the decision is already fully captured in an existing ADR — update the existing record rather than creating a duplicate
- When the task is to research or evaluate options rather than record a conclusion — use the research skill first to gather evidence, then return to this skill once a decision is ready to document

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. What is the decision being recorded, and what is its title?
2. What is the current status: Proposed, Accepted, Rejected, Superseded, or Deprecated?
3. What problem or opportunity drove this decision — what forces (technical, business, organisational) were at play?
4. What alternatives were considered, and why was each rejected?
5. Does this ADR supersede or relate to any existing ADR?

**Output style**:

- Produce a complete ADR document in markdown with YAML front matter
- Use precise, unambiguous language throughout — no weasel words, no vague attributions
- State consequences honestly: include both positive and negative impacts in equal rigour
- Use coded bullet identifiers (POS-001, NEG-001, ALT-001, IMP-001, REF-001) for multi-item sections to support machine parsing and cross-referencing
- Do not omit sections or use placeholders — every section must contain substantive content

---

## Inputs and Outputs

**Input**: A decision to document, with context about the forces at play, the chosen solution, and the alternatives considered  
**Output**: A complete ADR markdown file ready to commit to the project's ADR directory, with YAML front matter and all required sections  
**Composability**: Use research before this skill to gather evidence for the context and alternatives sections; use technical-writer after this skill if the ADR requires further prose editing for a broader audience; use swe when the decision involves architectural trade-offs that need grounding in SOLID, REST, or integration pattern principles

---

## ADR Format

Every ADR must follow this structure exactly. Do not reorder, rename, or omit sections.

### Front Matter

```yaml
---
title: "ADR-NNNN: [Decision Title]"
status: "Proposed"
date: "YYYY-MM-DD"
authors: "[Stakeholder Names or Roles]"
tags: ["architecture", "decision"]
supersedes: ""
superseded_by: ""
---
```

- Set `status` to `Proposed` for new ADRs unless the decision is already accepted
- Set `supersedes` to the ADR number being replaced, or leave empty
- Set `superseded_by` when this ADR is later replaced by another; update the original ADR at that time

---

### 1. Status

State the current lifecycle status on a single line:

**Proposed** | Accepted | Rejected | Superseded | Deprecated

---

### 2. Context

State the problem, constraints, and forces that made this decision necessary.

- Describe the situation as it existed before the decision
- Identify the technical, business, and organisational forces at play
- State any hard constraints that ruled out whole classes of solutions
- Do not state the decision here — only the forces that drove it

---

### 3. Decision

State the chosen solution clearly and without ambiguity.

- Open with a direct statement: "We will..." or "Adopt..."
- Explain the key factors that made this option preferable over the alternatives
- Do not repeat the context; assume the reader has read Section 2

---

### 4. Consequences

Document all significant outcomes of the decision.

#### Positive

- **POS-001**: [Beneficial outcome or advantage]
- **POS-002**: [Additional positive consequence]

#### Negative

- **NEG-001**: [Trade-off, limitation, or drawback]
- **NEG-002**: [Technical debt or risk introduced]

Include at least one item in each category. Use specific, concrete statements — "reduces query latency by eliminating a join" is acceptable; "improves performance" is not.

---

### 5. Alternatives Considered

Document every option that was evaluated and rejected.

#### [Alternative Name]

- **ALT-001**: **Description**: [What this option is and how it would work]
- **ALT-002**: **Rejection Reason**: [Why this option was not selected — specific, not generic]

Increment ALT codes sequentially across all alternatives. Document at least two alternatives, including the do-nothing option where applicable.

---

### 6. Implementation Notes

Provide actionable guidance for applying the decision.

- **IMP-001**: [Key implementation step or constraint]
- **IMP-002**: [Migration or rollout consideration, if applicable]
- **IMP-003**: [Success criterion or observable outcome that confirms the decision has been applied correctly]

---

### 7. References

Link to related ADRs, standards, and external resources.

- **REF-001**: [Related ADR — use relative path]
- **REF-002**: [External standard, specification, or framework]
- **REF-003**: [Research findings or evidence that informed the decision]

---

## File Naming and Location

### Naming Convention

`NNNN-[title-slug].md`

Where:
- `NNNN` is a zero-padded four-digit sequence number (0001, 0002, …)
- `[title-slug]` is the decision title in lowercase with spaces replaced by hyphens and special characters removed, kept to three to five words

**Examples**: `0001-database-selection.md`, `0015-microservices-architecture.md`

### Location

Store all ADRs in a dedicated directory within the project. Confirm the project's ADR directory before creating a file; common locations are `docs/adr/`, `decisions/`, or `architecture/decisions/`. If no directory exists, propose creating one and confirm with the team.

### Sequence Number

Check the existing ADR files to determine the next sequential number. Do not assume a number — verify it by inspecting the directory.

---

## Maintaining Existing ADRs

When a decision is superseded or its status changes:

1. Update the `status` field in the original ADR's front matter
2. Set `superseded_by` to the number of the new ADR
3. In the new ADR, set `supersedes` to the number of the original
4. Do not delete or rewrite the original ADR — the historical record must be preserved

When an ADR contains an error in the context or alternatives sections, append a correction note rather than editing the original prose. Preserve the decision as it was understood at the time it was made.

---

## Quality Checklist

Before finalising any ADR, verify all items:

- [ ] ADR number is sequential and does not duplicate an existing number
- [ ] File name follows the naming convention
- [ ] Front matter is complete: title, status, date, authors, tags
- [ ] Date is in YYYY-MM-DD format
- [ ] Status is one of the five valid values
- [ ] Context explains the forces without stating the decision
- [ ] Decision is stated unambiguously in the opening sentence
- [ ] At least one positive and one negative consequence are documented
- [ ] At least two alternatives are documented with specific rejection reasons
- [ ] Implementation notes provide at least one observable success criterion
- [ ] All coded items follow the format (POS-001, NEG-001, ALT-001, IMP-001, REF-001)
- [ ] No section is empty or contains a placeholder
- [ ] Language is precise — no weasel words, no vague attributions, no passive constructions that hide the decision-maker
- [ ] Related ADRs are cross-referenced in both directions

---

## Failure Modes

- Creating an ADR for a decision that has not yet been made — ADRs record decisions, not open questions; use a different format (RFC, proposal, spike) for options under evaluation
- Stating consequences without specificity — "improves maintainability" is not a consequence; name what concretely changes
- Documenting only positive consequences — every real decision involves trade-offs; if no negatives are listed, the record is incomplete
- Listing alternatives that were never seriously considered — every alternative must have a genuine rejection reason
- Editing the substance of a historical ADR rather than superseding it — this destroys the audit trail the format is designed to preserve
