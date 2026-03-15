---
name: peer-reviewer
version: "1.0"
description: Checks a completed research item for logical coherence, alternative explanations, and cross-item integration. Use after research investigation is complete and before the item is marked done. Audit-only — never edits the item.
---

# Skill: Peer Review

## When Not to Use

- When the research item is still in progress — complete the investigation first
- When a quick citation or writing check is needed — use `citation-discipline`, `speculation-control`, or `remove-ai-slop` individually
- When the goal is to improve the prose — this skill audits logical structure and evidential support; it does not rewrite

---

## Interaction Protocol

**Operating mode**: Audit-only. Read the item. Report violations. Do not edit, rewrite, or commit anything.

**Before starting**, confirm:
1. Is the item complete? (Findings, Evidence Map, and Executive Summary are populated — not stubs or "TBD")
2. Is the Executive Summary a standalone readable conclusion, or a stub pointing elsewhere?

**Output**: A structured violation report. See Output Format.

---

## Inputs and Outputs

**Input**: A completed research item in structured Markdown format with Research Skill Output and Findings sections  
**Output**: A structured audit report with per-check PASS/FAIL verdicts and specific violations  
**Composability**: Use alongside `research-reviewer`; together they form a complete post-investigation quality gate. Apply after `research` §8 Output Finalisation.

---

## Check 1 — Logical Coherence

Verify that every conclusion stated in the Executive Summary is traceable to evidence in the Findings or Evidence Map.

Flag if any of the following are present:

- A conclusion in the Executive Summary that has no corresponding supporting evidence in the Findings or Evidence Map
- A conclusion that contradicts or overstates what the cited evidence actually shows
- A confidence level (e.g., "high confidence", "likely", "strongly suggests") that is not calibrated to the volume and quality of evidence — e.g., asserting high confidence from a single secondary source, or expressing low confidence when multiple primary sources converge
- A causal claim in the Executive Summary that is not labelled as inference and not supported by a causal study or mechanism in the Findings

Do not flag conclusions that are labelled as inference, hypothesis, or speculation when the label is present and appropriate.

---

## Check 2 — Alternative Explanations

Verify that at least one major competing hypothesis or alternative interpretation has been considered for the central finding.

Flag if any of the following are present:

- The Executive Summary or Key Findings section presents a single explanation for a contested or multi-causal phenomenon without acknowledging that alternatives exist
- A competing hypothesis that is commonly discussed in the domain is absent from the item with no stated reason for its exclusion
- An alternative explanation is dismissed without reasoning or evidence supporting the dismissal
- Competing explanations are listed but not engaged with — the item neither integrates them nor provides grounds for preferring the stated conclusion

Do not flag items where the question is definitional or taxonomic, or where only one explanation is supported by the available evidence and the item states this explicitly.

---

## Check 3 — Cross-Item Integration

Verify that the item connects to related completed research where that connection is material to the conclusion.

Flag if any of the following are present:

- A conclusion that depends on, contradicts, or extends a finding from a related item, where no cross-reference is present
- Confidence levels or conclusions that would change materially if a related item's findings were taken into account, but that item is not referenced
- Assumptions stated in this item that are investigated and settled in a related item, where the settled finding is not cited

Do not flag the absence of cross-references when no related completed items exist, or when the connection between items is peripheral rather than material to the conclusion.

---

## Output Format

Produce the report in this exact format:

```
REVIEW_TARGET: <item identifier or title>
logical-coherence: PASS | FAIL
  VIOLATION: <specific violation with section reference or quote>
alternative-explanations: PASS | FAIL
  VIOLATION: <specific violation with section reference or quote>
cross-item-integration: PASS | FAIL
  VIOLATION: <specific violation with section reference or quote>
OVERALL: PASS | FAIL
```

Rules:
- Use `PASS` if no violations are found for a check; use `FAIL` if any violations are found
- Each violation on its own line, indented two spaces, prefixed `VIOLATION: `
- `OVERALL: PASS` only if all three checks passed; otherwise `OVERALL: FAIL`
- If the item is a stub (Findings not yet populated), write `ITEM_INCOMPLETE` and do not audit
