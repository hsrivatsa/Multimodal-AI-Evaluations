# T-08 — Audio Quality Evaluator
**Contract 5 (Audio) | Multimodal AI Feature Evaluation**

> **Purpose:** Production-ready LLM judge prompt for Contract 5 — Output Quality (Audio).  
> **When to use:** After completing error analysis and human labeling. Validate against your Audio Judge before deploying.  
> **Key rule:** Score each dimension independently — do not average. A single dimension fail is a contract fail.

---

## Document Header

| Field | Value |
|---|---|
| Version | v_____ |
| Last calibrated | |
| Kappa on validation set | |
| Minimum kappa for CI gate | 0.80 |
| Minimum kappa for monitoring | 0.70 |
| Recalibration schedule | Monthly + after any TTS update |

---

## Evaluator Overview

Evaluates a 30-second audio segment on four independent dimensions against an approved script.

> ⚠️ Evaluate each dimension **independently** — do not average scores across dimensions.  
> ⚠️ A single dimension fail = contract fail for that segment.  
> ⚠️ The entity reference list **must** be populated before deployment — pronunciation accuracy against domain-specific terms is the primary failure mode for TTS in specialized products.

---

## The Four Dimensions

| Dimension | What It Measures | Fail Condition |
|---|---|---|
| Script Fidelity | Whether the audio matches the approved script word-for-word | ≥ 1 content word omitted, replaced, or added |
| Pronunciation | Correct rendering of entities, technical terms, product names, person names | Any entity on the reference list mispronounced or rendered ambiguously |
| Prosody | Natural emphasis on key findings, headlines, and named conclusions | Emphatic content delivered with uniformly flat, monotone prosody |
| Glitch-Free | Absence of audible artifacts, clicks, dropouts, distortion, or long unscripted pauses | Any artifact, click, dropout, distortion, or unscripted pause > 1.5 seconds |

---

## Deployment Checklist

| Step | Task | Status |
|---|---|---|
| 1 | Human labels collected from the Audio Judge (100–150 segments) | ☐ |
| 2 | Data split: 60% build / 20% validate / 20% holdout (holdout untouched) | ☐ |
| 3 | Calibration examples added from your own product's failures | ☐ |
| 4 | Entity reference list populated with all domain-specific terms | ☐ |
| 5 | Cohen's Kappa measured on validation split — documented and above threshold | ☐ |
| 6 | Slice analysis run: kappa reported separately per dimension | ☐ |
| 7 | Sensitivity test passed: 10 known-bad segments caught at 100% | ☐ |
| 8 | Prompt version tagged and frozen — no "latest" model pins | ☐ |
| 9 | Recalibration scheduled monthly + after every TTS model update | ☐ |

---

## Judge Prompt

```
AUDIO QUALITY JUDGE PROMPT v___ — [Your Product Name]

You evaluate a 30-second audio segment against an approved
script, scoring four dimensions independently.

You receive:
  1. An audio clip (base64-encoded)
  2. The approved script the audio should perform

Score each dimension independently as binary pass/fail.

Return ONLY valid JSON. No preamble, no markdown fences.

{
  "script_fidelity": {
    "label": "pass" | "fail",
    "reasoning": "<what was omitted, replaced, or added?>"
  },
  "pronunciation": {
    "label": "pass" | "fail",
    "reasoning": "<which term was mispronounced, and how?>"
  },
  "prosody": {
    "label": "pass" | "fail",
    "reasoning": "<what content had wrong emphasis?>"
  },
  "glitch_free": {
    "label": "pass" | "fail",
    "reasoning": "<describe any artifact or pause>"
  }
}

FAIL CRITERIA — each dimension is independent:

  script_fidelity: FAIL if ≥ 1 content word is omitted,
    replaced, or added vs. the approved script.

  pronunciation: FAIL if any entity, technical term, product
    name, or person's name in the entity reference list is
    mispronounced or rendered ambiguously.

  prosody: FAIL if emphatic content (key findings, headlines,
    named conclusions) is delivered with uniformly flat,
    monotone prosody.

  glitch_free: FAIL if any audible artifact, click, dropout,
    distortion, or unscripted pause > 1.5 seconds is present.

ENTITY REFERENCE:
[REQUIRED — Add your product's domain-specific terms, person
 names, product names, and acronyms with expected pronunciation]

Audio clip: {audio_base64}
Approved script: {script_text}
```

---

## Entity Reference List (Fill Before Deploying)

This list must be populated before the evaluator is deployed. Every term added here becomes part of the pronunciation contract.

| Term / Entity | Expected Pronunciation | Category | Added Date |
|---|---|---|---|
| | | Technical term | |
| | | Product name | |
| | | Person name | |
| | | Acronym | |
| | | Institution | |
| | | [Other] | |

---

## Calibration Examples (Fill Before Deploying)

### Example 1 — All Dimensions Pass
> **Script fidelity:** pass  
> **Pronunciation:** pass  
> **Prosody:** pass  
> **Glitch-free:** pass  
> **Segment description:**  
> **Reasoning:**  

### Example 2 — Script Fidelity Fail
> **Script fidelity:** fail  
> **What was omitted / replaced / added:**  
> **Other dimensions:**  
> **Reasoning:**  

### Example 3 — Pronunciation Fail
> **Pronunciation:** fail  
> **Term mispronounced:**  
> **How it was rendered:**  
> **Expected rendering:**  
> **Reasoning:**  

### Example 4 — Prosody Fail
> **Prosody:** fail  
> **Content with wrong emphasis:**  
> **Reasoning:**  

### Example 5 — Glitch Fail
> **Glitch-free:** fail  
> **Artifact type:**  
> **Timestamp in segment:**  
> **Reasoning:**  

---

## Dimension Score Tracking

Track per-dimension pass rates over time. Dimension-level tracking reveals TTS model drift that overall MOS scores can mask.

| Date | Run ID | Script Fidelity Pass % | Pronunciation Pass % | Prosody Pass % | Glitch-Free Pass % | Overall Pass % | Kappa |
|---|---|---|---|---|---|---|---|
| | | | | | | | |
| | | | | | | | |
| | | | | | | | |

---

## Rollback Triggers (Audio-Specific)

| Trigger | Action |
|---|---|
| Audio MOS drops below defined threshold | Immediate investigation |
| Silence gap > 5 seconds detected in any output | Immediate investigation |
| Pronunciation pass rate drops > 2% from baseline | Hold; update pronunciation lexicon before continuing |
| Glitch rate exceeds defined per-10-min threshold | Immediate investigation |

---

## Calibration History

| Date | Kappa | Labeled By | TTS Version at Time of Calibration | Notes |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

---

> This prompt is a starting point. The entity reference list and calibration examples must be completed before deployment. Recalibrate after every TTS model update — TTS providers update models silently and pronunciation behavior can change without notice.
