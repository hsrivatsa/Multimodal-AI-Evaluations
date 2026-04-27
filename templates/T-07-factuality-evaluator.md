# T-07 — Factuality Evaluator
**Contract 3 | Multimodal AI Feature Evaluation**

> **Purpose:** Production-ready LLM judge prompt for Contract 3 — Factuality (output ↔ world).  
> **When to use:** After completing error analysis and human labeling. Validate against your Judge Panel before deploying.  
> **Key rule:** This is a separate contract from Faithfulness (T-06). Do not use the Faithfulness evaluator for this purpose. A claim can be faithful to the sources but still factually wrong about the world.

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

Evaluates whether a claim is factually correct about the real world — independent of source documents.

> ⚠️ Evaluate **one claim per call**.  
> ⚠️ This evaluator uses world knowledge, not source documents. The distinction from T-06 is intentional and critical.  
> ⚠️ High-confidence "incorrect" labels must trigger an automatic escalation flag.

---

## Contract 3 vs. Contract 2 — Critical Distinction

| Dimension | Faithfulness (T-06) | Factuality (T-07) |
|---|---|---|
| Question asked | Is this claim in the sources? | Is this claim true about the world? |
| Evidence used | Source documents only | World knowledge only |
| A claim true in sources but wrong about world | Supported | Incorrect |
| A claim correct about world but absent from sources | Unsupported | Correct |
| Both evaluators must pass for | High-stakes output | High-stakes output |

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
FACTUALITY JUDGE PROMPT v___ — [Your Product Name]

You evaluate whether a single verifiable claim from a
generated output is factually correct about the real world.

IMPORTANT: This is NOT a faithfulness check. You are NOT
checking whether the claim appears in the source documents.
You are checking whether the claim is true, using your
world knowledge.

You receive:
  1. A single claim from the output
  2. The domain context (e.g., "clinical research summary")

Evaluate one claim only.

Return ONLY valid JSON. No preamble, no markdown fences.

{
  "reasoning": "<step-by-step: is this verifiable and correct?>",
  "confidence": "high" | "medium" | "low",
  "label": "correct" | "incorrect" | "unverifiable"
}

DEFINITIONS:
  "correct"      = factually accurate against world knowledge
  "incorrect"    = contradicts established world knowledge
  "unverifiable" = cannot be confirmed — applies to internal
                   data, predictions, opinions, very recent
                   events, or uncertain domain claims

STRICT RULES:
  ▷ Named entities are highest priority: dates, titles,
    people, places, institutions, published statistics.
  ▷ Speculative or forward-looking claims = "unverifiable."
  ▷ When uncertain, prefer "unverifiable" over guessing.
  ▷ High-confidence "incorrect" = automatic escalation flag.

CALIBRATION EXAMPLES:
[REQUIRED — Add 3–5 examples before deploying:
 • One clear "correct" named fact
 • One high-confidence "incorrect"
 • One "unverifiable" prediction or internal data point]

Claim: "{claim_text}"
Domain context: "{domain}"
```

---

## Calibration Examples (Fill Before Deploying)

### Example 1 — Clear Correct Named Fact
> **Label:** correct  
> **Confidence:** high  
> **Claim:**  
> **Domain context:**  
> **Reasoning:**  

### Example 2 — High-Confidence Incorrect
> **Label:** incorrect  
> **Confidence:** high  
> **Claim:**  
> **Domain context:**  
> **What the correct fact is:**  
> **Reasoning:**  

### Example 3 — Unverifiable (Prediction / Internal Data)
> **Label:** unverifiable  
> **Confidence:** high  
> **Claim:**  
> **Domain context:**  
> **Why unverifiable:**  
> **Reasoning:**  

### Example 4 — [Product-Specific Domain Fact]
> **Label:**  
> **Confidence:**  
> **Claim:**  
> **Domain context:**  
> **Reasoning:**  

### Example 5 — [Product-Specific Domain Fact]
> **Label:**  
> **Confidence:**  
> **Claim:**  
> **Domain context:**  
> **Reasoning:**  

---

## Domain Zero-Tolerance Events

Name the specific factual failure in your domain that triggers immediate rollback. Examples: incorrect drug dosage in a medical product; wrong regulatory figure in a compliance product; incorrect jurisdiction in a legal product.

| Domain | Zero-Tolerance Failure Type | Action |
|---|---|---|
| [Your domain] | | Immediate rollback |
| [Your domain] | | Immediate rollback |

---

## Escalation Protocol

| Condition | Action | Owner |
|---|---|---|
| High-confidence "incorrect" on any named entity | Automatic escalation flag | Content Judge |
| High-confidence "incorrect" on domain zero-tolerance claim | Immediate rollback | Product Lead |
| "Incorrect" rate > 0 on regression set | CI gate block | Engineering Lead |

---

## Label Distribution Tracking

Track label distribution over time. A drift toward "incorrect" or a sudden spike in "unverifiable" labels signals a model, prompt, or domain coverage regression.

| Date | Run ID | Correct % | Incorrect % | Unverifiable % | Kappa | Notes |
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

> This prompt is a starting point. Calibration examples and domain zero-tolerance events must be defined before deployment. Track kappa trend over time — a drop of more than 0.10 signals your judge model was updated.
