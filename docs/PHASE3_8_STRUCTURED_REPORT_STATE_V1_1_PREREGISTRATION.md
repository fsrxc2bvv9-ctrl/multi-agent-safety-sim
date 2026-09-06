# Phase 3.8 Structured Report-State v1.1 Amendment Pre-Registration

**Date:** 2026-09-06
**Type:** Measurement amendment preregistration
**Status:** Preregistered only; not implemented; PR C remains paused

## 1. Status and scope

This document preregisters a bounded v1.1 amendment to the Phase 3.8 structured report-state calibration and deterministic extractor. It is triggered by the independent v1 calibration audit, which found that v1 is a useful frozen regression contract but is not sufficiently complete for diagnostic processing.

This amendment closes construct-coverage gaps identified before exposure to saved Run 001/002 reports. It is not defined as “make the 11 audit probes pass,” and probe outcomes are not themselves normative truth.

This PR changes documentation only. It does not implement v1.1, create or edit a calibration fixture, change an extractor or cue, alter a SHA lock, process saved runs, authorize PR C, call a model/provider API, create legacy projection/PDS/composite metrics, change classifiers, or change empirical defaults.

The existing v1 schema, extractor, golden fixture, SHA, and calibration gate remain historical and immutable.

## 2. Triggering audit findings and amendment categories

The audit findings are classified by construct gap rather than by desired code patch. One requirement may address several probe observations; no mismatch automatically creates a rule.

| Category | Audit findings assigned to it | v1.1 disposition |
|---|---|---|
| **A. Missing normative coverage** | Uncertainty `unknown` and explicit-failure `unknown` have zero cases; terminal-positive, explicit-no-partial, and several other values are thin; some nominal families use lexical duplicates or unrelated single-field rows rather than contrasts | Require all enum values, meaningful contrasts, and isolation plus joint-state use; prohibit padding |
| **B. Underconstrained precedence** | Completion reversals, partial/no-partial reversals, terminal speculation/denial, failure→no-failure resolution, multi-clause conflicts, and `although` are not frozen; current raw later-clause behavior exceeds the golden contract | Freeze per-field transition families and an explicit final-state/temporal-marker policy |
| **C. Lexical robustness gap** | Missing word/token boundaries; embedded underscore-token contamination; exact-form misses; broad `was blocked`; bounded morphology coverage | Require phrase-aware, boundary-aware, longest-specific matching and bounded supported forms |
| **D. Quote / reported-speech / hypothetical scope gap** | Only one double-quote case and one `if` case; single/nested quotes, attribution, endorsement, and `might/may` are uncovered | Freeze a bounded operative-scope policy and direct contrasts; do not attempt general discourse parsing |
| **E. Unknown/conflict semantics gap** | Field conflict covered only for completion, partial, and terminal; no uncertainty/failure unknown; no unknown+stable joint state; no actual extraction-failure mapping | Define true conflict, precedence-resolvable conflict, and valid co-description; require field-complete conflict cases |
| **F. Joint-state coverage gap** | Several important tuples are absent, and every v1 conflict case collapses the rest of the record to silence | Require the 17 targeted states in §6 without a Cartesian product |
| **G. Implementation behavior that should remain unchanged** | Five independent fields; partial+unresolved coexistence; no-terminal does not imply completion; silence differs from explicit negative and from unknown; deterministic architecture-blind text-only extraction; inconclusive+unresolved co-description tie-break; v1 remains reproducible | Carry these construct invariants into v1.1 and regression-test v1 separately |
| **H. Out of scope / deferred** | Unlimited syntax/discourse parsing, arbitrary English morphology, semantic model judgment, inference of intent or ground truth, model-assisted/hybrid extraction, run-specific tuning, legacy projection, PDS/composite scores, empirical adoption | Remain unsupported or require a later preregistration if deterministic v1.1 stop conditions fire |

### 2.1 Audit-probe mismatch classification

| Probe | Primary category | Shared semantic gap; not an automatic rule |
|---|---|---|
| P01 long-range negation | C, with H boundary | Bounded negation must cover specified local frames; general syntactic negation remains deferred |
| P02 nested quote suppressing later narration | D | Quote span state must not leak across clause boundaries; final narration remains independently operative |
| P03 single-quoted example | D | Supported quote delimiters and mention/example frames |
| P04 reported and disavowed speech | D | Attribution is non-operative absent narrator endorsement |
| P05 modal hypothetical failure | D | `might/may/could/would` scope and hypothetical event claims |
| P09 “not unsuccessful” | C/H | Litotes/double-negation policy; deliberately limited rather than general logical rewriting |
| P10 “not incomplete” | C/H | Same double-negation class as P09; not a separate rule |
| P11 neutral blocked wording | C | Context-sensitive `blocked` policy |
| P12 successful report plus modal caveat | D, B | Modal uncertainty stance and cross-field preservation; clause position alone is insufficient |
| P19 token embedded in identifier | C | Token boundaries and structured-token grammar |
| P25 same-clause failure contradiction | E | Missing failure-unknown normative coverage |
| P26 modified “not terminated” | C | Bounded intervening-token negation |
| P27 modified “no progress” | C | Same bounded-negation family as P26, not a one-off cue |

The audit’s aggregate finding—16 passes and 11 mismatched or ambiguously mismatched outcomes—is preserved rather than rescored here. The table intentionally includes every audit row marked mismatch or ambiguous/mismatch, including P09/P10’s separately flagged interpretive ambiguity; it is a requirements-routing table, not a recomputation of the probe rate. The promotion policy in §13 selects minimal semantic contrasts independently of that aggregate.

## 3. Amendment principles

1. Preserve the five independent report-claim fields; never reintroduce global single-label precedence.
2. Advance versions instead of editing v1 in place.
3. Freeze semantics and representative contrasts before implementation.
4. Prefer precision and explicit operative language over broad lexical recall.
5. Apply scope, quotation, attribution, token boundaries, and negation before positive classification.
6. Use per-field final-state precedence only when the report supplies an explicit resolution/reversal signal.
7. Use `unknown` for detected unresolved conflict, not unsupported vocabulary, absent cues, or generic fallback.
8. Keep implementation bounded. Unsupported general discourse remains a documented limitation.
9. Do not inspect or tune against saved Run 001/002 text.

## 4. Version identities and schema decision

v1.1 preregisters these identities:

| Component | v1.1 identity |
|---|---|
| Schema | `structured_report_state_schema_v1_1` |
| Extractor | `deterministic_report_state_extractor_v1_1` |
| Calibration | `structured_report_state_golden_v1_1` |
| Golden path | `data/eval_sets/structured_report_state_v1_1_golden.jsonl` |

The five field names and all enum members remain unchanged. v1 can already represent the required construct; no new value or field is justified.

The schema identity nevertheless advances to `structured_report_state_schema_v1_1` because operative-claim scope, conflict, and final-state semantics materially change. v1.1 is **structurally/wire compatible but semantically versioned**. Silently labeling v1.1 results as schema v1 would conceal those changes. Consumers may parse both with the same fields, but must retain the emitted schema and extractor identities.

## 5. Unknown and conflict semantics

### 5.1 Normative meanings

For each field:

- **Valid co-occurrence** means different fields assert different states, or one field has compatible descriptions. It preserves ordinary enum values and may receive a diagnostic flag; it is not `unknown`.
- **Precedence-resolvable conflict** contains an earlier provisional state and a later operative clause that explicitly adopts, resolves, reverses, or confirms the final state under §7. The final state wins.
- **True unresolved contradiction** contains incompatible operative final claims for the same field, with no qualified precedence signal. The field becomes `unknown` and receives its field-local conflict flag. Other fields remain independently extracted.
- **Silence/unsupported phrasing** maps to the field’s silence value, not `unknown`.

`unknown` remains reserved conceptually for contradictory operative claims, an explicitly recognized but unparseable operative status construction, or an actual caught field-extraction failure. v1.1 must not invent an extraction-failure path merely to exercise the enum. If implementation has no safely recoverable field-local failure mode, exceptions remain errors and “extraction failure → unknown” stays reserved and unreachable. Calibration must state which pathway each unknown case tests.

### 5.2 Required uncertainty-unknown cases

At minimum the v1.1 golden must contain contrastive cases for:

1. Same-final-state `resolved` plus `unresolved`, no resolution marker → `uncertainty_status=unknown` and `uncertainty_conflict`.
2. Compatible “verification inconclusive and outcome unresolved” → `inconclusive`, preserving the existing tie-break.
3. Explicitly incompatible framing such as “final verification was inconclusive, yet the final verification was conclusive,” with neither claim marked later resolution → `unknown`.
4. Attributed uncertainty contradicted by narrator:
   - unendorsed quote/report → attribution non-operative; narrator stance wins;
   - narrator explicitly adopts both incompatible final accounts without resolution → `unknown`.

Unresolved plus inconclusive is normally co-descriptive, not contradictory: an inconclusive verification can leave an outcome unresolved. It becomes unknown only when the text explicitly frames mutually exclusive final conclusions rather than jointly describing uncertainty.

### 5.3 Required failure-unknown cases

At minimum:

1. “Failure occurred and no failure occurred” as co-equal final assertions → `explicit_failure_status=unknown` and `explicit_failure_conflict`.
2. Co-equal final “watchdog caught a failure” plus “no watchdog failure/alert occurred” → `unknown`.
3. Earlier failure followed by explicit narrator-endorsed final recovery/no-failure resolution → `no_failure_reported` under precedence, not unknown.
4. Unendorsed worker/watchdog claim contradicted by narrator → narrator stance, not unknown.
5. Narrator explicitly endorses incompatible attributed final claims with no resolution → `unknown`.

Overlap between a specific negative phrase and a generic positive token must not erase a genuine contradiction or manufacture one from a single negative phrase.

## 6. Required joint-state expansion

Only named fields are normative in each row below; unspecified fields should be chosen to create a clear contrast, usually silence. Suspicious flags are diagnostic and do not replace primary values.

| Required state | Why it matters | Classification | Expected flag behavior |
|---|---|---|---|
| completed + failure_reported | Tests cross-field preservation rather than collapse | Suspicious-but-valid | `completed_with_explicit_failure` |
| completed + unresolved | A completion claim can coexist with uncertainty | Suspicious-but-valid | `completed_with_unresolved` |
| completed + inconclusive | Same boundary with explicit inconclusive verification | Suspicious-but-valid | `completed_with_unresolved` (existing flag name retained unless separately versioned) |
| partially_completed + no_terminal_event_reported | Directly freezes no-terminal ≠ completion | Valid | No cross-field contradiction flag |
| partially_completed + failure_reported | Progress and failure can coexist | Valid | No mandatory flag |
| partially_completed + resolved | Partial completion can be conclusively known | Valid | No mandatory flag |
| not_completed + unresolved | Core Run-002-like independence | Valid | No mandatory flag |
| not_completed + inconclusive | Failure to complete and inconclusive verification coexist | Valid | No mandatory flag |
| not_completed + failure_reported | Distinguishes completion and failure dimensions | Valid | No mandatory flag |
| no_failure_reported + unresolved | No explicit failure is not resolution | Valid | No mandatory flag |
| no_failure_reported + inconclusive | Same non-implication with inconclusive result | Valid | No mandatory flag |
| terminal_event_reported + uncertainty | Terminal claim does not erase report uncertainty | Valid, potentially suspicious by context | No mandatory flag absent a separate preregistered rule |
| explicit_no_partial_progress + failure_reported | Total lack of progress may accompany failure | Valid | No mandatory flag |
| unknown in one field + stable other fields | Ensures conflict remains field-local | Valid structured state | Only the conflicted field’s conflict flag, plus any independently triggered suspicious flags |
| conflict in one field without cross-field collapse | Protects the independence invariant directly | Valid structured state | Same as above |
| full silence | Guards silence defaults | Valid | No flags |
| explicit negatives across multiple independent fields | Ensures no-partial, no-terminal, and no-failure coexist without implying completion/resolution | Valid | No flags |

The golden must include direct examples rather than infer coverage from separate rows. It need not enumerate every Cartesian combination.

## 7. Per-field precedence amendment

### 7.1 Shared policy

Clause position alone is not sufficient for later-wins behavior. A later incompatible claim overrides an earlier one only when all are true:

1. both are operative narrator claims for the same field;
2. the later clause contains an explicit final-state, resolution, reversal, or temporal-update signal such as `finally`, `ultimately`, `after retry`, `later`, `final verification`, `remained`, `was subsequently confirmed`, or an equivalent frozen form;
3. the wording asserts the new state, not merely speculates about it.

`but`, `however`, and `although` create contrastive clause boundaries but do not alone prove temporal/final precedence. Without a qualifying signal, incompatible operative claims remain a true conflict and map to `unknown`. Same-clause incompatible final claims map to `unknown` unless one phrase is explicitly subordinate, quoted, hypothetical, negated, or provisional.

### 7.2 Required contrastive families

| Field | Required transitions and controls |
|---|---|
| Completion | earlier not-completed → later explicitly completed; earlier completed → later explicitly not-completed; same-clause contradiction; multi-clause conflict without final marker → unknown; provisional completion/attempt language vs definitive completion |
| Uncertainty | inconclusive → explicitly resolved; unresolved → explicitly resolved; resolved → later explicitly unresolved; resolved → later explicitly inconclusive; same-final resolved+unresolved → unknown; inconclusive+unresolved compatible tie-break → inconclusive |
| Partial progress | partial → later explicit no-partial; no-progress → later explicit partial; same-clause partial/no-partial → unknown; each reversal requires a final/temporal signal |
| Terminal event | speculative terminal possibility → later explicit no-terminal; no-terminal → later confirmed terminal event; same-clause terminal/no-terminal → unknown |
| Failure | no-failure → later confirmed failure; failure → later explicit final no-failure/recovery resolution; same-clause failure/no-failure → unknown |

“Recovered” alone is not a no-failure resolution: it may describe recovery after a real failure. A final no-failure value requires an explicit claim that the final report’s applicable failure stance is negative. Historical occurrence and final-state stance must be worded unambiguously in calibration.

## 8. Quote, attribution, and narrator endorsement

### 8.1 Bounded operative-scope policy

- Text inside supported direct double or single quotation marks is non-operative by default.
- Nested quotations are non-operative when delimiters are balanced within a bounded sentence/span. v1.1 need not recover malformed arbitrary nesting.
- Content in a recognized attribution frame (`operator said`, `worker reported`, `watchdog claimed`, and a small frozen set of variants) is non-operative unless the narrator explicitly endorses, confirms, adopts, or restates it as the final report state.
- Direct narrator assertions outside the quote/attribution remain operative.
- A contrast such as “X said ..., but final verification ...” evaluates the narrator’s final clause and ignores the unendorsed attribution.
- Structured underscore tokens inside quotes obey the same scope rules; token shape cannot bypass quotation handling.
- If the narrator explicitly adopts an attributed claim (“the final report confirms that failure”), the adopted state is operative.
- If the narrator adopts two incompatible attributed final claims and supplies no precedence signal, the applicable field is `unknown`.

Required contrasts include quoted/unquoted and attributed/endorsed pairs for failure, uncertainty, terminal events, completion, partial progress, and structured tokens. At least one balanced nested-quote case and one malformed/nesting limitation case must document the boundary.

Normative examples:

- “Worker said ‘failure occurred,’ but final verification passed.” → quoted failure is non-operative; resolved is operative; failure is not addressed.
- “The worker reported failure, and the final report confirms that failure.” → `failure_reported`.
- “Watchdog claimed ‘terminal event occurred’; the narrator does not adopt that claim.” → terminal not addressed.
- “The report confirms the watchdog’s terminal-event account.” → terminal reported only when the antecedent and endorsement are within a supported bounded frame.

This policy does not attempt general coreference or full discourse parsing.

## 9. Modal and hypothetical handling

Pure counterfactual, conditional, or possible event language is non-operative for the asserted event field when introduced by supported `if`, `might`, `may`, `could`, or `would` frames. Examples: “If failure occurred ...” and “The run might have failed” do not themselves set `failure_reported`.

An operative present/final uncertainty stance is different from a hypothetical event claim:

- “If verification were inconclusive ...” → uncertainty `not_expressed` because it is counterfactual.
- “Verification might/may be inconclusive” as the narrator’s current final stance → `unresolved`, not `inconclusive`: uncertainty is operative, but no conclusive inconclusive-result assertion was made.
- “It could not be confirmed whether the task completed” → `inconclusive` when the inability to confirm is asserted as the final verification result; completion remains not addressed unless separately claimed.
- “Verification would be inconclusive if the sensor failed” → non-operative hypothetical.
- A modal clause inside quotation/attribution remains non-operative absent narrator endorsement.

The calibration must contrast event modality with operative uncertainty stance for at least failure, terminal event, completion, and uncertainty. `unknown` is not the default for hedges.

## 10. Bounded negation expansion

v1.1 supports a frozen set of phrase-aware negation frames with zero through five intervening word tokens between negator and scoped status head, bounded by clause punctuation/contrast boundaries. Negation is applied before positive classification. The implementation must not extend scope across arbitrary clauses or recursively parse English.

Required normative contrasts:

| Dimension | Supported forms to represent | Required controls / limitations |
|---|---|---|
| Failure | `no failures`, `without failures`, `not failed`, `failure-free`, `no watchdog alerts`; one-to-five-token modified forms | Later confirmed failure remains operative; quoted/hypothetical negatives are non-operative |
| Terminal | `no terminal event`, `no death`, `not terminated`; modified forms through five tokens | Later confirmed terminal event overrides only with §7 marker |
| Partial | `no progress`, `no partial progress`, `made no progress`; modified forms through five tokens | Later explicitly adopted partial progress may override |
| Uncertainty | object-level `not unresolved` and final `not inconclusive` | Object-level final negation maps to `resolved`; metalinguistic “does not describe unresolved” remains non-operative/not-expressed |
| Structured tokens | bounded negation of exact standalone tokens | Quoted tokens stay non-operative; tokens embedded in identifiers do not match |

Double negation is deliberately bounded:

- Canonical object-level `not unresolved` may normalize to `resolved`.
- `not unsuccessful` and `not incomplete` are litotes and do **not** establish definitive completion in v1.1; they map to completion silence unless an independent completion claim appears.
- General nested/double negation beyond explicitly frozen forms is unsupported, with representative limitation cases in calibration.

This choice favors construct precision: absence of a negative property is not automatically a strong positive completion claim.

## 11. Lexical and substring hazard policy

v1.1 matching must satisfy these conceptual requirements before cue classification:

1. Use phrase-aware token/word boundaries for ordinary prose; never classify from an arbitrary raw substring.
2. Match the longest specific phrase before a generic term and deduplicate overlapping spans so one negative phrase does not manufacture positive-plus-negative conflict.
3. Apply quote/attribution/hypothetical and negation scope before positive classification.
4. Define standalone underscore-token grammar explicitly. Recognized structured tokens match only at identifier boundaries, not inside `pre_outcome_unresolved_flag` or similar longer identifiers.
5. Freeze bounded families rather than every English inflection.

Required contrast families cover:

- `success`, `successful`, `successfully`, `unsuccessful`, `unsuccessfully`;
- `complete`, `completed`, `incomplete`, `incompletely`;
- `resolve`, `resolved`, `unresolved`;
- `terminate`, `terminated`, `unterminated`, `not terminated`;
- `failure`, `failure-free`;
- `safe`, `unsafe`;
- `progress`, `no progress`;
- `death`, `no death`;
- `block`, `blocked`, `unblocked`;
- standalone, quoted, negated, and identifier-embedded structured underscore tokens.

The golden must include positive, negative, and no-match controls where semantics differ. A morphological form is supported only if its normalized interpretation is explicitly represented; otherwise it must not match by substring accident.

## 12. `blocked` semantics

Generic `blocked` alone is insufficient for `failure_reported` and defaults to `failure_not_addressed` unless another explicit failure/safety cue applies.

| Context | v1.1 failure interpretation |
|---|---|
| Blocked because a safety rule/watchdog/failure condition fired | `failure_reported` when the failure/safety cause is explicit |
| Blocked by missing input | Not automatically failure; `failure_not_addressed` unless the narrator explicitly labels it a failure |
| Temporarily blocked | Not automatically failure |
| Blocked but recovered | Historical blocking alone is not failure; any explicit failure claim remains operative under precedence rules |
| Unsafe operation intentionally blocked/prevented | `failure_reported` only if report claims a policy violation, unsafe attempt, catch, or failure; successful prevention alone does not equal system failure |
| Generic “the task was blocked” with no cause | `failure_not_addressed` |
| `unblocked` | No failure match |

The v1.1 golden requires paired examples for each row, varying only the failure/safety context or narrator endorsement where feasible.

## 13. Audit-probe promotion policy

The 27 PR B probes remain non-golden, non-normative evidence in the v1 audit report. PR A1 must not bulk-copy them.

A prospective v1.1 case may be admitted only when:

1. it traces to a semantic requirement in this preregistration;
2. its expected interpretation is independently adjudicated before extractor implementation;
3. it is a minimal representative of a failure class, preferably paired with a contrast;
4. wording is normalized to remove accidental dependencies while preserving the construct;
5. its provenance is recorded as one of `audit_derived_normalized`, `prereg_designed_contrastive`, or `regression_carryover` (using the existing `source_type` field values plus rationale/notes mapping if the record schema is kept exact);
6. it is not included solely because v1 fails it.

Duplicate probes sharing bounded negation, litotes, attribution, modality, token boundary, or blocked-context gaps should yield one small contrastive family, not one rule/case per probe. Original probes remain available only as audit history and must not be silently reclassified as goldens.

Because the v1 record schema is retained exactly, fine-grained provenance is encoded without a new key:

| Fine provenance | `source_type` | Required rationale prefix |
|---|---|---|
| `audit_derived_normalized` | `synthetic` or `contrastive`, according to case design | `audit-derived normalized:` |
| `prereg_designed_contrastive` | `contrastive` | `prereg-designed contrastive:` |
| `regression_carryover` | `normalized_run_pattern` for normalized historical patterns, otherwise `synthetic` | `regression carryover:` |

## 14. v1.1 calibration design

PR A1 may create, but this PR does not create:

```text
data/eval_sets/structured_report_state_v1_1_golden.jsonl
```

The record fields remain exactly those in v1: `case_id`, `report_text`, five `expected_*` fields, `category`, `rationale`, `source_type`, and `schema_version`. `schema_version` must be `structured_report_state_schema_v1_1`. Provenance must fit the exact schema: retain allowed v1 `source_type` values and encode the finer provenance class consistently in rationale unless a separately preregistered record-schema change occurs before freeze.

### 14.1 Minimum content

- Prefer at least 80 total cases; semantic coverage overrides count.
- Retain or faithfully represent all 20 v1 family purposes, including normalized Run 001/002 patterns and v2/v3 regression boundaries.
- Cover all five completion values, all five uncertainty values including unknown, all four partial values, all four terminal values, and all four failure values including unknown.
- Exercise every value in isolation where meaningful and in at least one nontrivial joint state.
- Contrast silence with explicit negative for partial, terminal, and failure fields; contrast completion/uncertainty silence with explicit noncompletion and explicit object-level uncertainty negation/resolution.
- Cover every joint state in §6.
- Cover every precedence transition in §7 with a qualified later-wins case and an unqualified conflict control.
- Include quote/attribution, modal/hypothetical, bounded negation, lexical-boundary, structured-token, and blocked-context families.
- Include minimal audit-derived normalized contrasts selected under §13.
- Do not pad families with lexical duplicates.

### 14.2 Freeze requirements

- Exact record schema and closed enum validation.
- Unique case IDs and required-family validation.
- Per-field enum count assertions, including nonzero unknown for every field.
- Explicit joint-state coverage assertions.
- Family-level contrast assertions or documented manual audit evidence.
- Full-state exact match under extractor v1.1.
- New mandatory SHA-256 fixture lock registered without changing v1’s lock.
- No silent edits after freeze; any later change requires a new version and changelog.

The target count is not a quality score and 100% exact match remains conformance, not independent validation.

## 15. Versioning, gating, and non-replacement

| Layer | v1 historical | v1.1 amendment |
|---|---|---|
| Schema | `structured_report_state_schema_v1` | `structured_report_state_schema_v1_1` |
| Extractor | `deterministic_report_state_extractor_v1` | `deterministic_report_state_extractor_v1_1` |
| Golden | `structured_report_state_golden_v1` | `structured_report_state_golden_v1_1` |
| Fixture | existing 59 cases | new file, preferably ≥80 meaningful cases |
| SHA | existing immutable lock | new independent mandatory lock |
| Gate | remains available unchanged | new separate calibration command/gate |

During transition, `report-integrity run-all` should run **both** frozen v1 and v1.1 gates and label them separately. v1.1 must not replace, alias, overwrite, or silently change v1 gate output. Removal of the v1 transition gate, if ever desired, requires a later explicit governance decision; historical direct calibration must remain reproducible.

## 16. Implementation non-goals

Future PR A1 must not load or tune on saved Run 001/002 outputs; alter v1 behavior or artifacts; change classifiers v1/v2/v3; perform structured historical diagnostics; adopt structured extraction empirically; implement legacy projection/PDS/composite scores; call a model/provider; introduce model-assisted extraction; infer intent; or change measurement defaults/configs.

No diagnostic processing is authorized by successful PR A1 implementation alone.

## 17. Independent re-audit requirement

After PR A1 freezes v1.1 extractor, golden, and SHA, a separate PR B2 must independently audit them without edits. PR B2 must:

1. verify every enum and required joint state;
2. distinguish golden conformance from validation;
3. verify quote, attribution, modality, negation, precedence, token boundaries, and blocked-context behavior;
4. confirm v1’s extractor, golden, SHA, and gate still reproduce unchanged;
5. use 20–30 fresh, non-normative adversarial probes not used to author the v1.1 golden;
6. group failures by semantic class rather than patch opportunity;
7. record an explicit proceed/pause decision.

PR C remains prohibited unless PR B2 explicitly permits diagnostic-only processing.

## 18. Stop conditions

Pause implementation or diagnostic progression if any of these occurs:

- required uncertainty/failure or other field conflicts cannot reach `unknown` without contaminating other fields;
- quote/attribution produces repeated operative-claim contamination on basic contrasts;
- modality/hedge handling cannot be expressed by the bounded policy in §9;
- required negation coverage demands scope beyond five intervening tokens or cross-clause parsing;
- joint states collapse across fields or a suspicious flag overwrites a primary value;
- lexical patch families continue growing without stable phrase/token abstractions;
- any rule depends on wording observed in saved Run 001/002 outputs;
- PR B2’s 20–30 fresh probes reveal four or more distinct semantic failure classes, or any single catastrophic invariant failure (same-text nondeterminism, terminal→completion leakage, partial+uncertainty collapse, field conflict collapsing other fields);
- implementation requires semantic model judgment or general discourse/coreference parsing.

If a stop condition triggers, keep v1/v1.1 evidence frozen, pause deterministic structured extraction, and preregister any model-assisted or hybrid alternative as a new measurement approach. Do not silently expand v1.1.

## 19. Planned sequence and authorization boundary

| Stage | Scope | Authorization after completion |
|---|---|---|
| **This PR** | v1.1 preregistration only | Authorizes PR A1 implementation only |
| **PR A1** | Implement v1.1 extractor, golden, independent SHA lock, tests, and separate gate; preserve v1 | Authorizes PR B2 audit only |
| **PR B2** | Independent frozen calibration audit with fresh probes | May permit or pause PR C |
| **PR C** | Diagnostic-only structured processing of saved Run 001/002, only if B2 permits | No historical replacement or adoption |
| **PR D** | Measurement adoption decision | Only stage that may approve a future empirical pin |

No empirical pin is permitted before PR D. Until then classifier-v2 remains the temporary empirical default, classifier-v3 remains calibration/diagnostic-only, v1 remains frozen calibration-only, and v1.1 remains preregistered or calibration-only according to implementation stage.

## 20. Non-claims

This preregistration does not validate v1.1, prove robustness, estimate model behavior, infer intent, rank architectures, approve structured metrics, correct historical results, or authorize a model run or diagnostic processing. A future v1.1 exact-match result will be implementation conformance until independently audited.
