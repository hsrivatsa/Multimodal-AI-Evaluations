# T-16 — Dataset Record
**Multimodal AI Feature Evaluation**

> **Purpose:** Versioned metadata record for every evaluation dataset, including modality coverage, taxonomy coverage, source breakdown, media blob registry, and known gaps.  
> **When to use:** Create a record when a new dataset is created or a new version is cut. Review and update quarterly.  
> **Key rule:** Never update a media blob in place — treat it as a new case. A modified blob silently changes what a regression case tests.

---

## Document Header

| Field | Value |
|---|---|
| Dataset Name | |
| Version | |
| Owner | |
| Created | |
| Last Refreshed | |
| Next Review Due | |

---

## Dataset Purpose

| Purpose | Selected? |
|---|---|
| Iteration set — prompt development | ☐ |
| Validation set — evaluator calibration | ☐ |
| Holdout set — final evaluation only | ☐ |
| Regression suite — CI and nightly | ☐ |
| Canary corpus — never refresh; fixed permanently | ☐ |
| Red-team set — adversarial testing | ☐ |

---

## Modality Coverage

| Source Type | Case Count |
|---|---|
| Single clean document | |
| Single scanned document | |
| Multi-source (3–5 sources) | |
| Multi-source (6+ sources) | |
| Audio input | |
| Video input | |
| Mixed sources | |
| Non-primary language | |
| Other: | |
| **TOTAL** | |

---

## Taxonomy Coverage

> Flag any tag with fewer than 5 cases — it is a blind spot.

| Failure Tag | Case Count | Target | Gap? |
|---|---|---|---|
| `ingestion.[type].dropped_caption` | | ≥ 5 | ☐ |
| `ingestion.[type].layout_scramble` | | ≥ 5 | ☐ |
| `ingestion.ocr.scanned_drop` | | ≥ 5 | ☐ |
| `ingestion.ocr.handwriting` | | ≥ 5 | ☐ |
| `ingestion.asr.term_miss` | | ≥ 5 | ☐ |
| `ingestion.asr.silence_hallucination` | | ≥ 5 | ☐ |
| `retrieval.modality_bias` | | ≥ 5 | ☐ |
| `retrieval.visual_chunk_dropped` | | ≥ 5 | ☐ |
| `grounding.faithfulness_break` | | ≥ 5 | ☐ |
| `grounding.speaker_attribution` | | ≥ 5 | ☐ |
| `grounding.cross_source_merge` | | ≥ 5 | ☐ |
| `generation.fabricated_quote` | | ≥ 5 | ☐ |
| `generation.invented_statistic` | | ≥ 5 | ☐ |
| `cross_modal.output_mismatch` | | ≥ 5 | ☐ |
| `cross_modal.speaker_drift` | | ≥ 5 | ☐ |
| `output.audio.mispronunciation` | | ≥ 5 | ☐ |
| `output.audio.prosody_flat` | | ≥ 5 | ☐ |
| `output.audio.script_drift` | | ≥ 5 | ☐ |
| `output.visual.layout_overlap` | | ≥ 5 | ☐ |
| `output.visual.taxonomic_error` | | ≥ 5 | ☐ |
| `output.visual.concept_gap` | | ≥ 5 | ☐ |
| `safety.pii_in_output` | | ≥ 5 | ☐ |
| `safety.copyright_reproduction` | | ≥ 5 | ☐ |
| [Product-specific tag] | | ≥ 5 | ☐ |

---

## Source Breakdown

| Source Type | Case Count | % of Total |
|---|---|---|
| Production (consented) | | |
| Red-team generated | | |
| Synthetic (validated) | | |

> **Synthetic data generation model family used:**  
> *(Must differ from the system under test to avoid circular evaluation)*

---

## Media Blob Registry

| Field | Entry |
|---|---|
| Blob storage bucket | |
| SHA-256 manifest file | |
| Retention policy | |
| PII review completed | ☐ Yes &nbsp; ☐ No &nbsp; ☐ N/A |
| PII reviewer | |
| PII review date | |

### Media Blob Index

One row per case containing audio or video content.

| Case ID | Failure Tag | Blob URI | SHA-256 Hash | Added Date | Expiry Date | Media Expired? |
|---|---|---|---|---|---|---|
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |

---

## Known Gaps

| # | Gap Description |
|---|---|
| 1 | |
| 2 | |
| 3 | |

---

## Distribution Audit

Run quarterly.

| Field | Entry |
|---|---|
| Last audit date | |
| Auditor | |
| Matches current production traffic | ☐ Yes — no refresh needed &nbsp; ☐ No — gap described below |
| Gap description | |

---

## Dataset Refresh Cadence

| Dataset Type | Minimum Cadence | Refresh Trigger |
|---|---|---|
| Iteration set | Monthly | After any major taxonomy revision |
| Validation set | Monthly | After each evaluator calibration cycle |
| Regression suite | Quarterly | When new tags appear; when coverage audit shows gaps |
| Holdout set | Semi-annually | After each major model version evaluation |
| Red-team adversarial set | Per session | After each red-team session |
| Canary corpus | Never | Fixed permanently — do not refresh |

---

## Version History

| Version | Date | Changes | Author |
|---|---|---|---|
| v1.0 | | Initial creation | |
| | | | |
| | | | |
| | | | |
| | | | |

---

> Dataset records are version-controlled artifacts. Tag each version alongside the evaluation runs that reference it. A dataset without a record is untrustworthy — you cannot verify what it contains, whether it has leaked, or whether it still reflects the current production distribution.
