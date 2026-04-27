# T-15 — Experiment Pre-Registration
**Multimodal AI Feature Evaluation**

> **Purpose:** Lock in the hypothesis, primary metric, decision rule, and novelty exclusion window before any data is collected.  
> **When to use:** Before running any A/B experiment that touches an output modality. Non-negotiable for audio, visual, or video changes.  
> **Key rule:** Commit the decision rule before any data is seen. Once results are visible, the decision must follow the pre-committed rule — not a re-analysis.

---

## Document Header

| Field | Value |
|---|---|
| Experiment Name | |
| Date | |
| Owner | |
| Approver | |

---

## What Is Being Tested

| Field | Entry |
|---|---|
| Change being tested | |
| Hypothesis | If [change], then [primary metric] will [direction] by [estimated magnitude] because [reason] |

---

## Randomisation

| Field | Selection |
|---|---|
| Randomisation unit | ☐ User &nbsp; ☐ Session &nbsp; ☐ Query |
| Traffic split | Control: _____ &nbsp; Treatment: _____ |
| Justification if not user-level | |

### Randomisation Unit Guide

| Unit | Use When | Risk If Misapplied |
|---|---|---|
| User-level | Feature affects audio or video output | None — safe default for multimodal features |
| Session-level | Sessions ≥ 5 min; user-level technically difficult | Users experience inconsistency across sessions |
| Query-level | Change affects text output only — no audio or visual | For audio/video: users notice inconsistency and attribute it to product quality |

---

## Primary Metric

> One metric only. Do not add a second primary metric after seeing results.

| Field | Entry |
|---|---|
| Metric | |
| Direction | ☐ Higher is better &nbsp; ☐ Lower is better |
| Minimum detectable effect (MDE) | _____% |
| Required sample size | _____ users |
| Required duration | _____ days |
| Statistical method | |
| Significance level | α = _____ (default: 0.05) |

---

## Secondary Metrics

> Observed and reported only — **NOT** used for the go/no-go decision. Changing the decision rule to use secondary metrics after seeing results is a protocol violation.

| # | Secondary Metric |
|---|---|
| 1 | |
| 2 | |
| 3 | |

---

## Guardrail Metrics

If any guardrail is breached, the experiment stops immediately regardless of primary metric performance.

| # | Metric | Threshold | Action on Breach |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |

| Field | Entry |
|---|---|
| Guardrail breach owner | |

---

## Novelty Exclusion Window

| Field | Entry |
|---|---|
| First exposure date | |
| Primary metric measured from day | _____ to _____ (must be ≥ 14 days after first exposure) |

### Cohort Monitoring Plan

| Window | What It Measures | How to Use It |
|---|---|---|
| Days 1–7 | Initial engagement | Observe only — do NOT use as primary metric |
| Days 8–14 | Transition; novelty decay begins | Watch for rapid decline |
| Days 15–21 | Sustained engagement | Primary metric measurement window |
| Days 22+ | Repeat value; retention signal | Leading indicator of long-term product-market fit |

> ⚠️ Minimum experiment duration: **21 days**. Any experiment shorter than 21 days for an audio or video feature is measuring novelty, not value.

---

## Decision Rule

> Committed **before** any data is collected.

| Outcome | Condition | Action |
|---|---|---|
| Ship | Primary metric improves ≥ MDE, α < 0.05 | Proceed to production |
| Hold | Primary metric neutral (within ±MDE) | Do not ship; investigate |
| Rollback | Primary metric declines ≥ MDE, α < 0.05 | Revert immediately |

| Field | Entry |
|---|---|
| Decision owner | |
| Override condition (the one case where the committed rule does not apply, if any) | |

---

## Sign-Off

Required before the experiment launches.

| Role | Name | Signature | Date |
|---|---|---|---|
| Owner | | | |
| Product Lead | | | |
| Data / ML Lead | | | |

---

## Post-Experiment Record

Complete after the experiment concludes.

| Field | Entry |
|---|---|
| Experiment | |
| Completion date | |
| Primary metric result | _____% vs. MDE: _____% |
| Statistical significance | p = _____ &nbsp; α threshold = _____ |
| Guardrails triggered | ☐ None &nbsp; ☐ Yes — describe: |
| Decision rule applied | ☐ Ship &nbsp; ☐ Hold &nbsp; ☐ Rollback |
| Secondary metric observations | |
| Any deviation from pre-committed rule | ☐ No &nbsp; ☐ Yes — describe and justify: |

---

## Experiment Archive

| Experiment Name | Launch Date | Completion Date | Primary Metric Result | Decision | Deviation from Rule? |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |

---

> Pre-registration documents must be archived with a timestamp before the experiment launches. Any deviation from the pre-committed decision rule must be documented and reviewed by the Product Lead and Data Lead.
