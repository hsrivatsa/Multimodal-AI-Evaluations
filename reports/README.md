# Evaluation Reports
### Applying the Multimodal AI Evaluation Framework to Real Products in the Wild

This directory contains independent evaluation reports for multimodal AI products assessed against the five quality contracts defined in this framework — Ingestion Fidelity, Faithfulness, Factuality, Cross-Modal Consistency, and Output Quality. Each report applies the same structured methodology, the same rubrics, and the same thresholds to every product evaluated. The goal is a consistent, evidence-backed view of how real products perform against a common standard — not a ranking, not a review, and not a vendor comparison.

These reports are independent. No product vendor has sponsored, reviewed, or approved any evaluation before publication.

---

## Product Evaluation Index

| Product | Category | Report | Status |
|---|---|---|---|
| **Huxe** | Document-to-audio AI | [View Report →](./huxe/) | 🔜 Coming Soon |
| **Google NotebookLM** | Document-to-audio AI | [View Report →](./google-notebooklm/) | 🔜 Coming Soon |
| **HeyGen** | AI video generation | [View Report →](./heygen/) | 🔜 Coming Soon |
| **Synthesia** | Enterprise AI video | [View Report →](./synthesia/) | 🔜 Coming Soon |
| **Loom AI** | Async video + AI summary | [View Report →](./loom-ai/) | 🔜 Coming Soon |
| **Descript** | Multimodal audio/video editing | [View Report →](./descript/) | 🔜 Coming Soon |
| **Adobe Firefly** | Generative image AI | [View Report →](./adobe-firefly/) | 🔜 Coming Soon |

---

## What Each Report Covers

Every evaluation report in this directory follows the same structure. A report that skips a contract is a report with a gap — and the gap is clearly marked.

### Contract 1 — Ingestion Fidelity
How faithfully does the product extract content from uploaded sources? This covers document parsing, OCR on scanned inputs, ASR on audio, caption and figure retention, and reading-order preservation. For document-to-audio products, this is the contract that determines everything downstream.

### Contract 2 — Faithfulness
Are the product's output claims traceable to the source material it was given? This is not a factuality check — it is a source-grounding check. A product can be faithful to bad sources. A product can also fabricate claims that happen to be factually correct. Faithfulness measures the link between output and source, not output and world.

### Contract 3 — Factuality
Are the product's verifiable output claims correct about the world? Named entities, dates, statistics, and attributions are the primary targets. This contract is evaluated independently of faithfulness.

### Contract 4 — Cross-Modal Consistency
When a product produces output across more than one modality — audio narration alongside a visual summary, for example — do those modalities tell the same story? A central contradiction between modalities is a zero-tolerance failure regardless of how well each modality performs independently.

### Contract 5 — Output Quality
How good is the output in each modality on its own terms? For audio: voice naturalness, pronunciation, prosody, glitch rate, and script alignment. For visual: layout validity, taxonomic accuracy, and concept coverage. For generative image: prompt adherence, compositional coherence, and artifact rate.

---

## How We Evaluate

### Methodology

Each product is evaluated against the same five contracts using the evaluator rubrics defined in T-05 through T-09 of this framework. Where a contract does not apply to a product's modality profile — for example, Cross-Modal Consistency for a single-modality product — it is marked N/A with an explanation.

Evaluations follow a structured test protocol:

1. A defined set of source inputs is prepared across source types — clean documents, scanned documents, multi-source combinations, and audio where applicable
2. Each product is run against the input set under controlled conditions
3. Outputs are scored against the five contracts using the framework rubrics
4. Results are reported at the contract level, with per-source-type breakdowns where sample size permits
5. Zero-tolerance events are reported separately and explicitly — they are never buried in aggregate scores

### What We Do Not Do

- We do not benchmark products against each other — each product is evaluated against the framework contracts, not against other products in this index
- We do not test unreleased features or private beta functionality
- We do not accept vendor access, credits, or briefings in exchange for coverage
- We do not publish partial evaluations — a report is filed when all applicable contracts have been scored

### Sample Sizes and Confidence

Every report states the input set size, source type distribution, and evaluation date. Where sample sizes are too small to support a reliable contract score, that limitation is stated explicitly rather than hidden behind an aggregate number. A score based on 8 inputs is not the same as a score based of 80 inputs, and the reports say so.

---

## Categories Explained

| Category | What It Means for Evaluation |
|---|---|
| **Document-to-audio AI** | Primary focus on Ingestion Fidelity (Contract 1) and Audio Quality (Contract 5). Faithfulness is the critical downstream contract — ingestion failures cascade directly into audio output. |
| **AI video generation** | Primary focus on Cross-Modal Consistency (Contract 4) between script/prompt and visual output, and Output Quality (Contract 5) for both audio and visual modalities. |
| **Enterprise AI video** | Same as AI video generation, with additional emphasis on Faithfulness (Contract 2) where source documents drive generated content. |
| **Async video + AI summary** | Dual evaluation surface: video output quality and text summary faithfulness. Contract 2 (Faithfulness) and Contract 4 (Cross-Modal Consistency) are the primary contracts. |
| **Multimodal audio/video editing** | Focus on Contract 5 (Output Quality) for both audio and visual, and Contract 4 (Cross-Modal Consistency) for transcript-to-edit fidelity. |
| **Generative image AI** | Primary focus on Contract 5 (Output Quality) for visual output. Contract 3 (Factuality) applies where generated images assert real-world content. |

---

## Reading a Report

Each product report is structured as follows:

```
Product Name
├── README.md          — Product overview, evaluation scope, and score summary
├── contract-1.md      — Ingestion Fidelity findings
├── contract-2.md      — Faithfulness findings
├── contract-3.md      — Factuality findings
├── contract-4.md      — Cross-Modal Consistency findings
├── contract-5.md      — Output Quality findings
└── zero-tolerance.md  — Any zero-tolerance events detected, documented separately
```

Start with the `README.md` for the product — it contains the score summary table and flags any zero-tolerance events at the top, before the contract-level detail. A zero-tolerance event is never buried.

---

## Score Summary Format

Every report's README.md opens with a score summary in this format:

| Contract | Score | Threshold | Status | Zero-Tolerance Events |
|---|---|---|---|---|
| Ingestion Fidelity | | ≥ defined bar | | |
| Faithfulness | | ≥ defined bar | | |
| Factuality | | ≥ defined bar | | |
| Cross-Modal Consistency | | ≤ defined bar | | |
| Output Quality | | ≥ defined bar | | |

Scores are reported as measured values against the reference quality bars from T-02. Where a contract is not applicable to the product, the score cell reads `N/A` with a one-line explanation.

---

## Requesting an Evaluation

If you would like to nominate a multimodal AI product for evaluation, open a GitHub Issue with the label `evaluation-request` and include:

- Product name and URL
- Product category (use the categories defined above, or propose a new one)
- The primary modalities the product works with (inputs and outputs)
- Why this product is relevant to the community using this framework

Nominations do not guarantee evaluation. Priority is given to products that are widely used, represent a distinct modality profile not yet covered, or where the community has identified a specific gap in the current index.

---

## Disclosure

All evaluations in this directory are conducted independently using publicly available product tiers. No evaluation has been sponsored by, commissioned by, or shared with any product vendor prior to publication. Scores reflect the product's performance at the time of evaluation — multimodal AI products update frequently, and a report's evaluation date is the boundary of its claims.

If a vendor believes a finding is factually incorrect, they may open a GitHub Issue with the label `vendor-dispute` and provide specific evidence. Disputes will be reviewed and, where warranted, corrections will be published as a new report version with a clear changelog entry.

---

> The value of a consistent evaluation framework is that it makes comparison honest — not by comparing products to each other, but by holding every product to the same standard. These reports are that standard applied.

