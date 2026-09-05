# Manual evaluation: 006-scope-too-broad-personal-finance-basics

Compared `runs/manual/006-scope-too-broad-personal-finance-basics.output.json` with `expected-behavior/scope-too-broad/personal-finance-basics.expected.json`, its referenced fixture, and `schemas/output.schema.json`. Behavior evaluated without requiring exact wording; no web browsing.

1. **Overall result: PASS.** All mandatory assertions pass. One optional behavior is not exercised, and one minor warning-text issue is non-fatal.
2. **Schema result: PASS.** Structural review and a local checker covering every validation keyword present in the schema found conformity with the BLOCKED branch. This used a purpose-built checker, not a standard JSON Schema library.
3. **Status result: PASS.** Actual and expected: `BLOCKED`. Actual reason code `SCOPE_TOO_BROAD` also matches the expected reason code.
4. **MUST results: 5/5 PASS.**

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | SCOPE_001 | PASS | Reason recognizes nine required domains, a 10-slide maximum, and inability to explain them coherently at low density. |
   | SCOPE_002 | PASS | Explicitly cites mat_10 and distinguishes meaningful teaching from a list of definitions. |
   | SCOPE_003 | PASS | Recommendation calls for a focused objective and one prioritized domain for the next run. |
   | SCOPE_004 | PASS | Repair step 1 provides narrower domain options, including budgeting, emergency funds, and debt; step 2 requires one focused understanding for the selected unit. |
   | SCOPE_005 | PASS | resume_when requires narrower objective/directives and one takeaway explainable meaningfully within 10 slides without dense paragraphs. |

5. **MUST_NOT results: 5/5 PASS** (prohibited behavior absent).

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | SCOPE_N001 | PASS | No shallow ten-slide output. Partial findings are explicitly a material map, not a slide plan. |
   | SCOPE_N002 | PASS | No dense carousel copy is generated. Explanatory blocker prose is not carousel copy. |
   | SCOPE_N003 | PASS | Recommends future separate inputs without creating a series or multiple carousels. |
   | SCOPE_N004 | PASS | Leaves narrowing to upstream and does not silently choose one domain. |
   | SCOPE_N005 | PASS | Returns BLOCKED despite technical room to list all domain names. |

6. **SHOULD results: 1 PASS; 1 optional behavior not exercised**, independently assessed.

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | SCOPE_S001 | PASS | Recommendation and repair steps propose domain-based future content units without authoring them now. |
   | SCOPE_S002 | NOT EXERCISED (optional) | partial_findings identifies scope as the blocker but does not affirm that existing material is itself sufficient; missing/repair fields also ask for enough detail for the future objective. The assertion permits this observation rather than requiring it. The fixture's short notes and mat_10 make the qualification reasonable. |

7. **Unexpected problems:** No unsupported financial additions or dangling references identified; partial findings summarize mat_01–09 and scope reasoning uses mat_10 and dir_01. Minor inconsistency: `MOCK_CONTEXT_ONLY` describes a neutral graphic treatment as a test decision despite no visuals being produced. Additional evidence requests are prospective requirements for a narrowed objective, not a replacement reason code.
8. **Recommended engine change:** Make MOCK warning text branch-aware so BLOCKED outputs do not imply completed design decisions. No mandatory scope-handling change is needed.
