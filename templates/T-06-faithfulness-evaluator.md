# T-06 — Faithfulness Evaluator
**Contract 2 | Multimodal AI Feature Evaluation**

> **Purpose:** Production-ready LLM judge prompt for Contract 2 — Faithfulness (output ↔ sources).  
> **When to use:** After completing error analysis and human labeling. Validate against your Judge Panel before deploying.  
> **Key rule:** An evaluator is only as good as its agreement with your Judge Panel. Measure Cohen's Kappa before deploying anything.

---

## Document Header

| Field | Value |
|---|---|
| Version | v_____ |
| Last calibrated | |
| Kappa on validation set | |
| Minimum kappa for CI gate | 0.80 |
| Minimum kappa for monitoring | 0.70 |

---

## Evaluator Overview

Evaluates whether a single output claim is traceable to the uploaded sources.

> ⚠️ Evaluate **one claim per call**.  
> ⚠️ Pass source images to the judge — it must be able to see figures.  
> ⚠️ This is a separate contract from Factuality (T-07). Do not conflate the two. A claim can be faithful (in the sources) but factually wrong, or factually correct but unsupported by the sources.

---

## Deployment Checklist

| Step | Task | Status |
|---|---|---|
| 1 | Human labels collected from the Content Judge (100–150 outputs) | ☐ |
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
FAITHFULNESS JUDGE PROMPT v___ — [Your Product Name]

You evaluate whether a single claim from a generated output
is faithful to the uploaded source documents.

You receive:
  1. Extracted text from source documents
  2. Images of figures and tables (if present in sources)
  3. One single claim from the output, with timestamp if audio

Evaluate one claim only.

Return ONLY valid JSON. No preamble, no markdown fences.

{
  "reasoning": "<step-by-step: where in the sources is
                 this claim supported, contradicted, or
                 absent?>",
  "supporting_evidence": "<direct quote or figure reference,
                           or null if unsupported>",
  "modality_of_evidence": "text" | "figure" | "table" | "none",
  "label": "supported" | "contradicted" | "unsupported"
}

DEFINITIONS:
  "supported"    = claim directly traceable to source content
  "contradicted" = source explicitly asserts the opposite
  "unsupported"  = source is silent, OR claim goes beyond
                   sources — even if factually correct

STRICT RULES:
  ▷ Do NOT use your world knowledge. Sources only.
  ▷ Treat figures and tables as evidence equal to text.
  ▷ True by world knowledge but not in sources = "unsupported."

CALIBRATION EXAMPLES:
[REQUIRED — Add 3–5 examples before deploying:
 • One "supported" from text
 • One "supported" from figure
 • One "unsupported"
 • One "contradicted"]

Sources (text + figures): {source_text_and_figures}
Claim at {timestamp}: "{claim_text}"
```

---

## Calibration Examples (Fill Before Deploying)

### Example 1 — Supported from Text
> **Label:** supported  
> **Claim:**  
> **Source excerpt:**  
> **Modality of evidence:** text  
> **Reasoning:**  

### Example 2 — Supported from Figure
> **Label:** supported  
> **Claim:**  
> **Figure reference:**  
> **Modality of evidence:** figure  
> **Reasoning:**  

### Example 3 — Unsupported
> **Label:** unsupported  
> **Claim:**  
> **Why unsupported:**  
> **Modality of evidence:** none  
> **Reasoning:**  

### Example 4 — Contradicted
> **Label:** contradicted  
> **Claim:**  
> **What the source says instead:**  
> **Modality of evidence:**  
> **Reasoning:**  

### Example 5 — [Product-Specific]
> **Label:**  
> **Claim:**  
> **Source reference:**  
> **Modality of evidence:**  
> **Reasoning:**  

---

## Zero-Tolerance Events

The following faithfulness failures trigger immediate rollback regardless of all other scores:

| Event | Action |
|---|---|
| Fabricated quote with named attribution | Immediate rollback |
| Invented citation (source does not exist) | Immediate rollback |
| [Product-specific zero-tolerance event] | Immediate rollback |

---

## Label Distribution Tracking

Track label distribution over time. A drift toward "unsupported" without a corresponding source change signals a prompt, model, or retrieval regression.

| Date | Run ID | Supported % | Contradicted % | Unsupported % | Kappa | Notes |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |

---

## Calibration History

| Date | Kappa | Labeled By | Notes |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

---

> This prompt is a starting point. Calibration examples must be added before deployment. Track kappa trend over time — a drop of more than 0.10 signals your judge model was updated.
