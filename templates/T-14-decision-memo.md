# T-14 — Decision Memo
**Multimodal AI Feature Evaluation**

> **Purpose:** An evidence-backed record for every Ship, Ramp, Hold, or Rollback decision.  
> **When to use:** For every significant product or ramp decision.  
> **Key rule:** Write the reversal conditions before executing the decision. Once a rollout is announced, organisational pressure works against rolling back. Pre-committing removes that pressure.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Version | |
| Date | |
| Author | |

---

## Decision

| Field | Selection |
|---|---|
| Decision | ☐ Ship to GA &nbsp; ☐ Ramp to _____ &nbsp; ☐ Hold &nbsp; ☐ Rollback |
| Reversibility | ☐ Easy &nbsp; ☐ Hard &nbsp; ☐ Irreversible |

---

## Evidence Summary — Contract Scores

| Contract | Current Score | Baseline | Delta | Status |
|---|---|---|---|---|
| Ingestion Fidelity | _____% | _____% | | ☐ Pass &nbsp; ☐ Fail |
| Faithfulness | _____% | _____% | | ☐ Pass &nbsp; ☐ Fail |
| Factuality | _____% | _____% | | ☐ Pass &nbsp; ☐ Fail |
| Cross-Modal Consistency | _____ / 10 min | _____ / 10 min | | ☐ Pass &nbsp; ☐ Fail |
| Audio MOS | _____ | _____ | | ☐ Pass &nbsp; ☐ Fail |

---

## Evidence Summary — Consumption Signals

| Signal | Current | Baseline | Cohort Window | Status |
|---|---|---|---|---|
| Listen-through % | _____% | _____% | Day _____ | ☐ On track &nbsp; ☐ Declining |
| Visual export rate | _____% | _____% | | ☐ On track &nbsp; ☐ Declining |
| 7-day return rate | _____% | _____% | | ☐ On track &nbsp; ☐ Declining |

---

## Zero-Tolerance Events

| Field | Entry |
|---|---|
| Zero-tolerance events detected | ☐ None &nbsp; ☐ Present — describe below |
| Description | |

---

## Signal Conflict Assessment

| Field | Entry |
|---|---|
| Do automated metrics and user behaviour agree? | ☐ Aligned — no conflict &nbsp; ☐ Conflict detected |
| Conflict description | |
| Resolution | |

> ⚠️ When automated metrics and user behaviour disagree, believe the users. Run a manual Judge Panel review of 20 recent outputs before making a decision.

---

## Options Considered

Document at least three options before making a recommendation.

| Option | Description | Key Risks |
|---|---|---|
| A | | |
| B | | |
| C | | |

---

## Recommendation and Rationale

| Field | Entry |
|---|---|
| Recommended action | |
| Rationale | |

---

## Accepted Risks by Modality

| Modality | Accepted Risk |
|---|---|
| Audio | |
| Visual | |
| Ingestion | |

---

## Reversal Conditions

> Committed **before** the decision executes. These are pre-commitments, not suggestions.

| # | If This Happens | Action | Window |
|---|---|---|---|
| 1 | [metric] < [threshold] | | within _____ days |
| 2 | | | |
| 3 | | | |

| Field | Entry |
|---|---|
| Reversal decision owner | |
| Rollback time target | _____ minutes |

---

## Sign-Off

All six signatures required before the decision executes.

| Role | Name | Signature | Date |
|---|---|---|---|
| Content Judge | | | |
| Ingestion Judge | | | |
| Audio Judge | | | |
| Visual Judge | | | |
| Product Lead | | | |
| Engineering Lead | | | |

---

## Decision Rubric

| Observed Pattern | Recommended Action | Why |
|---|---|---|
| All five contracts pass; one segment regresses | Scope-restrict; continue ramp; fix segment in parallel | Don't let an edge case block a working product |
| Ingestion regressed; generation quality good | Hold. Fix ingestion before anything else. | Quality built on regressed ingestion will fail unpredictably |
| Technical metrics up; consumption down | Hold. Investigate judge drift or unmeasured quality dimension. | Users are more honest than evaluators |
| Judges green; user satisfaction declining | Hold; manual Judge Panel review of 20 recent traces first | Trust users first |
| Audio quality up; pronunciation down on entity list | Hold; update pronunciation lexicon before continuing | Named entity accuracy is a trust issue |
| All metrics up; cost up > 30% | Ramp slowly; add cost guardrail | This will force a quality regression later |
| Any zero-tolerance event in any modality | Rollback immediately. No exceptions. | Zero-tolerance means exactly that |
| Cost per output trending up 3+ consecutive days | Monitor closely; set explicit cost guardrail before next ramp stage | Early cost trends always accelerate — address before the guardrail triggers |

---

## Decision History Log

| Date | Feature | Decision | Key Evidence | Reversal Triggered? | Outcome |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

---

> A decision without a written memo is an opinion, not a decision. Pre-committed reversal conditions are what separate ramp discipline from optimism.
