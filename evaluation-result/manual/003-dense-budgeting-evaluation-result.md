# Manual evaluation: 003-dense-budgeting

Compared `runs/manual/003-dense-budgeting.output.json` with `expected-behavior/dense/budgeting.expected.json`, its referenced fixture, and `schemas/output.schema.json`. Behavior evaluated without requiring exact creative choices; no web browsing.

1. **Overall result: PASS.** All mandatory assertions pass.
2. **Schema result: PASS.** Structural review and a local checker covering every validation keyword present in the schema found conformity with the NEEDS_REVIEW branch. This used a purpose-built checker, not a standard JSON Schema library.
3. **Status result: PASS.** Actual and expected: `NEEDS_REVIEW`.
4. **MUST results: 9/9 PASS.**

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | DENSE_001 | PASS | One takeaway centers on planning money's use; selects 11 of 20 material blocks. |
   | DENSE_002 | PASS | slide_02 distinguishes recording past spending from planning its use, while preserving the usefulness of records. |
   | DENSE_003 | PASS | Nine blocks are substantively omitted in six groups. |
   | DENSE_004 | PASS | Each omitted group has a rationale: scope, redundancy/compression, or distraction from the objective. |
   | DENSE_005 | PASS | Prioritizes definition, planning versus recording, available money, simple categories, and review. |
   | DENSE_006 | PASS | No catalogue of budgeting methods. |
   | DENSE_007 | PASS | Each slide has a distinct core message: definition, distinction, starting funds, categories, or review. |
   | DENSE_008 | PASS | Five slides, below the hard maximum of 10. |
   | DENSE_009 | PASS | Short supporting copy and compact labels; no long paragraphs used to force material onto slides. |

5. **MUST_NOT results: 4/4 PASS** (prohibited behavior absent).

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | DENSE_N001 | PASS | Nine of 20 blocks omitted; example lists reduced to one example per category on slide_04. |
   | DENSE_N002 | PASS | Method/tool detail in mat_14 and mat_18–20 is omitted. |
   | DENSE_N003 | PASS | Concise copy and stacked cards preserve scanability at brief level; final rendered readability is outside this JSON evaluation. |
   | DENSE_N004 | PASS | No invented allocation percentages or monetary formulas. Equal-size category cards explicitly do not imply equal allocation. |

6. **SHOULD results: 3/3 PASS**, independently assessed.

   | Assertion | Result | Evidence |
   | --- | --- | --- |
   | DENSE_S001 | PASS | Five slides meet the preferred 5–7 range. |
   | DENSE_S002 | PASS | mat_15 supports slide_04's beginner framing around broad categories. |
   | DENSE_S003 | PASS | Tools and detailed methods are omitted with editorial reasons. |

7. **Unexpected problems: None identified.** Claims and examples match the selected fixture material and source mappings. Selected and omitted blocks account for all 20 blocks without overlap. No unsupported factual additions or dangling structured ID references; registry IDs are unique and slide sequence/indices agree. Nonconsecutive claim numbers reflect selected material and are not dangling references.
8. **Recommended engine change: None needed for this run.**
