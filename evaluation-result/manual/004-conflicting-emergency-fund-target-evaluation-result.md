# Manual evaluation: 004-conflicting-emergency-fund-target

Compared `runs/manual/004-conflicting-emergency-fund-target.output.json` with `expected-behavior/conflicting/emergency-fund-target.expected.json`, its referenced fixture, and `schemas/output.schema.json`. Behavior evaluated without requiring exact creative choices; no web browsing.

1. **Overall result: PASS.** All mandatory assertions pass.
2. **Schema result: PASS.** Structural review and a local checker covering every validation keyword present in the schema found conformity with the NEEDS_REVIEW branch. This used a purpose-built checker, not a standard JSON Schema library.
3. **Status result: PASS.** Actual and expected: `NEEDS_REVIEW`.
4. **MUST results: 5/5 PASS.**

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | CONFLICT_001 | PASS | Editorial rationale and slide_01 explicitly recognize different guidelines. |
   | CONFLICT_002 | PASS | slide_02 retains A's three-month initial target and B's six-month target, both based on routine expenses; slide_03 preserves C's contextual approach. |
   | CONFLICT_003 | PASS | Central takeaway and slide_05 explicitly limit the conclusion to material that cannot establish a universal target. |
   | CONFLICT_004 | PASS | Produces NEEDS_REVIEW because explaining disagreement answers the objective. |
   | CONFLICT_005 | PASS | claim_01 maps to src_01/mat_01, claim_02 to src_02/mat_02, and claim_03 to src_03/mat_03; visible source attribution is preserved. |

5. **MUST_NOT results: 5/5 PASS** (prohibited behavior absent).

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | CONFLICT_N001 | PASS | Three months remains Guide A's initial target, not universal advice. |
   | CONFLICT_N002 | PASS | Six months remains Guide B's target, not universal advice. |
   | CONFLICT_N003 | PASS | No compromise target, average, or merged recommendation is invented. |
   | CONFLICT_N004 | PASS | Source disagreement does not trigger BLOCKED. |
   | CONFLICT_N005 | PASS | Disagreement remains explicit in comparison and closing; the shared buffer function does not erase target differences. |

6. **SHOULD results: 2/2 PASS**, independently assessed.

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | CONFLICT_S001 | PASS | Separates named guides and explains C's income stability, dependents, and individual circumstances without inventing a formula. |
   | CONFLICT_S002 | PASS | Equal-weight comparison cards present the two numerical guidelines clearly. |

7. **Unexpected problems: None identified.** Factual additions are supported by mat_01–06; no unsupported ranking, factor-to-target relationship, or guarantee appears. All structured ID references resolve; registry IDs are unique and slide sequence/indices agree. MOCK limitations are disclosed.
8. **Recommended engine change: None needed for this run.**
