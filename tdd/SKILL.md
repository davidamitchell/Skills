---
name: tdd
version: "1.0"
description: Guides implementation of any feature or fix using test-driven development;
  use when writing new production code, fixing bugs, or changing existing behaviour.
---

# Skill: Test-Driven Development

## When Not to Use

- When the work is a throwaway spike or prototype that will be deleted before merging — confirm with your partner before treating any code as throwaway
- When writing configuration, migrations, or generated code that has no testable logic of its own — generated code that contains conditional logic is not exempt
- When the existing codebase has no test infrastructure at all and establishing it is out of scope — in that case, stop and flag the gap rather than silently skipping tests

---

## Interaction Protocol

**Before starting**, ask if not already clear:

1. What is the expected behaviour — what should the code do, and under what conditions?
2. What test infrastructure exists (unit, integration, system/end-to-end)?
3. Are there existing conventions for test location, naming, or isolation tooling?

**Output style**:

- Name each test to describe the behaviour, not the method: `rejects empty email` not `test_submitForm`
- Produce tests before production code in every response
- When reporting progress, state which phase of the cycle you are in (Red / Green / Refactor) and what the next step is
- Flag any test that is hard to write — difficulty is a design signal, not a reason to skip

---

## Inputs and Outputs

**Input**: A feature requirement, bug report, or behaviour change, with optional context about the existing codebase and test infrastructure  
**Output**: A test written to the failing state, then minimal production code to pass it, then a refactored result — each step verified before proceeding  
**Composability**: Use alongside code-review (to audit implementation quality after the cycle completes); use swe for structural design decisions that arise during refactoring; use technical-writer to document the behaviour under test

---

## The Iron Law

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

Write production code before the test? Delete it. Start over.

**No exceptions**:

- Do not keep it as "reference"
- Do not "adapt" it while writing tests
- Do not look at it
- Delete means delete

---

## Red-Green-Refactor

The cycle has five mandatory steps. Skipping any step invalidates the cycle.

### Step 1 — RED: Write a Failing Test

Write one test that specifies the next unit of required behaviour.

Requirements for the test:

- Tests exactly one behaviour
- Name describes the behaviour, not the mechanism
- Uses real code, not mocks, unless the dependency is external and cannot be controlled
- Contains a clear oracle: an explicit expected result that can be verified without reading the implementation

If you cannot state the expected result before writing the test, the oracle is missing. Resolve the ambiguity first.

**Good**:

```
"retries a failed operation exactly three times before propagating the error"
```

**Bad**:

```
"retry works" — vague; "tests the retry mock" — tests mock behaviour, not code behaviour
```

### Step 2 — VERIFY RED: Confirm the Test Fails Correctly

Run only the new test before writing any production code.

Confirm all three:

1. The test fails (does not error, does not skip)
2. The failure message matches the missing behaviour, not a typo or import error
3. The test fails because the feature is absent, not because of a defect in the test itself

**Test passes immediately?** You are testing existing behaviour or the test is wrong. Fix or discard the test. Do not proceed.

**Test errors?** Fix the error until the test reaches a genuine failure. A test that errors is not a failing test.

Never proceed to Step 3 without completing Step 2.

### Step 3 — GREEN: Write the Minimal Implementation

Write the simplest code that makes the failing test pass.

Rules:

- Pass the test, nothing more
- Do not add features the current test does not require (YAGNI)
- Do not refactor other code in this step
- Do not "improve" names, extract helpers, or consolidate duplication — that belongs in Step 5

### Step 4 — VERIFY GREEN: Confirm All Tests Pass

Run the full test suite.

Confirm both:

1. The new test passes
2. All previously passing tests still pass

**New test fails?** Fix the production code. Do not weaken the test.

**Previously passing test now fails?** Fix the regression before proceeding. Regressions are not acceptable collateral.

### Step 5 — REFACTOR: Clean Up Without Changing Behaviour

With all tests green, improve the code's internal quality.

Permitted in this step:

- Remove duplication
- Improve names for clarity
- Extract helpers or shared logic
- Simplify control flow

Not permitted in this step:

- Adding new behaviour
- Modifying tests to hide a design problem

Run the full suite after each refactoring change. If any test fails, the refactoring introduced a defect — revert and try again.

### Repeat

Return to Step 1. Write the next failing test for the next unit of behaviour.

---

## Testing Pyramid

Structure the test suite as a pyramid: many fast, focused unit tests at the base; fewer integration tests in the middle; a small number of system tests at the top. Invert this ratio and the suite becomes slow, fragile, and hard to diagnose.

### Unit Tests (base — majority)

- Test a single unit of logic in isolation
- Run in milliseconds; the full suite must run in seconds
- Cover the normal path, all boundary conditions, and all error paths
- Do not cross process, network, or filesystem boundaries unless the boundary is the unit under test

When a unit test requires extensive setup or mocking, treat this as a design signal: the unit is over-coupled. Simplify the design before writing the test.

### Integration Tests (middle — selective)

- Test the interaction between two or more units, or between a unit and an external dependency (database, API, message broker)
- Verify that components connect correctly: data flows, contracts are honoured, and errors propagate
- Scope each test to one interaction boundary; do not build full-stack fixtures for an integration concern
- Cover the realistic happy path and the failure modes at the boundary (connection failure, malformed response, timeout)

### System Tests (top — minimal)

- Test the complete system from the outermost entry point against a realistic environment
- Cover the critical paths that must work for the system to be useful — not every feature
- Accept that system tests are slower and more brittle; compensate by keeping their count small and their scope focused
- A failing system test with no failing unit or integration test indicates a missing lower-level test — add it

### Anti-Pattern: Inverted Pyramid

Many E2E tests, few unit tests — the "ice cream cone" shape. Symptoms:

- Suite takes minutes or hours to run
- A single change breaks many tests for unrelated reasons
- Failures are hard to localise

If the test suite has this shape, add unit and integration tests for any code changed, and do not add new system tests until the lower levels provide adequate coverage.

---

## Test Design Principles

These principles, grounded in systematic testing research by Bertrand Meyer (ETH Zürich), guide the selection and construction of test cases.

### Oracles

Every test requires an oracle: a rule for determining whether the output is correct. State the expected result explicitly before running the test. An oracle that depends on reading the implementation is circular and provides no verification.

Sources of strong oracles:

- Formal specifications or contracts (preconditions, postconditions, invariants)
- Reference implementations (compare two independently written versions)
- Symmetry properties (encode then decode should return the original)
- Domain constraints that must always hold (a sorted list must be non-decreasing)

### Partition Testing

Divide the input domain into equivalence classes — sets of inputs expected to trigger the same behaviour. Select at least one test per class. Tests within a class are redundant; tests across classes are not.

Required partitions to cover for any input:

- Typical value
- Boundary value (minimum, maximum, exactly-at-limit, just-outside-limit)
- Empty or zero case
- Invalid or malformed input
- Largest feasible value

### Test Independence

Each test must be executable in isolation and in any order. A test that depends on state left by another test is not a test — it is a script fragment. Use setup and teardown to create fresh state for every test.

### Mutation Sensitivity

A test suite that cannot detect simple mutations in the production code is not providing verification. After writing a test, mentally apply one mutation at a time to the code under test (change a `<` to `<=`, negate a condition, remove a branch) and confirm the test would fail. If a mutation survives all tests, the test suite has a gap — add a test that catches it.

### Non-Redundancy

Two tests that test the same behaviour under the same conditions are redundant. Remove or combine redundant tests; their maintenance cost is real and their verification value is zero.

---

## Test Quality Standards

| Property | Required | Disqualifying |
|---|---|---|
| **Oracle** | Explicit expected result stated before running | "It should work" or assertion-free |
| **Isolation** | No shared mutable state with other tests | Depends on execution order |
| **Focus** | Tests one behaviour | "and" in the test name |
| **Naming** | Describes the behaviour | Describes the method or uses a number |
| **Realism** | Uses real code for the unit under test | Tests mock behaviour instead of real behaviour |
| **Minimality** | Minimal setup to exercise the behaviour | Requires a full system fixture for a unit concern |

---

## Rationalizations to Reject

| Rationalization | Response |
|---|---|
| "Too simple to test" | Simple code breaks. The test takes less than a minute. |
| "I'll write tests after" | Tests written after pass immediately. A passing test that was never red proves nothing. |
| "I already manually tested it" | Manual testing is ad-hoc, unrepeatable, and leaves no record. It is not equivalent to an automated test. |
| "Tests after achieve the same goals" | Tests-after answer "what does this do?" Tests-first answer "what should this do?" They are not the same question. |
| "Deleting X hours of work is wasteful" | Sunk cost. Keeping unverified code incurs ongoing debt. Rewrite with TDD. |
| "Keep it as reference, write tests first" | You will adapt it. That is testing after. Delete means delete. |
| "This is too hard to test" | Hard to test means hard to use. Simplify the design. |
| "TDD slows me down" | Debugging production defects is slower. TDD moves the cost forward. |

---

## Stopping Conditions — Start Over

Stop and restart from Step 1 (Red) if any of the following are true:

- Production code was written before the test
- The test passed immediately without a corresponding code change
- The failing test was never observed before writing code
- A rationalization from the table above was accepted

---

## Verification Checklist

Before marking work complete:

- Every new function or method has at least one test
- Every test was observed to fail before the corresponding code was written
- Every failure was for the expected reason (missing feature, not a defect in the test)
- All tests pass
- The test suite covers: normal path, at least one boundary, at least one error path
- Tests use real code for the unit under test; mocks are used only for external or uncontrollable dependencies
- Each test is independent: it passes in isolation and in any order
- The test pyramid ratio is maintained: the new tests add to the base, not the top

Cannot check all boxes? Return to the first unchecked item and resolve it.
