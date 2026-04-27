# T-01 — Evaluation Brief
**Multimodal AI Feature Evaluation**

> **Purpose:** Team alignment on all five quality contracts before any evaluation work begins.  
> **When to use:** At the start of every new feature or major model update. Fill this in before running any evaluations. Set every threshold before seeing any scores.  
> **Who signs:** All four judges, the Product Lead, and the Engineering Lead.

---

## Document Header

| Field | Value |
|---|---|
| Feature Name | |
| Version | |
| Date | |

---

## 1. Judge Panel

| Role | Name |
|---|---|
| Content Judge | |
| Ingestion Judge | |
| Audio Judge | |
| Visual Judge | |
| Tiebreaker | |

---

## 2. Modalities

**Inputs — check all that apply:**

| PDF | Slides | Audio | Video | Image | Web | Other |
|---|---|---|---|---|---|---|
| ☐ | ☐ | ☐ | ☐ | ☐ | ☐ | |

**Outputs — check all that apply:**

| Text | Audio | Visual | Video | Interactive | Other |
|---|---|---|---|---|---|
| ☐ | ☐ | ☐ | ☐ | ☐ | |

---

## 3. User Job Statement

One sentence in the user's voice:

> "When I _________________________, I want to _________________________ so I can _________________________."

---

## 4. What "Good" Feels Like

One sentence per output type:

| Output Type | Definition of Good |
|---|---|
| Audio | |
| Visual | |
| Text | |

---

## 5. Deterministic Success Criteria

| Criterion | Target |
|---|---|
| All supported file types parse without error | 100% |
| Output renders within | _____ seconds |
| Null output rate | Zero |

---

## 6. Quality Contracts

### Contract 1 — Ingestion Fidelity

| Metric | Threshold |
|---|---|
| Overall bar (clean documents) | ≥ _____% |
| Tail threshold (scanned / noisy) | ≤ _____% failure rate |
| Caption retention | ≥ _____% |
| OCR character error rate | ≤ _____% |
| ASR word error rate | ≤ _____% |
| Zero-tolerance event | |

---

### Contract 2 — Faithfulness (output ↔ sources)

| Metric | Threshold |
|---|---|
| Overall bar (% claims traceable) | ≥ _____% |
| High-stakes segment bar | ≥ _____% on _________ |
| Zero-tolerance event 1 | |
| Zero-tolerance event 2 | |

---

### Contract 3 — Factuality (output ↔ world)

| Metric | Threshold |
|---|---|
| Overall bar (verifiable claims) | ≥ _____% |
| Domain zero-tolerance event | |

---

### Contract 4 — Cross-Modal Consistency

| Metric | Threshold |
|---|---|
| Narration / visual mismatch rate | ≤ _____ per 10 min |
| Speaker attribution accuracy | ≥ _____% |
| Zero-tolerance event | |

---

### Contract 5 — Output Quality

| Metric | Threshold |
|---|---|
| Audio MOS | ≥ _____ |
| Audio glitch rate | ≤ _____ per 10 min |
| Pronunciation on entity list | ≥ _____% |
| Visual layout validity | Pass / Fail |
| Visual taxonomic accuracy | ≥ _____% |

---

## 7. Consumption Targets

| Metric | Threshold |
|---|---|
| Listen-through % (by day 7) | ≥ _____% |
| Visual export / share rate | ≥ _____% |
| Repeat engagement within 7 days | ≥ _____% |

---

## 8. Pending Decision

Decision expected in the next 2–4 weeks:  
☐ Ship &nbsp; ☐ Ramp &nbsp; ☐ Hold &nbsp; ☐ Rollback

Evidence that would change that decision:

| Trigger | Action |
|---|---|
| Ship → Hold | |
| Hold → Rollback | |

---

## 9. Riskiest Assumption

> "If _________________________, the feature is useless."

**Test method:**

---

## 10. Sign-Off

All six signatures required before evaluation work begins.

| Role | Name | Signature | Date |
|---|---|---|---|
| Content Judge | | | |
| Ingestion Judge | | | |
| Audio Judge | | | |
| Visual Judge | | | |
| Product Lead | | | |
| Engineering Lead | | | |

---

## Completion Guide

### Judge Panel

| Role | Jurisdiction |
|---|---|
| Content Judge | Factual accuracy, claim grounding, source representation |
| Ingestion Judge | Parsing, transcription, figure extraction — reads raw pipeline output |
| Audio Judge | Voice naturalness, pacing, pronunciation, prosody |
| Visual Judge | Layout, node clarity, taxonomic structure, readability |
| Tiebreaker | Final decision authority when panel disagrees |

You need one person per quality dimension. Minimum viable structure is two people — one for content and ingestion, one for output quality. If you cannot name a person for a role, filling that gap is your first priority — not the evaluation program itself.

---

### Setting Thresholds

Set every threshold before running any evaluations. Teams that measure first and set thresholds after anchor to what's currently achievable — not what users need. If your current performance is below the bar you set, that is a product decision, not a reason to lower the bar.

---

### Zero-Tolerance Events

Name at least two failure types per contract that trigger an immediate rollback regardless of all other scores. Examples: a fabricated quote with named attribution; a parse failure on any supported file type; PII appearing in output. Zero-tolerance means exactly that — no discussion, no exceptions.

---

### Riskiest Assumption

Leave nothing blank here. The blank is the problem. Fill in the assumption that, if false, makes the feature useless — and commit to a test method before launch.

---

### Common Mistakes

| Mistake | How to Spot It | Fix |
|---|---|---|
| Single accuracy metric | "95% accurate" covers all five contracts | Split into one number per contract |
| Thresholds set after seeing scores | Team anchors to what's currently achievable | Set thresholds before running any evaluations |
| No zero-tolerance events named | All metrics are distributional | Name at least two catastrophic failures |
| Skipping consumption targets | Only technical metrics listed | Add at least one behavior metric per output modality |
| Brief unsigned | No formal agreement exists | All judges plus PM and Eng Lead must sign |
| Riskiest assumption left blank | Team is avoiding a hard question | Fill it in and test it first |

---

> This brief is the anchor for every rubric, threshold, and quality bar in the evaluation program. Version-control this document alongside your evaluation runs. Tag every version with the feature name and date.
