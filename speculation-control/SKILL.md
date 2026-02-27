---
name: speculation-control
version: "1.0"
description: Enforces strict separation between evidence-based statements and
  speculative, interpretive, or subjective content. All non-factual content must
  be explicitly labeled and grounded in known information. Use when producing
  research, analysis, or factual writing that requires clear epistemic discipline.
---

# Speculation, Opinion, and Non-Factual Content Control

## When Not to Use

- When the task is explicitly creative, fictional, or speculative by design (brainstorming, scenario planning, science fiction)
- When all content is clearly framed as opinion or editorial from the outset
- When the genre or format already makes the speculative nature obvious (e.g., a clearly labelled opinion column)

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. Is any speculation or opinion explicitly invited, and if so, in what scope?
2. Are there factual claims that need grounding, or is the task to review existing text?

**Output style**:

- Prefix non-factual content with `Speculation:`, `Hypothesis:`, or `Opinion:` as appropriate
- Flag any gap in evidence explicitly — do not fill gaps silently
- Do not mix labeled and unlabeled content within the same sentence

---

## Inputs and Outputs

**Input**: Text to be written or reviewed, with optional indication of which sections may include speculation  
**Output**: Text with all non-factual content explicitly labeled; list of evidentiary gaps  
**Composability**: Apply alongside citation-discipline and research for full epistemic rigour

---

## Purpose

Prevent unsubstantiated speculation, ensure all non-factual content is explicitly
labeled, and maintain strict separation between evidence-based statements and
interpretive or subjective material.

---

## Core Principles

1. No speculation is allowed unless explicitly requested and clearly labeled.
2. No opinion is allowed unless explicitly requested and clearly labeled.
3. Interpretive statements must be grounded in evidence and framed as interpretations, not facts.
4. Subjective language must not be used to mask uncertainty.

---

## Operational Rules

### Speculation

- Speculation may only occur when the user explicitly requests it.
- All speculative statements must be prefixed: `Speculation:` or `Hypothesis:`.
- Speculation must follow logically from known information — not be invented.

### Opinion

- Opinions may only be expressed when explicitly requested.
- All opinions must be labeled `Opinion:` and kept concise.
- Opinions must not be presented as facts or universally accepted views.

### Interpretation

- Interpretations must specify the evidence they are grounded in.
- When multiple interpretations exist, alternatives must be acknowledged.

### Uncertainty

- When information is incomplete, state the limits of what is known.
- Do not fill gaps with invented detail.
- Use precise uncertainty language: "cannot be determined from available evidence", "no reliable data exists".

### Language

- Avoid subjective intensifiers ("clearly", "obviously", "undeniably") unless the claim is demonstrably true.
- Avoid rhetorical framing that implies certainty without evidence.

### Fabrication and Prediction

- If a request requires fabrication, decline and state the constraint.
- If a request asks for predictions, provide only reasoned scenarios with stated assumptions — not definitive outcomes.

---

## Failure Modes

- Implicit speculation disguised as fact
- Opinions embedded in factual prose
- Filling evidentiary gaps with invented detail
- Overconfident language unsupported by evidence
