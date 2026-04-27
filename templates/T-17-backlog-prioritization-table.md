# T-17 — Backlog Prioritization Table
**Multimodal AI Feature Evaluation**

> **Purpose:** Priority-rank all identified interventions using a six-dimension formula that rewards upstream, high-blast-radius fixes.  
> **When to use:** After error analysis is complete and causal chains are documented. Re-run whenever significant new failures are identified.  
> **Key rule:** Zero-tolerance failure tags always route to the top of the backlog regardless of score.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Session Date | |
| Facilitator | |
| Based on error analysis run | |

---

## The Priority Formula

**Priority Score = (S × F × C × B × U) ÷ TTL**

| Dimension | Symbol | Definition | Scale |
|---|---|---|---|
| Severity | S | How bad is this failure when it occurs? | High = 3 · Medium = 2 · Low = 1 |
| Frequency | F | What % of traces contain this failure tag? | Express as decimal: 15% = 0.15 |
| Confidence | C | How certain are we that the proposed fix will work? | High = 3 · Medium = 2 · Low = 1 |
| Time to Live | TTL | How many days to deploy this fix? | Actual days |
| Blast Radius | B | How many downstream failure tags does this fix resolve? Count from causal chain documentation. | Count of downstream tags |
| Upstream-ness | U | Where in the pipeline does the fix apply? | Ingestion = 5 · Retrieval = 4 · Generation = 3 · Synthesis = 2 · Delivery = 1 |

---

## Zero-Tolerance Overrides

These items route to rank #1 regardless of formula score. Address before any other backlog item.

| Zero-Tolerance Item | Failure Tag | Owner | Target Date |
|---|---|---|---|
| | | | |
| | | | |
| | | | |
| | | | |

---

## Backlog Prioritization Table

> Sort by Score (descending) after calculating. Higher score = higher priority.

| # | Intervention Description | Failure Tag(s) | S | F | C | TTL (days) | B | U | Score | Rank | Owner |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | | | |
| 2 | | | | | | | | | | | |
| 3 | | | | | | | | | | | |
| 4 | | | | | | | | | | | |
| 5 | | | | | | | | | | | |
| 6 | | | | | | | | | | | |
| 7 | | | | | | | | | | | |
| 8 | | | | | | | | | | | |
| 9 | | | | | | | | | | | |
| 10 | | | | | | | | | | | |
| 11 | | | | | | | | | | | |
| 12 | | | | | | | | | | | |
| 13 | | | | | | | | | | | |
| 14 | | | | | | | | | | | |
| 15 | | | | | | | | | | | |

---

## Worked Reference Example

| Intervention | Tag | S | F | C | TTL | B | U | Score | Rank |
|---|---|---|---|---|---|---|---|---|---|
| Parser upgrade — drops captions | `ingestion.dropped_caption` | 3 | 0.15 | 3 | 3 | 3 | 5 | 6.75 | 1 |
| Pronunciation lexicon update (TTS) | `output.audio.mispronunciation` | 2 | 0.12 | 3 | 1 | 1 | 2 | 1.44 | 2 |
| Cross-modal consistency check | `cross_modal.output_mismatch` | 3 | 0.08 | 2 | 7 | 2 | 3 | 0.41 | 3 |

> The parser upgrade wins despite being slower to deploy — triple the blast radius (B=3 vs. B=1) and three pipeline stages upstream (U=5 vs. U=2). One fix; three failure tags resolved.

---

## Blast Radius Worksheet

Fill in one row per intervention before scoring. Count every tag in the causal chain, including the origin tag.

| Intervention | Origin Tag | Downstream Tag 1 | Downstream Tag 2 | Downstream Tag 3 | Blast Radius (B) |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

**Causal chain narrative** *(for any intervention with B ≥ 2):*

> Fix: [Intervention name]  
> Chain: [Tag A] → [Tag B] → [Tag C]  
> Story: [Plain-language explanation of how the upstream failure causes the downstream ones]  
> Expected benefit: Resolves ~_____% of [Tag B] and ~_____% of [Tag C] simultaneously.

---

## Dimension Calibration Guide

### Severity (S)

| Score | Criteria |
|---|---|
| 3 — High | Produces incorrect output a user trusts; zero-tolerance or near-zero-tolerance territory; domain catastrophic (medical, legal, financial); significant user trust damage |
| 2 — Medium | Degrades output quality noticeably; user may detect the error; reduces consumption signals measurably |
| 1 — Low | Minor quality issue; user unlikely to detect; limited impact on trust or consumption |

### Frequency (F)

| Value | Meaning |
|---|---|
| 0.30+ | Present in > 30% of traces — systemic issue |
| 0.10–0.29 | Present in 10–29% of traces — frequent issue |
| 0.05–0.09 | Present in 5–9% of traces — notable issue |
| < 0.05 | Present in < 5% of traces — tail issue |

### Confidence (C)

| Score | Criteria |
|---|---|
| 3 — High | Fix validated on similar system; root cause confirmed; expected metric movement is predictable |
| 2 — Medium | Root cause confirmed; fix approach reasonable but untested on this system |
| 1 — Low | Root cause plausible but not confirmed; fix approach is exploratory |

---

## Sprint Planning Output

Top-ranked items after scoring. These become the sprint backlog.

| Sprint Priority | Intervention | Failure Tag | Score | Owner | Target Date |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |

---

## Session History

| Session Date | Facilitator | Error Analysis Run Referenced | Items Scored | Top Priority Item | Notes |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |

---

> Re-run this table whenever significant new failures are identified from production or error analysis. Archive each version with the date and the error analysis run it drew from.
