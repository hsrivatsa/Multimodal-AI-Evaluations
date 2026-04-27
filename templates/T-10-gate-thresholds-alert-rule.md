# T-10 — Gate Thresholds and Alert Rules
**Multimodal AI Feature Evaluation**

> **Purpose:** Per-metric monitoring configuration with gate thresholds, warning thresholds, owners, and actions.  
> **When to use:** Before deploying any production monitoring. Fill in every cell before the first alert is set up.  
> **Key rule:** Metrics without named owners and documented actions are not monitored — they are observed.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Version | |
| Date | |
| Owner | |

---

## Gate Threshold Table

> Metrics marked **(audio)** apply only to products producing audio output.  
> Metrics marked **(visual)** apply only to products producing visual output.

---

### Ingestion Contract

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| OCR character error rate on scanned docs | ≤ _____% | ≤ _____% | | |
| ASR word error rate — primary language | ≤ _____% | ≤ _____% | | |
| ASR word error rate — non-primary language | ≤ _____% | ≤ _____% | | |
| Caption retention rate | ≥ _____% | ≥ _____% | | |
| ASR hallucination rate | = 0 | > 0 | | Immediate investigation |
| Parse failure rate on supported file types | = 0 | > 0 | | Immediate rollback |
| Ingestion fidelity score (regression set) | ≥ _____% | ≥ _____% | | |

---

### Faithfulness Contract

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Faithfulness score (regression set) | ≥ _____% | ≥ _____% | | |
| Fabricated claim rate | = 0 | > 0 | | Immediate rollback |
| Speaker attribution accuracy | ≥ _____% | ≥ _____% | | |
| Cross-source merge rate | ≤ _____% | ≤ _____% | | |

---

### Factuality Contract

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Factuality score (regression set) | ≥ _____% | ≥ _____% | | |
| High-confidence incorrect claim rate | = 0 | > 0 | | Immediate escalation |

---

### Cross-Modal Consistency

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Cross-modal mismatch rate | ≤ _____ per 10 min | > _____ | | |
| Central contradiction rate | = 0 | > 0 | | Immediate rollback |
| Script-audio fidelity | ≥ _____% | ≥ _____% | | |

---

### Output Quality — Audio *(audio products only)*

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Audio MOS score | ≥ _____ | ≥ _____ | | |
| Audio glitch rate | ≤ _____ per 10 min | > _____ | | |
| Pronunciation accuracy on entity list | ≥ _____% | ≥ _____% | | |
| Script-audio alignment score | ≥ _____% | ≥ _____% | | |
| Silence gap > 5s rate | = 0 | > 0 | | Immediate investigation |

---

### Output Quality — Visual *(visual products only)*

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Layout validation pass rate | = 100% | < 100% | | |
| Taxonomic accuracy | ≥ _____% | ≥ _____% | | |
| Concept coverage score | ≥ _____% | ≥ _____% | | |

---

### Consumption Signals

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| Audio listen-through % — 7-day cohort | ≥ _____% | ≥ _____% | | Post-launch monitor |
| Audio listen-through % — 30-day cohort | ≥ _____% | ≥ _____% | | Cohort decay alert |
| Visual export rate | ≥ _____% | ≥ _____% | | |
| 7-day return visit rate | ≥ _____% | ≥ _____% | | |

---

### Operational

| Metric | Gate Threshold | Warning Threshold | Owner | Action on Gate Breach |
|---|---|---|---|---|
| P99 end-to-end latency | ≤ defined SLA | Warning line | | Auto-alert + page |
| Cost per output (p95) | ≤ Budget cap | Warning line | | Budget review |

---

## Alert Escalation Policy

### Immediate Rollback — No Discussion Required

| Trigger | Always Active? |
|---|---|
| Any zero-tolerance event fires | ☑ |
| Fabricated claim rate > 0 | ☑ |
| Central cross-modal contradiction detected | ☑ |
| Parse failure on any supported file type | ☑ |
| PII detected in any output modality | ☑ |

| Field | Value |
|---|---|
| Rollback owner | |
| Rollback time target | ≤ _____ minutes |

---

### Page On-Call — Within 15 Minutes

| Trigger | Always Active? |
|---|---|
| Any gate threshold breached | ☑ |
| P99 latency exceeds SLA | ☑ |
| Cost per output exceeds cap | ☑ |

| Field | Value |
|---|---|
| On-call owner | |

---

### Warning Alert — Investigate Within 24 Hours

| Trigger | Always Active? |
|---|---|
| Any warning threshold crossed | ☑ |
| Listen-through cohort decay detected | ☑ |

| Field | Value |
|---|---|
| Warning owner | |

---

### Weekly Review — No Immediate Action

| Trigger | Always Active? |
|---|---|
| Input distribution shift > 15% week-over-week | ☑ |
| Cost trend upward for 3+ consecutive days | ☑ |

| Field | Value |
|---|---|
| Review owner | |

---

## Segment Priority Tiers

| Tier | Description | Gate Action |
|---|---|---|
| Safety-critical | PII exposure, fabricated attribution, medical/legal hallucination | Block immediately; no ramp allowed |
| Business-critical | Core user flows, paid-tier reliability, flagship source types | Block on 3% regression from baseline |
| Growth-critical | New languages, new formats, onboarding flows | Monitor; gate at 10% regression |
| Exploratory | Edge source types, experimental formats | Report only; no gate |

---

## Drift Monitor Configuration

| Drift Type | What to Monitor | Alert Trigger |
|---|---|---|
| Input Drift | Weekly source-type distribution | Any category shifts > 15% week-over-week |
| Ingestion Drift | Daily canary on fixed corpus | Any metric drops > 20% from fixed baseline |
| Model Drift | Daily canary of fixed prompts | Output distribution shift above threshold |
| Judge Drift | Monthly kappa recalibration — 20 fresh labeled examples | Kappa drop > 0.10 from last measurement |
| Consumption Drift | 30-day cohort analysis | Week-4 listen-through drops > 20% vs. week-1 |

---

## Threshold Review History

| Review Date | Reviewer | What Changed | Rationale |
|---|---|---|---|
| | | | |
| | | | |
| | | | |
| | | | |

---

> Thresholds without named owners are not monitored — they are observed. Review this table quarterly as part of the Evaluation Debt Register (T-18).
