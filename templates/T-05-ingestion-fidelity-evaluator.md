# T-05 — Ingestion Fidelity Evaluator
**Contract 1 | Multimodal AI Feature Evaluation**

> **Purpose:** Production-ready LLM judge prompt for Contract 1 — Ingestion Fidelity.  
> **When to use:** After completing error analysis and human labeling. Validate against your Judge Panel before deploying.  
> **Key rule:** An evaluator is only as good as its agreement with your Judge Panel. Measure Cohen's Kappa before deploying anything.

---

## Document Header

| Field | Value |
|---|---|
| Version | v_____ |
| Last calibrated | |
| Kappa on validation set | |
| Minimum kappa for CI gate | 0.85 |
| Minimum kappa for monitoring | 0.75 |

---

## Evaluator Overview

Evaluates whether the ingestion pipeline faithfully extracted content from the uploaded source.

> ⚠️ Requires source document images — do not run on extracted text alone.

**Why ingestion fidelity requires stricter kappa (≥ 0.85):** Ingestion failures cascade through the entire pipeline — a miscalibrated ingestion evaluator produces misleading scores across all downstream contracts simultaneously.

---

## Kappa Requirements (All Evaluators Reference)

| Evaluator | CI Gate (required) | Monitoring (minimum) | Recalibration |
|---|---|---|---|
| T-05 Ingestion Fidelity | kappa ≥ 0.85 | kappa ≥ 0.75 | Quarterly + after any parser update |
| T-06 Faithfulness | kappa ≥ 0.80 | kappa ≥ 0.70 | Monthly |
| T-07 Factuality | kappa ≥ 0.80 | kappa ≥ 0.70 | Monthly |
| T-08 Audio Quality | kappa ≥ 0.80 | kappa ≥ 0.70 | Monthly + after any TTS update |
| T-09 Cross-Modal Consistency | kappa ≥ 0.80 | kappa ≥ 0.70 | Monthly |

---

## Universal Rules — Apply to All Five Evaluators

| Rule | Detail |
|---|---|
| Different model family for judging | Never use the same model family to judge as to generate — same-family judges produce self-enhancement bias |
| Binary labels only | Use pass/fail for most evaluators — forces precision in your rubric and makes kappa calculation clean |
| Calibration examples from your product | Add 3–5 examples from your own product's actual failures — not generic examples |
| Sensitivity test | Plant 10 known-bad outputs — evaluator must catch all 10 before deployment |
| Slice analysis | Report kappa separately per content type — overall kappa can hide per-modality blind spots |

---

## Deployment Checklist

| Step | Task | Status |
|---|---|---|
| 1 | Human labels collected from the relevant Judge (100–150 outputs) | ☐ |
| 2 | Data split: 60% build / 20% validate / 20% holdout (holdout untouched) | ☐ |
| 3 | Calibration examples added from your own product's failures | ☐ |
| 4 | Cohen's Kappa measured on validation split — documented and above threshold | ☐ |
| 5 | Slice analysis run: kappa reported separately per content type | ☐ |
| 6 | Sensitivity test passed: 10 known-bad outputs caught at 100% | ☐ |
| 7 | Prompt version tagged and frozen — no "latest" model pins | ☐ |
| 8 | Monthly recalibration scheduled on the governance calendar | ☐ |

---

## Judge Prompt

```
INGESTION FIDELITY JUDGE PROMPT v___ — [Your Product Name]

You evaluate whether the ingestion pipeline faithfully
extracted the content from an uploaded source document.

You receive:
  1. The original document (as image scans of each page)
  2. The extracted text produced by the parser

Return ONLY valid JSON. No preamble, no markdown fences.

{
  "reasoning": "<step-by-step: what is in the original
                 that is missing or wrong in the extraction?>",
  "missed_elements": ["<list each absent caption, table,
                        heading, or figure>"],
  "distorted_elements": ["<list each garbled, mis-ordered,
                           or truncated element>"],
  "label": "pass" | "fail"
}

DEFINITIONS:
  "pass" = the extracted text preserves all content a human
           reader would consider essential from the original.
           Minor whitespace differences are acceptable.

  "fail" = ANY of the following are true:
    ▷ A figure caption is absent from the extraction
    ▷ A table is missing, truncated, or its columns merged
    ▷ Reading order is wrong (e.g., columns read across
      instead of down in a multi-column layout)
    ▷ Substantive text is absent or garbled beyond OCR noise
      (> 5% character error rate on any single page)
    ▷ A heading is absent that changes the perceived
      structure or section hierarchy

STRICT RULES:
  ▷ Do NOT infer what the text "probably" said.
  ▷ Compare only what is visible in the page scans to
    what appears in the extracted text.
  ▷ When in doubt, label "fail."

CALIBRATION EXAMPLES:
[REQUIRED — Add 3–5 examples before deploying:
 • One clean pass
 • One caption drop fail
 • One layout scramble fail
 • One OCR fail on scanned content]

Original document (page scans): {page_images}
Extracted text: {extracted_text}
```

---

## Calibration Examples (Fill Before Deploying)

### Example 1 — Clean Pass
> **Label:** pass  
> **Input summary:**  
> **Reasoning:**  
> **Missed elements:** none  
> **Distorted elements:** none  

### Example 2 — Caption Drop Fail
> **Label:** fail  
> **Input summary:**  
> **Reasoning:**  
> **Missed elements:**  
> **Distorted elements:**  

### Example 3 — Layout Scramble Fail
> **Label:** fail  
> **Input summary:**  
> **Reasoning:**  
> **Missed elements:**  
> **Distorted elements:**  

### Example 4 — OCR Fail on Scanned Content
> **Label:** fail  
> **Input summary:**  
> **Reasoning:**  
> **Missed elements:**  
> **Distorted elements:**  

### Example 5 — [Product-Specific]
> **Label:**  
> **Input summary:**  
> **Reasoning:**  
> **Missed elements:**  
> **Distorted elements:**  

---

## Calibration History

| Date | Kappa | Labeled By | Notes |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

---

> This prompt is a starting point. Calibration examples and entity references must be added before deployment. Track kappa trend over time — a drop of more than 0.10 signals your judge model was updated.
