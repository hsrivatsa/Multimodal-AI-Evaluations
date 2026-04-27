# T-02 — Quality Statement
**Multimodal AI Feature Evaluation**

> **Purpose:** The technical specification that monitoring systems and CI gates reference. Translates the team alignment in T-01 into precise, system-readable thresholds.  
> **When to use:** After the Evaluation Brief (T-01) is signed. Fill this in before designing any evaluator or monitoring alert.  
> **Key distinction:** The Brief aligns the team. The Quality Statement specifies the system.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Version | |
| Date | |

---

## Contract 1 — Ingestion Fidelity

### Summary Thresholds

| Metric | Threshold |
|---|---|
| Overall bar | ≥ _____% for [primary source type] |
| Tail threshold | ≤ _____% failure rate on [noisy / scanned docs] |
| Critical segment | ≥ _____% for [high-value source type] |
| Zero tolerance | Parse failure = 0 on all supported file types |

### Specific Metrics

| Metric | Threshold |
|---|---|
| Caption retention rate | ≥ _____% |
| OCR character error rate | ≤ _____% |
| ASR word error rate | ≤ _____% |
| ASR hallucination rate | = 0 |

---

## Contract 2 — Faithfulness (output ↔ sources)

### Summary Thresholds

| Metric | Threshold |
|---|---|
| Overall bar | ≥ _____% of claims traceable |
| Segment bar | ≥ _____% on [high-stakes domain] |
| Zero tolerance | Fabricated quotes or invented citations |

### Specific Metrics

| Metric | Threshold |
|---|---|
| Speaker attribution accuracy | ≥ _____% |
| Cross-source merge rate | ≤ _____% |

---

## Contract 3 — Factuality (output ↔ world)

### Summary Thresholds

| Metric | Threshold |
|---|---|
| Overall bar | ≥ _____% on verifiable claims |
| Zero tolerance | [domain-specific catastrophic failure] |

### Domain Zero-Tolerance Event

> Describe the specific factual failure that triggers immediate rollback in your domain — e.g., incorrect drug dosage in a medical product, wrong regulatory figure in a compliance product.

---

## Contract 4 — Cross-Modal Consistency

| Metric | Threshold |
|---|---|
| Mismatch rate | ≤ _____ per 10 minutes of output |
| Attribution accuracy | ≥ _____% |
| Script-audio fidelity | ≥ _____% |
| Zero tolerance | Complete contradiction of a central claim across modalities |

---

## Contract 5 — Output Modality Quality

### Audio

| Metric | Threshold |
|---|---|
| MOS score | ≥ _____ |
| Glitch rate | ≤ _____ per 10 min |
| Pronunciation on entity list | ≥ _____% |
| Script-audio alignment | ≥ _____% |

### Visual

| Metric | Threshold |
|---|---|
| Layout validation pass rate | = 100% |
| Taxonomic accuracy | ≥ _____% |
| Concept coverage score | ≥ _____% |

---

## Consumption Bars

| Metric | Threshold |
|---|---|
| Audio listen-through % — 7-day cohort | ≥ _____% |
| Audio listen-through % — 30-day cohort | ≥ _____% |
| Visual export rate | ≥ _____% |
| Visual share rate | ≥ _____% |
| Repeat engagement (7 days) | ≥ _____% |

---

## Rollback Triggers

Any one of these firing requires immediate action regardless of all other scores.

| # | Trigger | Status |
|---|---|---|
| 1 | Any zero-tolerance event in any contract | Always active |
| 2 | Ingestion fidelity drops > 5% on any source type | Always active |
| 3 | Fabricated claim rate > 0 | Always active |
| 4 | Cross-modal central contradiction detected | Always active |
| 5 | Audio MOS drops below _____ | Fill in threshold |
| 6 | Listen-through drops below _____% within 7 days | Fill in threshold |

---

## Version Control

| Field | Value |
|---|---|
| This version | v_____ |
| Supersedes | v_____ |
| Last updated | |
| Updated by | |
| Change summary | |

---

## Reference Quality Bars (April 2026)

> Use these as starting points only. Set your own bars based on your domain and user stakes. Do not adopt these numbers without validating them against your product's actual risk profile.

| Contract | Baseline Bar | Strong Bar | Immediate Rollback Example |
|---|---|---|---|
| Ingestion Fidelity | ≥ 95% (clean docs) | ≥ 98% | Parse failure on any supported file type |
| Faithfulness | ≥ 93% claims traceable | ≥ 97% | Fabricated quote with named attribution |
| Factuality | ≥ 90% verifiable claims | ≥ 97% | Domain-specific factual catastrophe |
| Cross-Modal Consistency | ≤ 2 mismatches / 10 min | ≤ 1 / 10 min | Both modalities assert the same fabricated finding |
| Audio Quality (MOS) | ≥ 3.8 | ≥ 4.2 | Silence gap > 5 seconds |

---

## How This Document Is Used

| System | Uses This Document For |
|---|---|
| CI gate | Threshold values for blocking and review-flagged conditions (T-12) |
| Production monitoring | Gate and warning thresholds per metric (T-10) |
| Decision memos | Baseline values against which deltas are measured (T-14) |
| Evaluator prompts | Fail criteria definitions (T-05 through T-09) |
| Experiment pre-registration | Guardrail metric thresholds (T-15) |

---

## Versioning Rules

- Increment the version number any time a threshold changes
- Never edit a threshold retroactively after evaluation runs have referenced it
- Tag each version with the evaluation runs that used it
- If the panel cannot agree on a threshold, that disagreement is the most valuable output of the session — resolve it and document it before proceeding

---

> This document is the technical specification for the evaluation system. For team alignment context and sign-off, see T-01 (Evaluation Brief).
