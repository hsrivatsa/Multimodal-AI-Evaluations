# T-18 — Evaluation Debt Register
**Multimodal AI Feature Evaluation**

> **Purpose:** Quarterly audit of the evaluation program's health. Surfaces outdated rubrics, uncalibrated evaluators, stale datasets, taxonomy gaps, lapsed cadences, and production incidents not covered by the regression suite.  
> **When to use:** First week of each quarter. Run by the AI Reliability Lead with the full Judge Panel. Budget 3 hours.  
> **Key rule:** Every flagged item gets a named owner and a target date before the session ends. A debt register with no owners is a list of complaints, not a governance artifact.

---

## Document Header

| Field | Value |
|---|---|
| Team | |
| Quarter | |
| Review date | |
| Facilitated by | |
| Attendees | |

---

## RACI — Ownership Reference

Use this table to assign owners to every flagged item in this register.

| Role | Owns | Accountable For |
|---|---|---|
| AI Reliability Lead | Pipeline integrity, judge calibration, dataset lifecycle | Cross-modality evaluation health |
| Ingestion Engineer | Parser, OCR, ASR pipelines; ingestion canary | Ingestion fidelity; caption retention rate |
| Content Eval Engineer | Faithfulness, factuality, grounding evaluators | Faithfulness and factuality contracts |
| Audio / Visual Engineer | Output quality evaluators; TTS lexicon | Output quality contract |
| Product Manager | Consumption signals, quality bars, decision memos | Ship / Hold decisions |
| Judge Panel | Golden label sets, rubric review | Definition of "good" per modality |
| Safety / Policy | Safety gates, PII scrubbing, copyright | Zero-tolerance events |

---

## Section 1 — Cadence Audit

> The most commonly skipped governance activities cause the most regressions.

| Cadence | Frequency | Owner | Last Run | On Schedule? | Missed Runs This Quarter | Flag? |
|---|---|---|---|---|---|---|
| Prompt Review Board | Weekly | Prompt Eng Lead | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Evaluator calibration sample | Bi-weekly | ML Eng | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Full kappa measurement | Monthly | AI Reliability Lead | | ☐ Yes &nbsp; ☐ No | | ☐ |
| ASR/OCR vendor canary | Monthly | Ingestion Eng | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Consumption signal cohort analysis | Monthly | PM | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Holdout refresh + distribution audit | Quarterly | Data Eng | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Full evaluation debt review | Quarterly | AI Reliability Lead | | ☐ Yes &nbsp; ☐ No | | ☐ |
| Post-mortems — per incident | Per incident | All | | ☐ Yes &nbsp; ☐ No | | ☐ |
| T-10 Threshold Review | Quarterly | AI Reliability Lead | | ☐ Yes &nbsp; ☐ No | | ☐ |

### Prompt Review Board Audit

> The Prompt Review Board is the most commonly skipped governance activity and the one that prevents the most regressions. Any change to a system prompt must be reviewed before deployment.

| Field | Value |
|---|---|
| Prompt changes deployed this quarter | |
| Prompt changes reviewed by the board | |
| Prompt changes bypassed without review | |
| Bypassed changes that caused a regression | |

> ⚠️ Any bypassed prompt change that caused a regression is a process failure, not just a technical one.

| Bypassed Change | Regression Caused | Corrective Action | Owner |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

**Lapsed cadence count:** _____ flags

---

## Section 2 — Outdated Rubrics

> Flag any rubric not reviewed by a Judge in more than 90 days. See T-05 through T-09 for the current evaluator prompt versions that each rubric governs.

| Rubric | Last Reviewed | Reviewed By | Status | Owner | Target Date |
|---|---|---|---|---|---|
| Ingestion fidelity rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| Faithfulness rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| Factuality rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| Audio quality rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| Visual taxonomy rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| Cross-modal consistency rubric | | | ☐ Current &nbsp; ☐ Overdue | | |
| [Product-specific rubric] | | | ☐ Current &nbsp; ☐ Overdue | | |

**Overdue rubric count:** _____ flags

---

## Section 3 — Unvalidated Evaluators

> Flag any evaluator not recalibrated in more than 90 days, or with a kappa drop of more than 0.10 since last measurement.

| Evaluator | Version | Last Calibrated | Current Kappa | Delta from Previous | Status | Owner | Target Date |
|---|---|---|---|---|---|---|---|
| Ingestion fidelity | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |
| Faithfulness | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |
| Factuality | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |
| Audio quality | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |
| Cross-modal consistency | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |
| [Product-specific] | v____ | | | | ☐ Current &nbsp; ☐ Overdue | | |

> ⚠️ A kappa drop of more than 0.10 since last measurement signals the judge model was likely silently updated. Investigate before trusting current scores.

**Unvalidated evaluator count:** _____ flags

---

## Section 4 — Stale Datasets

> See T-16 (Dataset Record) for full dataset metadata, version history, and distribution audit results.

| Dataset | Version | Last Refreshed | Distribution Audit | Status | Owner | Target Date |
|---|---|---|---|---|---|---|
| Iteration set | v____ | | ☐ Matches traffic &nbsp; ☐ Stale | ☐ Current &nbsp; ☐ Stale | | |
| Validation set | v____ | | ☐ Matches traffic &nbsp; ☐ Stale | ☐ Current &nbsp; ☐ Stale | | |
| Regression suite | v____ | | ☐ Matches traffic &nbsp; ☐ Stale | ☐ Current &nbsp; ☐ Stale | | |
| Holdout set | v____ | | ☐ Matches traffic &nbsp; ☐ Stale | ☐ Current &nbsp; ☐ Stale | | |
| Red-team adversarial set | v____ | | ☐ Matches traffic &nbsp; ☐ Stale | ☐ Current &nbsp; ☐ Stale | | |
| Canary corpus | v1.0 — fixed | Never refresh | N/A — fixed by design | ☐ Intact &nbsp; ☐ Modified | | |

### Media Blob Expiry Audit

| Case ID | Failure Tag | Blob URI | SHA-256 Hash | Expiry Date | Status | Action Required |
|---|---|---|---|---|---|---|
| | | | | | ☐ Valid &nbsp; ☐ Expired | |
| | | | | | ☐ Valid &nbsp; ☐ Expired | |
| | | | | | ☐ Valid &nbsp; ☐ Expired | |
| | | | | | ☐ Valid &nbsp; ☐ Expired | |

**Expired blob count:** _____ cases invalidated  
**Stale dataset count:** _____ flags

---

## Section 5 — Taxonomy Coverage Gaps

> Any tag with fewer than 5 cases in the regression suite is a blind spot.

| Failure Tag | Cases in Suite | Minimum Required | Gap? | Owner | Target Date |
|---|---|---|---|---|---|
| `ingestion.[type].dropped_caption` | | 5 | ☐ | | |
| `ingestion.[type].layout_scramble` | | 5 | ☐ | | |
| `ingestion.ocr.scanned_drop` | | 5 | ☐ | | |
| `ingestion.ocr.handwriting` | | 5 | ☐ | | |
| `ingestion.asr.term_miss` | | 5 | ☐ | | |
| `ingestion.asr.silence_hallucination` | | 5 | ☐ | | |
| `retrieval.modality_bias` | | 5 | ☐ | | |
| `retrieval.visual_chunk_dropped` | | 5 | ☐ | | |
| `grounding.faithfulness_break` | | 5 | ☐ | | |
| `grounding.speaker_attribution` | | 5 | ☐ | | |
| `grounding.cross_source_merge` | | 5 | ☐ | | |
| `generation.fabricated_quote` | | 5 | ☐ | | |
| `generation.invented_statistic` | | 5 | ☐ | | |
| `cross_modal.output_mismatch` | | 5 | ☐ | | |
| `cross_modal.speaker_drift` | | 5 | ☐ | | |
| `output.audio.mispronunciation` | | 5 | ☐ | | |
| `output.audio.prosody_flat` | | 5 | ☐ | | |
| `output.audio.script_drift` | | 5 | ☐ | | |
| `output.visual.layout_overlap` | | 5 | ☐ | | |
| `output.visual.taxonomic_error` | | 5 | ☐ | | |
| `output.visual.concept_gap` | | 5 | ☐ | | |
| `safety.pii_in_output` | | 5 | ☐ | | |
| `safety.copyright_reproduction` | | 5 | ☐ | | |
| [Product-specific tag] | | 5 | ☐ | | |
| [Product-specific tag] | | 5 | ☐ | | |

### New Failure Patterns Not Yet in Taxonomy

| # | Pattern Description | Proposed Tag | Owner |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

### Languages Below Statistical Minimum

> Flag any language with fewer than 30 labeled cases in the evaluation dataset.

| Language | Current Cases | Minimum Required | Action |
|---|---|---|---|
| | | 30 | |
| | | 30 | |

**Taxonomy gap count:** _____ tags below minimum

---

## Section 6 — Production Incident Loop

> A program that adds every production failure to the regression suite within one sprint of discovery is operating at full maturity. A lag rate above 50% means the program is reactive.

| Field | Value |
|---|---|
| Production incidents this quarter | |
| Incidents covered by regression suite at time of incident | |
| Incidents NOT covered — evaluation program lag | |
| Lag rate | _____% |

### For Each Uncovered Incident — Document and Close the Loop

| Incident | Root Cause Tag | Was tag in taxonomy? | Regression case added? | Added by | Date |
|---|---|---|---|---|---|
| | | ☐ Yes &nbsp; ☐ No | ☐ Yes &nbsp; ☐ No | | |
| | | ☐ Yes &nbsp; ☐ No | ☐ Yes &nbsp; ☐ No | | |
| | | ☐ Yes &nbsp; ☐ No | ☐ Yes &nbsp; ☐ No | | |

### Post-Mortem Instrumentation Gaps

> For each incident, answer: "What should we have logged?" Add every identified field to T-04 (Minimum Logging Schema) this quarter.

| Incident | Gap Identified | Field to Add to T-04 Logging Schema | Owner |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

**Uncovered incident count:** _____ flags

---

## Section 7 — Gate Suppression Log Review

> A pattern of recurring suppressions on the same tag signals an evaluator rubric problem, not a product improvement. See T-12 (CI Gate Policy) for the source suppression log.

| Field | Value |
|---|---|
| Total gate suppressions this quarter | |
| Suppressions with complete documentation | |
| Undocumented suppressions | |

### Recurring Suppression Patterns

> Flag any tag suppressed more than twice in a quarter — this signals a rubric revision is needed, not a threshold adjustment.

| Tag | Suppression Count This Quarter | Rubric Action Required | Owner | Target Date |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |
| | | | | |

**Suppression flags:** _____ tags suppressed more than twice without rubric revision

---

## Section 8 — Priority Items This Quarter

> Every item flagged in Sections 1–7 must appear here with a named owner and a target date. No item leaves this session without both.

| # | Item | Source Section | Owner | Target Date | Status |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |
| 6 | | | | | |
| 7 | | | | | |

---

## Debt Score

Count all flags raised across Sections 1–7.

| Section | Flags Raised |
|---|---|
| Section 1 — Lapsed cadences | |
| Section 2 — Outdated rubrics | |
| Section 3 — Unvalidated evaluators | |
| Section 4 — Stale datasets + expired blobs | |
| Section 5 — Taxonomy coverage gaps | |
| Section 6 — Production incident loop | |
| Section 7 — Gate suppressions | |
| **Total Debt Flags** | |

### Debt Score Interpretation

| Score | Status | Recommended Action |
|---|---|---|
| 0–5 | Healthy — routine maintenance | Address flagged items within the quarter; no special action needed |
| 6–12 | Drift beginning | Dedicate a sprint to evaluation program maintenance before next quarter |
| 13–20 | Significant debt | Run the 12-Week Plan from Phase 1 to rebuild the foundation |
| 20+ | Critical | Treat as a reliability incident; escalate to product and engineering leadership immediately |

---

## Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| AI Reliability Lead | | | |
| Content Judge | | | |
| Ingestion Judge | | | |
| Product Manager | | | |

---

## Register History

| Quarter | Total Flags | Key Issues This Quarter | Priority Items Completed |
|---|---|---|---|
| | | | |
| | | | |
| | | | |
| | | | |

---

> The evaluation debt register is the maintenance record of your evaluation program. A program with a growing debt score quarter over quarter is producing evaluators for an outdated definition of quality and making decisions on scores that cannot be trusted. Run this review without exception. Governance that is not on the calendar does not happen.
