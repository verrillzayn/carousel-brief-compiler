# Manual evaluation: 005-insufficient-paylater-risk

Compared `runs/manual/005-insufficient-paylater-risk.output.json` with `expected-behavior/insufficient/paylater-risk.expected.json`, its referenced fixture, and `schemas/output.schema.json`. Behavior evaluated without requiring exact wording; no web browsing.

1. **Overall result: PASS.** All mandatory assertions pass; one non-fatal warning-text issue.
2. **Schema result: PASS.** Structural review and a local checker covering every validation keyword present in the schema found conformity with the BLOCKED branch. This used a purpose-built checker, not a standard JSON Schema library.
3. **Status result: PASS.** Actual and expected: `BLOCKED`. Actual reason code `OBJECTIVE_UNSUPPORTED` also matches the expected reason code.
4. **MUST results: 4/4 PASS.**

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | INSUFFICIENT_001 | PASS | Reason explicitly identifies absent threefold-risk evidence and cites mat_04. |
   | INSUFFICIENT_002 | PASS | Distinguishes general payment obligations/cashflow in mat_01–03 from the unsupported statistical and causal objective. |
   | INSUFFICIENT_003 | PASS | Repair instructions, read with the stated objective and missing evidence, request support for the paylater claim covering students, financial difficulty, effect magnitude, comparator, statistical measure, and causality. |
   | INSUFFICIENT_004 | PASS | resume_when requires mapped evidence supporting the same objective's numerical, population, outcome, and causal components. |

5. **MUST_NOT results: 4/4 PASS** (prohibited behavior absent).

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | INSUFFICIENT_N001 | PASS | Does not produce NEEDS_REVIEW. |
   | INSUFFICIENT_N002 | PASS | Does not replace the objective with generic paylater education; any changed objective must be explicitly supplied upstream for a new run. |
   | INSUFFICIENT_N003 | PASS | Repeats the threefold claim only to identify missing support, never as an established statistic. |
   | INSUFFICIENT_N004 | PASS | partial_findings contains grounded background observations and material references, not a partial carousel. |

6. **SHOULD results: 1/1 PASS**, independently assessed.

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | INSUFFICIENT_S001 | PASS | partial_findings preserves useful payment/cashflow background while stating that it cannot support the numerical or causal claim. No exact future-reuse wording is required. |

7. **Unexpected problems:** No unsupported financial assertions or dangling references identified; mat_01–04 and the prose reference to dir_01 resolve to the fixture. Minor inconsistency: `MOCK_CONTEXT_ONLY` says a neutral graphic treatment is a test decision even though the run explicitly stops before visuals or production. This is inaccurate process metadata, not a fatal assertion failure.
8. **Recommended engine change:** Make warning messages conditional on the output branch. BLOCKED runs should describe the supplied MOCK context without implying that visual treatment was selected.
