# T-11 — Regression Suite Coverage Audit
**Multimodal AI Feature Evaluation**

> **Purpose:** Track coverage of your regression suite against your full failure taxonomy.  
> **When to use:** When building the initial regression suite, and every quarter as part of the Evaluation Debt Register (T-18).  
> **Key rule:** Any tag with fewer than 5 cases is a blind spot — you cannot reliably detect a regression on a failure mode with fewer than 5 test cases.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Version | |
| Last Audit Date | |
| Auditor | |

---

## Coverage Audit Table

| Failure Tag | Case Count | Sources | Media Blobs Registered? | Gap? (< 5 cases) |
|---|---|---|---|---|
| `ingestion.[type].dropped_caption` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `ingestion.[type].layout_scramble` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `ingestion.ocr.scanned_drop` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `ingestion.ocr.handwriting` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `ingestion.asr.term_miss` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `ingestion.asr.silence_hallucination` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `retrieval.modality_bias` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `retrieval.visual_chunk_dropped` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `grounding.faithfulness_break` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `grounding.speaker_attribution` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `grounding.cross_source_merge` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `generation.fabricated_quote` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `generation.invented_statistic` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `cross_modal.output_mismatch` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `cross_modal.speaker_drift` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.audio.mispronunciation` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.audio.prosody_flat` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.audio.script_drift` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.visual.layout_overlap` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.visual.taxonomic_error` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `output.visual.concept_gap` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `safety.pii_in_output` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| `safety.copyright_reproduction` | | | ☐ Yes &nbsp; ☐ No | ☐ |
| [Product-specific tag] | | | ☐ Yes &nbsp; ☐ No | ☐ |
| [Product-specific tag] | | | ☐ Yes &nbsp; ☐ No | ☐ |
| **TOTAL** | | | | |

---

## Suite Tier Configuration

| Suite | Target Cases | Coverage | Target Runtime | Cadence |
|---|---|---|---|---|
| Per-PR fast gate | 40–60 | Ingestion + faithfulness + factuality; skip full TTS | ~12 minutes | Every PR |
| Nightly full regression | 300–500 | Full modality coverage per taxonomy tag | ~4 hours | Nightly |
| Weekly adversarial | 50 red-team | Worst-case inputs, tail source types | ~2 hours | Weekly |

---

## Source Distribution Target

| Source Type | Current Count | Target % | Gap? |
|---|---|---|---|
| Single clean document | | 25–30% | |
| Single scanned document | | 10–15% | |
| Multi-source (3–5) | | 20–25% | |
| Multi-source (6+) | | 10% | |
| Audio input | | 10–15% | |
| Mixed sources | | 10% | |
| Non-primary language | | 5–10% | |

---

## Media Blob Registry

> **Blob management rules:**
> - Store all evaluation media in a dedicated bucket separate from production
> - Verify integrity using SHA-256 hashes — a modified blob invalidates the test case
> - When a media file changes, create a new case; do not update in place
> - Evaluation media retention: 30–90 days; flag expired blobs in this registry

| Case ID | Failure Tag | Blob URI | SHA-256 Hash | Added Date | Expiry Date | PII Reviewed? |
|---|---|---|---|---|---|---|
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |
| | | | | | | ☐ |

---

## Gap Remediation Tracker

For every tag identified as a gap (< 5 cases), document the plan to close it.

| Failure Tag | Current Count | Target Count | Source Strategy | Owner | Target Date |
|---|---|---|---|---|---|
| | | 5 | | | |
| | | 5 | | | |
| | | 5 | | | |
| | | 5 | | | |
| | | 5 | | | |

---

## Audit History

| Audit Date | Auditor | Total Cases | Tags Below Minimum | Gaps Closed Since Last Audit | Notes |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |

---

> Run this audit at suite creation and every quarter as part of the Evaluation Debt Register (T-18). A suite that has never been audited is a suite whose blind spots are unknown.
