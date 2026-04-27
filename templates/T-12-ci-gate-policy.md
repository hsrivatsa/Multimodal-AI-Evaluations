# T-12 — CI Gate Policy
**Multimodal AI Feature Evaluation**

> **Purpose:** The documented policy for what blocks a merge, what flags a merge for human review, and how false positives are handled.  
> **When to use:** Before wiring any evaluator to your CI system. Document this before the gate fires for the first time — not after.  
> **Key rule:** Suppressing a gate failure without documentation is a policy violation.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Version | |
| Date | |
| Policy Owner | |

---

## Blocking Conditions

Merge halts if any of these breach. No exceptions.

| Condition | Threshold | Active? |
|---|---|---|
| Ingestion fidelity regression | > 5% drop on any source type from baseline | ☐ |
| Faithfulness regression | > 1% false-positive rate on regression set | ☐ |
| Factuality regression | > 1% false-positive rate on regression set | ☐ |
| Any zero-tolerance event | 0 tolerance — blocks regardless of other scores | ☐ |
| Cross-modal alignment regression | > 5% regression from baseline | ☐ |
| Catastrophic tail failure in any modality | 0 allowed across any source type | ☐ |
| Pronunciation regression on entity list | > 2% drop from baseline | ☐ |
| [Product-specific condition] | | ☐ |
| [Product-specific condition] | | ☐ |

---

## Review-Flagged Conditions

PR annotated; human review required before merge is allowed.

| Condition | Threshold | Reviewer |
|---|---|---|
| Overall faithfulness | ≥ prior – 1% | |
| Overall factuality | ≥ prior – 1% | |
| Audio MOS | ≤ prior – 0.2 | |
| Latency per modality | ≤ prior + 15% | |
| Cost per output | ≤ prior + 10% | |
| Any named segment | > 5% regression | |

**Review SLA:** _____ hours

---

## False Positive Handling Protocol

| Step | Action | Required? |
|---|---|---|
| 1 | Run the failing case 3× before declaring a false positive (pin temperature=0 and seed first) | ☑ |
| 2 | If fails all 3 runs → genuine regression — investigate before proceeding | ☑ |
| 3 | If passes 2/3 → non-determinism issue → update suite pass threshold for this case | ☑ |
| 4 | Review the case with the relevant Judge before clearing any failure | ☑ |
| 5 | If Judge agrees → update evaluator rubric before clearing; do not clear without a rubric change | ☑ |
| 6 | Log every cleared false positive in the Evaluation Debt Register (T-18) | ☑ |
| 7 | Written note required in the PR — see fields below | ☑ |

---

## Required PR Note for Any Suppression

| Field | Content |
|---|---|
| What the failure was | |
| Why it was judged a false positive | |
| What evaluator change will prevent recurrence | |
| Approved by | |

---

## Non-Determinism Policy

| Rule | Standard |
|---|---|
| Generation calls | Pin temperature=0 and seed on all generation calls in CI |
| Audio comparison method | MFCC cosine distance — not byte equality |
| Visual comparison method | SSIM ≥ 0.95 — not pixel equality |
| Pass threshold | Run each case 3×; require 2/3 pass for CI green |

---

## Fast Gate vs. Full Regression Coverage

| Evaluator | Runs in Fast Gate (per-PR) | Runs in Nightly Full Regression |
|---|---|---|
| Ingestion fidelity | ☑ | ☑ |
| Faithfulness | ☑ | ☑ |
| Factuality | ☑ | ☑ |
| Audio quality — script + pronunciation | ☐ | ☑ |
| Audio quality — prosody + glitch | ☐ | ☑ |
| Cross-modal consistency | ☑ (text proxy) | ☑ (full audio + visual) |

---

## Suppression Log

Every suppressed gate failure must be recorded here.

| Date | PR | Failure Description | Reason for Suppression | Rubric Change Made | Approved By |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

---

## Suppression Pattern Review

Run this analysis quarterly as part of the Evaluation Debt Register (T-18). A pattern of recurring false positives on the same tag signals your evaluator rubric needs revision — not that your product is getting better.

| Failure Tag | Suppression Count This Quarter | Pattern Detected? | Action Required |
|---|---|---|---|
| | | ☐ Yes &nbsp; ☐ No | |
| | | ☐ Yes &nbsp; ☐ No | |
| | | ☐ Yes &nbsp; ☐ No | |
| | | ☐ Yes &nbsp; ☐ No | |

---

## Policy Version History

| Version | Date | Change | Author |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

---

> A pattern of recurring false positives on the same tag signals your evaluator rubric needs revision — not that your product is getting better. Review the suppression log quarterly as part of the Evaluation Debt Register (T-18).
