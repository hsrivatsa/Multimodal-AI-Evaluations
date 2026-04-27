# T-09 — Cross-Modal Consistency Evaluator
**Contract 4 | Multimodal AI Feature Evaluation**

> **Purpose:** Production-ready LLM judge prompt for Contract 4 — Cross-Modal Consistency.  
> **When to use:** After completing error analysis and human labeling. Validate against your Judge Panel before deploying.  
> **Key rule:** Any central contradiction between output modalities is a zero-tolerance rollback trigger — no exceptions, no discussion.

---

## Document Header

| Field | Value |
|---|---|
| Version | v_____ |
| Last calibrated | |
| Kappa on validation set | |
| Minimum kappa for CI gate | 0.80 |
| Minimum kappa for monitoring | 0.70 |
| Recalibration schedule | Monthly |

---

## Evaluator Overview

Evaluates whether two output modalities from the same session tell a consistent story. Operates claim-by-claim across the primary and secondary output.

> ⚠️ A **central** contradiction is a zero-tolerance rollback trigger regardless of all other scores.  
> ⚠️ Absence of a topic in one modality is **not** a contradiction — only test claims that appear in both.  
> ⚠️ In CI fast gate, this evaluator runs on a text proxy. In nightly full regression, it runs on full audio + visual output.

---

## Severity Definitions

| Severity | Definition | Action on Contradiction |
|---|---|---|
| central | Primary finding, main conclusion, headline claim | Zero-tolerance rollback trigger |
| peripheral | Supporting detail, example, secondary data point | Flagged; investigated within 24 hours |
| na | No corresponding element in secondary modality | Not a contradiction; no action |

---

## Deployment Checklist

| Step | Task | Status |
|---|---|---|
| 1 | Human labels collected from Content Judge + Visual/Audio Judge (100–150 pairs) | ☐ |
| 2 | Data split: 60% build / 20% validate / 20% holdout (holdout untouched) | ☐ |
| 3 | Calibration examples added from your own product's failures | ☐ |
| 4 | Cohen's Kappa measured on validation split — documented and above threshold | ☐ |
| 5 | Slice analysis run: kappa reported separately per modality pair | ☐ |
| 6 | Sensitivity test passed: 10 known central-contradiction cases caught at 100% | ☐ |
| 7 | Prompt version tagged and frozen — no "latest" model pins | ☐ |
| 8 | Text proxy confirmed for CI fast gate; full audio+visual confirmed for nightly | ☐ |
| 9 | Monthly recalibration scheduled on the governance calendar | ☐ |

---

## Judge Prompt

```
CROSS-MODAL CONSISTENCY JUDGE PROMPT v___ — [Your Product Name]

You evaluate whether the two output modalities from the
same session tell a consistent story.

You receive:
  1. Key claims from the primary output (e.g., audio)
  2. Structured description of the secondary output (e.g., visual)

Return ONLY valid JSON. No preamble, no markdown fences.

{
  "claim_by_claim": [
    {
      "primary_claim": "<claim from primary output>",
      "secondary_element": "<corresponding element, or 'none'>",
      "consistent": true | false,
      "severity": "central" | "peripheral" | "na",
      "reasoning": "<explain the inconsistency or consistency>"
    }
  ],
  "overall_consistent": true | false,
  "central_contradiction_present": true | false,
  "summary": "<one sentence on overall consistency>"
}

SEVERITY DEFINITIONS:
  "central"    = primary finding, main conclusion, headline claim
  "peripheral" = supporting detail, example, secondary data point
  "na"         = no corresponding element in secondary modality

CONSISTENCY RULES:
  ▷ Consistent = same claim, even if worded differently.
  ▷ Inconsistent = one asserts X, other asserts not-X, or
    assigns conflicting values to the same named entity.
  ▷ Absence of a topic in one modality is NOT a contradiction.

ZERO-TOLERANCE RULE:
  central_contradiction_present = true is an automatic
  rollback trigger regardless of all other scores.

Primary output claims: {claims_list}
Secondary output structure: {structure}
```

---

## Calibration Examples (Fill Before Deploying)

### Example 1 — Fully Consistent (Central Claims)
> **Overall consistent:** true  
> **Central contradiction present:** false  
> **Primary claim:**  
> **Secondary element:**  
> **Reasoning:**  

### Example 2 — Peripheral Inconsistency Only
> **Overall consistent:** false  
> **Central contradiction present:** false  
> **Inconsistent claim:**  
> **Severity:** peripheral  
> **Reasoning:**  
> **Action:** Flagged for investigation; no rollback  

### Example 3 — Central Contradiction (Zero-Tolerance)
> **Overall consistent:** false  
> **Central contradiction present:** true  
> **Primary claim:**  
> **Secondary element (what it asserts instead):**  
> **Severity:** central  
> **Reasoning:**  
> **Action:** Immediate rollback  

### Example 4 — Absence in One Modality (Not a Contradiction)
> **Overall consistent:** true  
> **Central contradiction present:** false  
> **Primary claim:**  
> **Secondary element:** none  
> **Severity:** na  
> **Reasoning:** Topic absent in secondary modality — absence is not contradiction  

### Example 5 — [Product-Specific]
> **Overall consistent:**  
> **Central contradiction present:**  
> **Claim pair:**  
> **Severity:**  
> **Reasoning:**  

---

## CI Gate Configuration

| Gate Mode | What Runs | Trigger |
|---|---|---|
| Fast gate (per-PR) | Text proxy of claims vs. visual structure description | Blocks merge on central_contradiction_present = true |
| Nightly full regression | Full audio transcript claims vs. full visual render | Blocks on central contradiction; flags peripheral |
| Weekly adversarial | Worst-case cross-modal inputs | Reports only; feeds backlog |

---

## Rollback Protocol

| Trigger | Who Is Notified | Time to Rollback |
|---|---|---|
| `central_contradiction_present = true` | AI Reliability Lead, Product Lead, Engineering Lead | ≤ defined SLA minutes |
| `central_contradiction_present = true` in production | Rollback owner (named in T-10) | Immediate; no discussion required |

---

## Consistency Score Tracking

| Date | Run ID | Claims Evaluated | Consistent % | Peripheral Inconsistency Count | Central Contradictions | Kappa | Action Taken |
|---|---|---|---|---|---|---|---|
| | | | | | | | |
| | | | | | | | |
| | | | | | | | |

---

## Calibration History

| Date | Kappa | Labeled By | Modality Pair Tested | Notes |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

---

> This prompt is a starting point. Calibration examples must be completed before deployment. The zero-tolerance rule for central contradictions is non-negotiable — do not soften it in your rubric. Track kappa trend over time — a drop of more than 0.10 signals your judge model was updated.
