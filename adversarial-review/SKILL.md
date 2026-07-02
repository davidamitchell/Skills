---
name: adversarial-review
version: "1.0"
description: Runs a structured adversarial critique process using opposing reviewer roles
  and synthesis to expose hidden risks, weak reasoning, and blind spots in code,
  plans, documents, strategies, or agent outputs.
---

# Skill: Adversarial Review

## When Not to Use

- Use `feedback` when the goal is developmental critique without deliberate opposition pressure
- Use `code-review` when the scope is code quality only and a single reviewer perspective is sufficient
- Use `citation-discipline` and `speculation-control` when the primary risk is unsupported claims rather than reasoning robustness under challenge

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. What artifact is under review: code, plan, document, strategy, or agent output?
2. What failure cost matters most: security, safety, correctness, feasibility, reputational risk, or decision quality?
3. Should the review optimize for fault-finding depth, decision speed, or a balance of both?
4. What constraints cannot be violated during recommendation synthesis?

**Output style**:

- Present opposing perspectives explicitly rather than blending disagreement into one voice
- Tie each critique to observable evidence from the artifact, stated assumptions, or known failure patterns
- Distinguish contested points from converged findings
- End with a synthesis verdict that states confidence, residual risk, and highest-leverage revisions

---

## Inputs and Outputs

**Input**: Any review target (code, plan, document, strategy, or agent output), with optional context on stakes, constraints, and risk priorities  
**Output**: A multi-perspective adversarial assessment with explicit disagreements, rebuttals, synthesis verdict, and prioritized risk-reduction recommendations  
**Composability**: Use after `code-review` or `feedback` to stress-test initial findings; use before `strategy-author` or `technical-writer` to harden final outputs; combine with `research-reviewer` when evidence quality is central

---

## Overview

Adversarial review uses structured opposition to improve reliability. Instead of relying on one reviewer's internal self-check, it separates roles so one perspective advances a proposal while one or more independent perspectives actively challenge it. Research on multi-agent debate patterns, including debate-style frameworks such as D3 and adversarial review panel designs, shows that explicit disagreement can improve factuality, expose reasoning gaps, and reduce error cascades that appear when models mirror their own assumptions.

In practice, teams use adversarial review to break self-review monocultures. The method raises issues standard reviews often miss: latent security exposures, brittle assumptions, edge-case failures, optimistic planning bias, and architectural fragility hidden by surface-level correctness.

## Core Principles

### Productive Opposition

Create real argumentative tension. Require one role to attack assumptions, threat models, and boundary cases while another defends intent and constraints. Treat disagreement as signal generation, not interpersonal conflict.

### Role Specialization

Assign distinct critical lenses instead of generic "reviewer" roles. Separate perspectives such as security, correctness, operations, user harm, economics, or governance. Increase coverage by preventing one lens from dominating the review.

### Iterative Rebuttal

Run at least one rebuttal loop where critiques are answered and then re-challenged. Improve result quality through pressure-tested claims rather than first-pass objections.

### Diversity of Reasoning

Mix reviewer priors, heuristics, and framing styles. Reduce shared blind spots by avoiding single-model or single-prompt convergence.

### Judge-Level Synthesis

Introduce an integrating role that resolves disagreements, records uncertainty, and produces a decision-ready verdict. Preserve minority concerns when unresolved risk remains material.

## Key Mechanisms

Adversarial review commonly starts with independent pass generation. Each reviewer inspects the same artifact from a different attack angle before seeing others' conclusions. This preserves first-order signal and avoids groupthink.

Debate loops then compare claims, counterclaims, and rebuttals. Some implementations use fixed rounds; others stop when new evidence falls below a usefulness threshold. Both approaches can work when evidence traceability remains explicit.

Pre-mortem framing is a frequent accelerator: ask each reviewer to explain how the artifact fails in production, in governance, or under adversarial use. This shifts attention from "is this acceptable?" to "how does this break?"

Verdict synthesis typically classifies outcomes into converged defects, contested risks, and accepted trade-offs. Strong syntheses do not erase disagreement; they convert disagreement into actionable decisions with confidence and residual-risk labels.

## When to Use It

Use adversarial review when error cost is asymmetric and downstream correction is expensive: security-sensitive code, architecture commitments, policy documents, launch strategies, and autonomous agent outputs that will trigger real actions.

Use it selectively for low-stakes work where review latency matters more than maximal rigor. The method adds coordination overhead and can over-index on worst-case reasoning if scope and stopping criteria are unclear.

Pair it with complementary patterns when needed: evidence checks (`research-reviewer`, `citation-discipline`), prose refinement (`technical-writer`), and execution-oriented critique (`code-review`).

## Example Usage / Prompts

### Code Review Prompt

"Review this authentication module using adversarial roles. Have one reviewer defend implementation intent and one reviewer attack it from exploitability, race-condition, and failure-recovery angles. Surface disagreements, run rebuttals, and synthesize a final risk verdict with must-fix items before release."

### Plan Critique Prompt

"Stress-test this migration plan with adversarial review. Use one reviewer focused on delivery feasibility and one focused on operational failure modes. Require both sides to challenge assumptions about rollback, staffing, and blast radius, then produce a synthesis with confidence levels and unresolved risks."

### Document Review Prompt

"Apply adversarial review to this policy memo. Use one reviewer to test factual and logical coherence and one reviewer to challenge stakeholder impact, misuse risk, and ambiguity. Capture contested points and issue a final judgment on whether the memo is decision-ready."

### Agent Output Prompt

"Adversarially review this autonomous agent output before execution. Use separate critics for correctness, safety, and strategic alignment. Force rebuttal on every high-impact claim and return a go/no-go verdict with required revisions."

## Expected Outcomes and Benefits

Expect higher defect discovery in edge conditions, stronger justification quality, clearer uncertainty disclosure, and fewer unchallenged assumptions. Teams typically observe better calibration of confidence because synthesis roles must reconcile disagreement explicitly instead of collapsing to consensus language.

Expect improved resilience against hallucination and echo-chamber effects when reviewers are independent, role-specialized, and required to cite why they disagree. The method does not guarantee correctness, but it consistently improves decision quality by making hidden failure paths visible before commitment.

---

## Failure Modes

- Simulating disagreement without true role separation, producing cosmetic debate and low signal
- Letting one reviewer dominate the synthesis, collapsing model diversity into monoculture conclusions
- Treating rebuttal rounds as rhetorical win conditions instead of evidence-driven refinement
- Omitting uncertainty and residual-risk reporting in the final verdict
- Running adversarial review on low-stakes tasks where overhead exceeds the value of deeper critique
