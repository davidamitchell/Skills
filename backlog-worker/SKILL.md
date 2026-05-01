---
name: backlog-worker
version: "1.0"
description: Executes backlog items one at a time — selects the next ready item, decomposes it into atomic actions, performs each action using the appropriate sub-skill, reviews the output, records learnings, and advances the item to done. Use when asked to work the backlog, execute the next item, or make autonomous progress on defined work.
---

# Skill: Backlog Worker

## When Not to Use

- When the task is to add, refine, list, start, complete, or archive backlog items rather than execute the work they describe — use `backlog-manager` instead
- When no items are in `ready` status — apply `backlog-manager` to refine items to `ready` before invoking this skill
- When the item requires a human decision or external approval before work can proceed — stop and surface the decision rather than proceeding autonomously
- When the scope of an item cannot be completed in a single session and partial completion cannot be verified — record progress, leave the item `active`, and stop rather than marking it `done`

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. Which item to work — a specific item ID, or should the skill select the first `ready` item automatically?
2. Are there existing learnings records or prior research relevant to this work?
3. What constitutes done for this item — what observable state must be true before the item can be marked complete?
4. Should the skill stop at the first blocker, or continue to the next atomic action where possible?

**Output style**:

- Announce the selected item and its outcome statement before starting any work
- Report progress at each phase boundary: decomposition complete, each action complete, review complete
- State precisely what was done, what was skipped and why, and what remains
- When a blocker prevents progress, state it in one sentence and stop — do not fabricate forward progress

---

## Inputs and Outputs

**Input**: A backlog with at least one item in `ready` status; optional learnings record and prior research documents  
**Output**: The selected item advanced to `done` status; updated documentation reflecting the work; learnings appended to the project's persistent learnings record; backlog refined based on discoveries made during execution  
**Composability**: Use `backlog-manager` to read and advance item state; use `research` to investigate unknowns before acting; use `swe` and `tdd` for implementation work; use `code-review` to verify completed code; use `technical-writer` to update documentation; use `feedback` to evaluate non-code outputs before marking an item done

---

## 1. Initialise

Before selecting an item, establish full context.

1. Read the backlog in full using `backlog-manager List`.
2. Read any persistent learnings record for this project. If none exists, note the absence and proceed.
3. Read any prior research or completed items relevant to the candidate work.
4. If no items are in `ready` status, stop and report: "No items in ready status. Refine the backlog first using backlog-manager."

---

## 2. Select Item

Choose the item to work:

- If a specific item ID was provided, verify it exists and is in `ready` status. If not, report the mismatch and stop.
- Otherwise, select the first item in `ready` status, in backlog order.

Announce the selected item:

```
Working: W-XXXX — <Outcome statement>
```

Advance the item to `active` using `backlog-manager Start W-XXXX`.

---

## 3. Decompose

Before performing any work, decompose the item's Outcome into a list of atomic actions.

An atomic action satisfies all three conditions:

1. A single agent can complete it without further decomposition
2. Its completion is independently verifiable
3. It maps to exactly one sub-skill: research, implementation, documentation, or review

Write the action list before proceeding. Each entry must state:

1. The action in imperative form
2. The sub-skill to apply
3. The verifiable completion criterion

**Ambiguity gate**: If decomposition reveals that the Outcome is too vague to produce a concrete action list, stop. Record the ambiguity in the item's Notes using `backlog-manager Refine W-XXXX`, revert the item to `needing_refinement`, and stop. Do not attempt to execute a vague item.

---

## 4. Execute Actions

Execute each atomic action in sequence.

For each action:

1. **Apply the designated sub-skill.** For implementation tasks, apply `swe` and `tdd`. For research tasks, apply `research`. For documentation tasks, apply `technical-writer`. For review tasks, apply `code-review` or `feedback`.
2. **Verify the completion criterion.** Confirm the criterion stated in Step 3 is now true. If it cannot be verified, the action is not complete — do not proceed to the next action.
3. **Record progress.** Note what was done and what was discovered. These notes feed directly into the learnings update in Step 6.

**Blocker protocol**: If an action cannot be completed because a dependency is missing, a required decision cannot be made, or the work reveals the item was misspecified, stop immediately. Record the blocker precisely in the item's Notes. Do not attempt the next action. Proceed to Step 6 to record learnings, then stop before marking the item `done`.

---

## 5. Review

After all actions complete, review the full body of work before advancing the item to `done`.

1. Re-read the item's Outcome statement.
2. Verify each observable criterion from the Outcome is now true.
3. If implementation was produced, apply `code-review` to the result.
4. If documentation was produced, verify it accurately reflects the current state of the work.
5. Produce fixes for any findings before proceeding. If a finding cannot be fixed in the current session, add it to the backlog using `backlog-manager Add` before closing out.

---

## 6. Record Learnings

After the work is complete or after a blocker stops the session, append to the project's persistent learnings record:

- What was done and what was produced
- What was discovered that was not previously known
- What went wrong and why
- What the next agent working this area should know before starting

Learnings are append-only. Do not overwrite or remove previous entries.

---

## 7. Advance and Refine

If the review passes and all Outcome criteria are met:

1. Mark the item `done` using `backlog-manager Complete W-XXXX`.
2. Add any new work items discovered during execution using `backlog-manager Add`.
3. Refine any existing backlog items whose context or scope changed as a result of this work.
4. Commit all changes: completed work, updated documentation, learnings record, and backlog state.

If the review reveals unresolved blockers:

1. Leave the item in `active` status.
2. Record the blocker clearly in the item's Notes.
3. Do not mark the item `done`.

---

## 8. Repeat

If the session is continuing and more items are in `ready` status, return to Step 1 and select the next item.

If stopping after one item, report the final state: item completed or blocked, learnings appended, backlog updated.

---

## Failure Modes

- Marking an item `done` before all Outcome criteria are verifiable — verify each criterion explicitly against the Outcome statement before advancing status
- Skipping decomposition and executing a vague item — any item that cannot be decomposed into a concrete action list must be sent back to `needing_refinement`, not executed
- Fabricating progress when blocked — a blocker is a stop condition; record it and stop rather than inventing a workaround
- Overwriting learnings instead of appending — learnings accumulate over time; each session's entries are a new append to the record, not a replacement
- Treating a partially complete item as done because the session is ending — set status to `active`, record progress explicitly, and stop
- Discovering new work during execution but failing to add it to the backlog — all work revealed during execution must be captured in the backlog before the session closes
