# Evaluation Reports
### Applying the Multimodal AI Evaluation Framework to Real Products in the Wild

This directory contains independent evaluation reports for multimodal AI products assessed against the five quality contracts defined in this framework — Ingestion Fidelity, Faithfulness, Factuality, Cross-Modal Consistency, and Output Quality. Each report applies the same structured methodology, the same rubrics, and the same thresholds to every product evaluated. The goal is a consistent, evidence-backed view of how real products perform against a common standard — not a ranking, not a review, and not a vendor comparison.

These reports are independent. No product vendor has sponsored, reviewed, or approved any evaluation before publication.

---

## Product Evaluation Index

| Product | Category | Protocol Stage | Report | Status |
|---|---|---|---|---|
| **Huxe** | Personal intelligence AI | Pilot Protocol v3 | [View Report →](./huxe/huxe-evaluation-v3.md) | 🟡 Published — Simulation-derived scores |
| **Google NotebookLM** | Document-to-audio AI | — | [View Report →](./google-notebooklm/) | 🔜 Coming Soon |
| **HeyGen** | AI video generation | — | [View Report →](./heygen/) | 🔜 Coming Soon |
| **Synthesia** | Enterprise AI video | — | [View Report →](./synthesia/) | 🔜 Coming Soon |
| **Loom AI** | Async video + AI summary | — | [View Report →](./loom-ai/) | 🔜 Coming Soon |
| **Descript** | Multimodal audio/video editing | — | [View Report →](./descript/) | 🔜 Coming Soon |
| **Adobe Firefly** | Generative image AI | — | [View Report →](./adobe-firefly/) | 🔜 Coming Soon |

### Protocol Stage Definitions

Every report in this directory carries one of three protocol stage labels. The label determines how scores should be interpreted. A Pilot Protocol score and a Full Evaluation score are not the same thing, and the distinction is never hidden.

| Protocol Stage | What It Means | Score Type |
|---|---|---|
| **Pilot Protocol** | Structured evaluation without production trace access. Scores are calibrated hypotheses derived from architecture reasoning, published reviews, and structured simulation. Use as a starting point for a real pilot — not as an audited product metric. | [SIM-EST] — Simulation-derived |
| **Beta Evaluation** | Limited trace access. Scores are partially empirical. Sample size is stated explicitly and may be below the minimum for full statistical confidence. | Partially empirical — sample size stated |
| **Full Evaluation** | Production trace access. Empirical scores. Sample size meets the minimum thresholds defined in this framework. | Empirical — audited |

---

## Evidence Provenance Standards

Every score, kappa value, count, and percentage in every report in this directory carries one of four evidence labels. This labeling is not a disclaimer — it is a methodological commitment. A simulated score treated as empirical data is worse than no score, because it gives false confidence. All future reports must adopt this labeling system.

| Label | What It Means |
|---|---|
| **[SIM]** | Simulated — derived from structured reasoning about the product, not actual trace access |
| **[EST]** | Estimated — calibrated against public data sources (reviews, architecture patterns, industry benchmarks) |
| **[REV]** | Review-derived — directly supported by published App Store, Google Play, or press reviews |
| **[INF]** | Architectural inference — derived from known patterns in similar multimodal pipeline systems |

Labels may be combined where appropriate (e.g., **[SIM]+[REV]** for a failure pattern confirmed by both structured simulation and published user reviews, or **[SIM-EST]** for a simulated score calibrated against external benchmarks).

**Application rule:** Apply the evidence label to every specific claim, score, or count — not to the report as a whole. A single report will typically contain multiple label types. The Huxe report (v3 Pilot Protocol) is the reference implementation of this labeling system.

---

## What Each Report Covers

Every evaluation report follows the same core structure. A report that skips a contract must mark it N/A with a one-line explanation — a blank is not acceptable. Reports on architecturally complex products may include supplementary sections beyond the five contracts; these are documented in the Supplementary Sections reference below.

---

### Core Structure

#### Executive Summary
One to two paragraphs covering: what the product is, the central architectural insight that drives the evaluation design, the overall finding, and a single-sentence verdict. The executive summary is immediately followed by two mandatory blocks before any deep-dive section begins.

**Block 1 — Score Summary Table** *(immediately after Executive Summary)*

| Contract | Score | Threshold | Status | Zero-Tolerance Events |
|---|---|---|---|---|
| Ingestion Fidelity | | ≥ defined bar | 🔴 / 🟡 / 🟢 | |
| Faithfulness | | ≥ defined bar | 🔴 / 🟡 / 🟢 | |
| Factuality | | ≥ defined bar | 🔴 / 🟡 / 🟢 | |
| Cross-Modal Consistency | | ≤ defined bar | 🔴 / 🟡 / 🟢 | |
| Output Quality | | ≥ defined bar | 🔴 / 🟡 / 🟢 | |

All scores carry their evidence label. Where a contract does not apply to the product's modality profile, the score cell reads `N/A` with a one-line explanation. Status indicators: 🔴 FAIL · 🟡 WARN · 🟢 PASS · ⚪ NOT EVALUATED.

**Block 2 — Zero-Tolerance Summary** *(immediately after Score Summary)*

List every zero-tolerance event detected, its evidence label, and the recommended action. If no zero-tolerance events were detected, this block states that explicitly — it is never omitted. A zero-tolerance event is never buried in contract-level detail.

| Event | Evidence Label | Action |
|---|---|---|
| [Description of event] | [SIM] / [REV] / etc. | Rollback / Hold / Investigate |

---

#### Contract 1 — Ingestion Fidelity
How faithfully does the product extract content from its input sources? This covers document parsing, OCR on scanned inputs, ASR on audio, email thread integrity, caption and figure retention, and reading-order preservation.

**For document-to-audio products:** Ingestion Fidelity is the contract that determines everything downstream. A faithfulness gap traced to ingestion is not a generation problem — it is a Stage 1 problem, and fixing it at Stage 1 resolves the downstream chain.

**For personal intelligence / ambient AI products:** The primary inputs are email threads, calendar entries, live news feeds, and social media — not user-uploaded documents. Ingestion Fidelity here covers email thread context retention, HTML parsing quality, calendar attendee and timezone accuracy, and feed deduplication. The ingestion surface is also the primary privacy risk surface for these products.

#### Contract 2 — Faithfulness
Are the product's output claims traceable to the source material it was given? This is not a factuality check — it is a source-grounding check. A product can be faithful to bad sources. A product can also fabricate claims that happen to be factually correct. Faithfulness measures the link between output and source, not output and world.

**Tense fidelity** is a faithfulness sub-dimension specific to live-data products: a future calendar event stated in past tense is a faithfulness failure, not a factuality failure. Evaluate tense separately for any product ingesting time-sensitive sources.

#### Contract 3 — Factuality
Are the product's verifiable output claims correct about the world? Named entities, dates, statistics, and attributions are the primary targets. This contract is evaluated independently of faithfulness — a claim can pass faithfulness (it is in the sources) and fail factuality (the source was wrong and the product stated it as fact).

#### Contract 4 — Cross-Modal Consistency
When a product produces output across more than one modality — audio narration alongside a transcript overlay, for example — do those modalities tell the same story? A central contradiction between modalities is a zero-tolerance failure regardless of how well each modality performs independently. Absence of a topic in one modality is not a contradiction.

**For products with real-time interaction layers** (e.g., voice interruption mid-stream): cross-modal consistency includes post-interruption state consistency — the product must not contradict itself or repeat already-covered content after a user interaction.

#### Contract 5 — Output Quality

**Audio dimensions:**
- Voice naturalness, host differentiation, and prosodic appropriateness
- Pronunciation accuracy on entity reference list (sender names, company names, technical terms, product acronyms)
- Script-audio alignment and glitch rate
- Interruption recovery naturalness — evaluated by listening, not transcript review

**Audio-native evaluation requirement:** For audio-first products, transcript review alone is insufficient. The following six dimensions must be evaluated by an Audio Judge listening to actual audio output — they are invisible to transcript analysis:

| Audio-Native Dimension | What to Listen For |
|---|---|
| Interruption recovery naturalness | Does resumed audio sound like a natural continuation or an awkward restart? |
| Host differentiation over time | Do distinct voices remain distinguishable at the 5-minute and 10-minute marks? |
| Prosodic appropriateness | Is emphasis placed on the right words? Does delivery reflect comprehension? |
| Conversational latency feel | After a user question, does the answer feel responsive or pre-recorded? |
| Topic transition smoothness | Do content-type transitions feel like a coherent conversation or a stitched content dump? |
| Energy arc | Does the audio maintain engagement across a long session, or does energy deflate? |

**Visual dimensions:**
- Layout validity, taxonomic accuracy, and concept coverage
- Transcript-audio sync timing (offset measured in seconds, not subjectively)

**Generative image dimensions:**
- Prompt adherence, compositional coherence, and artifact rate

---

### Privacy Evaluation — Two Separate Layers

For any product that ingests personal communications (email, messages, calendar, documents containing personal data), privacy evaluation requires two independent evaluators. Running only one of these is an incomplete evaluation.

**Layer 1 — Hard-Pattern PII Scorer (rule-based)**
Deterministic regex patterns for: account numbers, passwords, phone numbers in signature context, email addresses in signature context, financial amounts above defined thresholds in email context. This evaluator is fast and precise but limited — it catches structured PII only.

**Layer 2 — Contextual Privacy Scorer (LLM-based)**
Evaluates whether content that is *not* structured PII is nonetheless inappropriate to surface in the product's output context. Examples of what regex cannot catch: a medical appointment read aloud on a commute; a salary negotiation email synthesized into a morning briefing; a strained professional relationship discussed in podcast format; a legal dispute surfaced as a news item.

The contextual scorer scores for three handling options:
- **Summarize abstract:** Surface the category, not the content ("You have a message about a health appointment")
- **Skip entirely:** Leave it for the user to review privately
- **Surface with consent:** Prompt the user before including borderline content

Both layers must pass before a product ingesting personal communications can be recommended for any ramp.

---

## The Nine-Stage Pipeline Reference

All reports in this directory map failures to the pipeline stage where they originate. Upstream fixes are always prioritized because they resolve downstream failures simultaneously. Evaluators trace every failure tag to its origin stage before recommending a fix surface.

```
Stage 1 — Ingestion:     Parse and extract content from all source types
Stage 2 — Normalization: Chunk, clean, deduplicate, rank by relevance
Stage 3 — Indexing:      Store processed content in vector store
Stage 4 — Retrieval:     Find relevant content for the current request
Stage 5 — Reasoning:     Assemble context; resolve novelty and coverage state
Stage 6 — Generation:    Generate output script or response
Stage 7 — Synthesis:     Convert to output modality (TTS, render, encode)
Stage 8 — Guardrails:    PII detection; content filtering; safety screening
Stage 9 — Delivery:      Stream or serve output; handle interaction state
```

---

## Supplementary Sections

Reports on architecturally complex products may include the following supplementary sections beyond the five core contracts. These are not optional extras — for the right product, they are essential. The Huxe v3 report is the reference implementation for all of them.

| Section | When to Include | Template Reference |
|---|---|---|
| **A Note on Evidence Provenance** | Always — required for Pilot Protocol reports; recommended for all reports | Huxe v3, opening section |
| **Product Understanding** | Always — includes feature table, competitive distinction, multimodal profile, and nine-stage pipeline mapped to the product | Huxe v3, Section 1 |
| **Judge Panel with Multi-Rater Protocol** | Always — names all four judges, their jurisdiction, adjudication process, and kappa targets | Huxe v3, Section 2 |
| **Evaluation Brief** | Always — completed T-01, formatted inline, with all thresholds set before any evaluation was run | Huxe v3, Section 3 |
| **Surface Mapping** | Always — maps the full pipeline to failure surfaces; identifies the top 5 highest-risk surfaces | Huxe v3, Section 4 |
| **Error Analysis and Failure Taxonomy** | Always — open coding results, failure tags, causal chains, and counts by junction | Huxe v3, Section 5 |
| **Evaluator Designs** | Always — one evaluator design per contract scored; kappa estimates with evidence labels | Huxe v3, Section 6 |
| **Audio-Native Evaluation** | Required for any audio-first or audio-primary product | Huxe v3, Section 7 |
| **Five Drifts Analysis** | Recommended — input, ingestion, model, judge, and consumption drift risks | Huxe v3, Section 9 |
| **Prioritized Backlog** | Recommended — T-17 formula applied; causal chains documented | Huxe v3, Section 10 |
| **Driver Analysis** | Required when any contract fails — structured root-cause analysis per T-13 | Huxe v3, Section 11 |
| **Decision and Recommendations** | Always — Ship / Ramp / Hold / Rollback with reversal conditions pre-committed | Huxe v3, Section 12 |
| **Maturity Assessment** | Recommended — five-level maturity model; current level and 12-week target | Huxe v3, Section 13 |
| **Key Takeaways** | Always — 3–5 numbered findings in plain language; no jargon | Huxe v3, Section 14 |
| **Evidence Provenance Index** | Required for Pilot Protocol reports — table mapping every section to its evidence labels | Huxe v3, Appendix |

---

## Categories Explained

| Category | What It Means for Evaluation |
|---|---|
| **Document-to-audio AI** | Primary inputs are user-selected documents (closed-world sources). Primary focus: Ingestion Fidelity (Contract 1) and Audio Quality (Contract 5). Faithfulness is the critical downstream contract — ingestion failures cascade directly into audio output. Source material is known, bounded, and user-controlled. |
| **Personal intelligence / ambient AI** | Primary inputs are personal communications, live data, and open-world feeds — email threads, calendar entries, news, social media. Source material is open-world, highly variable, personally sensitive, and constantly changing. Evaluation requires: email thread integrity, temporal accuracy, tense fidelity, hard-pattern PII detection, and a separate contextual privacy scorer. Standard source-grounding checks are necessary but not sufficient. |
| **AI video generation** | Primary focus: Cross-Modal Consistency (Contract 4) between script/prompt and visual output, and Output Quality (Contract 5) for both audio and visual modalities. |
| **Enterprise AI video** | Same as AI video generation, with additional emphasis on Faithfulness (Contract 2) where source documents drive generated content. Enterprise use cases typically require stricter named-entity accuracy. |
| **Async video + AI summary** | Dual evaluation surface: video output quality and text summary faithfulness. Contract 2 (Faithfulness) and Contract 4 (Cross-Modal Consistency) are the primary contracts. Summary accuracy against the video transcript is the central faithfulness test. |
| **Multimodal audio/video editing** | Focus on Contract 5 (Output Quality) for both audio and visual, and Contract 4 (Cross-Modal Consistency) for transcript-to-edit fidelity. The primary failure mode is edit operations that contradict the transcript or introduce audio artifacts at edit boundaries. |
| **Generative image AI** | Primary focus: Contract 5 (Output Quality) for visual output — prompt adherence, compositional coherence, and artifact rate. Contract 3 (Factuality) applies where generated images assert real-world content (maps, data visualizations, charts, named entities rendered visually). |

---

## Report Format and Length

Reports in this directory are published as **single integrated markdown documents**, not split across multiple contract files. The integrated format is preferred because:

- The most important findings in multimodal AI evaluation are causal chains that span multiple contracts — a thread collapse in Contract 1 causes a faithfulness failure in Contract 2. A split-file structure obscures these chains.
- A reader following a causal chain should not have to navigate between files to trace it from origin to fix.
- The supplementary sections (driver analysis, backlog, maturity) are integrative by nature — they draw from all five contracts simultaneously.

**Minimum sections for a published report:** Evidence Provenance note + Executive Summary + Score Summary Block + Zero-Tolerance Summary Block + all applicable contracts + Decision and Recommendations + Key Takeaways.

**Typical report length:** 3,000–8,000 words depending on product complexity and protocol stage. Pilot Protocol reports are typically longer because they must document their reasoning in place of empirical data.

---

## Failure Taxonomy — Standard Tags

All reports use these standard failure tags for consistency across the evaluation index. Product-specific tags are permitted and must follow the `layer.subtype.failure_mode` naming convention.

```
INGESTION LAYER
  ingestion.[type].dropped_caption
  ingestion.[type].layout_scramble
  ingestion.ocr.scanned_drop
  ingestion.ocr.handwriting
  ingestion.asr.term_miss
  ingestion.asr.silence_hallucination
  ingestion.email.thread_collapse        ← personal intelligence products
  ingestion.email.html_garble            ← personal intelligence products
  ingestion.calendar.attendee_drop       ← personal intelligence products
  ingestion.calendar.timezone_error      ← personal intelligence products

RETRIEVAL + GROUNDING
  retrieval.modality_bias
  retrieval.visual_chunk_dropped
  retrieval.email_ranking_noise          ← personal intelligence products
  retrieval.dedup_failure                ← live-feed products
  grounding.faithfulness_break
  grounding.speaker_attribution
  grounding.cross_source_merge
  grounding.tense_collapse               ← live-data products
  grounding.calendar_invented            ← personal intelligence products

GENERATION
  generation.fabricated_quote
  generation.invented_statistic
  generation.gap_fill                    ← thin-context products

CROSS-MODAL
  cross_modal.output_mismatch
  cross_modal.speaker_drift
  cross_modal.transcript_content_mismatch
  cross_modal.transcript_sync_lag
  cross_modal.interruption_repeat        ← interactive audio products

OUTPUT SYNTHESIS
  output.audio.mispronunciation
  output.audio.prosody_flat
  output.audio.script_drift
  output.audio.interruption_recovery_lag ← interactive audio products
  output.audio.host_convergence          ← dual-host audio products
  output.audio.energy_deflation          ← long-form audio products
  output.audio.topic_seam                ← multi-source audio products
  output.audio.delivery_drop
  output.visual.layout_overlap
  output.visual.taxonomic_error
  output.visual.concept_gap

SAFETY
  safety.pii_hard_pattern
  safety.pii_contextual_leakage          ← personal intelligence products
  safety.contact_detail_exposure
  safety.copyright_reproduction
```

---

## The Priority Formula

All backlog items in every report are scored using the same formula so that prioritization decisions are consistent and traceable across products.

**Priority Score = (S × F × C × B × U) ÷ TTL**

| Symbol | Dimension | Scale |
|---|---|---|
| S | Severity | High = 3 · Medium = 2 · Low = 1 |
| F | Frequency | Express as decimal: 15% = 0.15 |
| C | Confidence | High = 3 · Medium = 2 · Low = 1 |
| TTL | Time to Live | Actual days to deploy |
| B | Blast Radius | Count of downstream tags resolved by this fix |
| U | Upstream-ness | Ingestion = 5 · Retrieval = 4 · Generation = 3 · Synthesis = 2 · Delivery = 1 |

Zero-tolerance failure tags override the formula and route to rank #1 regardless of score.

---

## Methodology

### How We Evaluate

Each product is evaluated against the five quality contracts using the evaluator rubrics defined in T-05 through T-09. Where a contract does not apply to the product's modality profile, it is marked N/A with an explanation.

Evaluations follow this structured protocol:

1. The evaluation brief (T-01) is completed and all thresholds are set **before any evaluation is run** — thresholds set after seeing scores anchor to what's achievable, not what users need
2. A source input set is prepared across source types relevant to the product
3. The nine-stage pipeline is mapped to the product's actual architecture
4. Surfaces are risk-ranked and the top failure surfaces identified
5. Error analysis produces the failure taxonomy and causal chains
6. Evaluators are designed per contract, with kappa targets stated before deployment
7. Outputs are scored against the five contracts
8. Results are reported with evidence labels; zero-tolerance events are surfaced first
9. A prioritized backlog is produced using the Priority Formula
10. A Ship / Ramp / Hold / Rollback decision is made with pre-committed reversal conditions

### What We Do Not Do

- Benchmark products against each other — each product is evaluated against the framework contracts, not against other products in this index
- Test unreleased features or private beta functionality
- Accept vendor access, credits, or briefings in exchange for coverage
- Publish partial evaluations — a report is filed when all applicable contracts have been addressed
- Treat simulation-derived scores as empirical findings — the protocol stage label and evidence provenance system exist precisely to prevent this

---

## Requesting an Evaluation

To nominate a multimodal AI product for evaluation, open a GitHub Issue with the label `evaluation-request` and include:

- Product name and URL
- Proposed category (from the Categories Explained table above, or propose a new one with justification)
- The primary input and output modalities
- Whether the product ingests personal communications (email, calendar, messages)
- Why this product is relevant to the community using this framework

Priority is given to products that are widely used, represent a distinct modality profile not yet covered, or where the community has identified a specific evaluation gap.

---

## Disclosure

All evaluations are conducted independently using publicly available product tiers. No evaluation has been sponsored by, commissioned by, or shared with any product vendor prior to publication. Scores reflect the product's performance at the time of evaluation — multimodal AI products update frequently, and a report's evaluation date is the boundary of its claims.

Vendors who believe a finding is factually incorrect may open a GitHub Issue with the label `vendor-dispute` and provide specific evidence. Disputes will be reviewed and, where warranted, corrections will be published as a new report version with a clear changelog entry.

---


> The value of a consistent evaluation framework is not that every product gets the same report — it is that every product gets held to the same standard. The framework bends to fit the product's architecture. The quality contracts do not.

> The value of a consistent evaluation framework is that it makes comparison honest — not by comparing products to each other, but by holding every product to the same standard. These reports are that standard applied.

