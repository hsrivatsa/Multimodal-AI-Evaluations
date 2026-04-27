# T-04 — Minimum Logging Schema
**Multimodal AI Feature Evaluation**

> **Purpose:** The minimum viable logging specification for a multimodal AI product. Covers all four layers: request identity, ingestion trace, retrieval and generation, output and consumption.  
> **When to use:** During instrumentation setup. Implement before going to production.  
> **Ground rule:** If you didn't log it, you cannot evaluate it.

---

## The Four Logging Layers

| Layer | What It Covers | Commonly Skipped? |
|---|---|---|
| 1 — Request Identity | Trace IDs, session IDs, timestamps, file types | Rarely |
| 2 — Ingestion Trace | Parser output, OCR/ASR confidence, caption retention | Yes — most commonly missing |
| 3 — Retrieval & Generation | Chunk distribution, token counts, model version | Partially |
| 4 — Output & Consumption | Drop-off timestamps, export rate, return visits | Yes — most commonly missing |

---

## Blind Spot Self-Check

Run this before finalising your logging implementation. Every "No" is a field to add this sprint.

| For any given production trace, can you reconstruct... | Status |
|---|---|
| The original uploaded files? | ☐ Yes &nbsp; ☐ No |
| The ingestion layer's extracted representation? | ☐ Yes &nbsp; ☐ No |
| The exact retrieved chunks with modality distribution? | ☐ Yes &nbsp; ☐ No |
| The assembled prompt with token counts by section? | ☐ Yes &nbsp; ☐ No |
| The output in its original media format? | ☐ Yes &nbsp; ☐ No |
| The user's consumption behavior including drop-off timestamps? | ☐ Yes &nbsp; ☐ No |

---

## Full Schema (YAML)

Copy this schema into your logging implementation. Fields marked `# MOST COMMONLY MISSING` are the ones teams typically skip and regret within 30 days. Do not skip them.

```yaml
# ════════════════════════════════════════════════════════
# LAYER 1 — REQUEST IDENTITY
# Always log. No exceptions.
# ════════════════════════════════════════════════════════

trace_id: str                      # Unique per request; primary debug key
span_id: str                       # For distributed tracing systems
session_id: str                    # Groups traces within one user session
user_id: str                       # Hashed per your privacy policy
timestamp_ingress: datetime        # When request arrived
timestamp_egress: datetime         # When response was delivered
end_to_end_duration_ms: int        # Total wall-clock time

# ════════════════════════════════════════════════════════
# LAYER 1b — SOURCES UPLOADED
# Log for every source in the request.
# ════════════════════════════════════════════════════════

sources:
  - source_type: pdf | slides | docx | audio | image | video
    original_size_bytes: int
    original_hash: sha256           # Enables re-pull for debugging
    pdf_page_count: int
    pdf_has_scanned_content: bool
    pdf_has_figures: bool
    pdf_has_tables: bool
    audio_duration_sec: float
    audio_language_detected: str
    audio_has_multiple_speakers: bool
    video_duration_sec: float

# ════════════════════════════════════════════════════════
# LAYER 2 — INGESTION TRACE
# MOST COMMONLY MISSING — DO NOT SKIP.
# Without this layer you cannot diagnose Stage 1 failures,
# which cause ~34% of all multimodal product failures.
# ════════════════════════════════════════════════════════

ingestion:
  parser_version: str              # Version-pin; enables silent-update detection
  pages_extracted: int
  pages_with_ocr_fallback: int     # High ratio = scanned-heavy input
  ocr_char_confidence_p50: float   # Median character confidence
  ocr_char_confidence_p05: float   # Tail confidence — reveals failure cases
  asr_word_confidence_p50: float   # Median word confidence
  asr_hallucination_flag: bool     # True if ASR invented content during silence
  figures_detected: int
  captions_retained: int
  captions_expected: int           # Gap = caption drop rate
  extracted_char_count: int

# ════════════════════════════════════════════════════════
# LAYER 3 — RETRIEVAL
# ════════════════════════════════════════════════════════

retrieval:
  retrieved_chunk_modality_counts:
    text: int
    image: int
    table: int
    audio_transcript: int
  corpus_modality_distribution:
    text_pct: float
    image_pct: float
    table_pct: float

# ════════════════════════════════════════════════════════
# LAYER 3b — GENERATION
# ════════════════════════════════════════════════════════

model_version: str
system_prompt_hash: str
prompt_assembly_tokens_per_section:
  source_text: int
  figure_descriptions: int
  retrieved_chunks: int
  instructions: int
total_prompt_tokens: int
temperature: float
seed: int
cost_reasoning_usd: float

# ════════════════════════════════════════════════════════
# LAYER 4a — OUTPUT SYNTHESIS
# ════════════════════════════════════════════════════════

audio:
  tts_model_version: str
  audio_duration_sec: float
  pronunciation_lexicon_version: str
  script_audio_alignment_score: float
  tts_cost_usd: float

visual:
  renderer_version: str
  node_count: int
  render_validator_pass: bool
  concept_coverage_score: float

# ════════════════════════════════════════════════════════
# LAYER 4b — CONSUMPTION
# MOST COMMONLY MISSING — DO NOT SKIP.
# ════════════════════════════════════════════════════════

user_feedback: thumbs_up | thumbs_down | regenerate | null
audio_listen_completion_pct: float
audio_drop_off_timestamps: list[float]
audio_relisten_segments: list[{start_ms: int, end_ms: int}]
visual_export_performed: bool
visual_share_performed: bool
return_visit_within_7d: bool
```

---

## Tiered Storage Policy

### Always Log
All metadata fields above. Full payloads for a 1–2% random sample.

### Automatically Expand to Full Payload When

| Trigger Condition | Why It Matters |
|---|---|
| User clicks thumbs-down or regenerates | Direct failure signal |
| Audio listen-through < 30% | Strong signal of output quality failure |
| User drops off within first 90 seconds | Likely a severe early-output failure |
| `ocr_char_confidence_p05` < 0.65 | Tail OCR failure detected |
| `asr_word_confidence_p50` < 0.72 | ASR quality below acceptable floor |
| `captions_retained` < 85% of `captions_expected` | Significant caption drop |
| `asr_hallucination_flag` = true | Invented content entered the pipeline |
| `render_validator_pass` = false | Visual output structurally invalid |

### When Expanded, Store
Full audio waveform · Full ingestion parse tree · All retrieved chunks · Visual render snapshot · Speaker turn map with per-word timestamps

---

## Retention Schedule

| Data Type | Retention Period |
|---|---|
| Log metadata (text only) | 90 days + aggregates permanent |
| Expanded text payloads | 30–90 days |
| Audio / video blobs | 14–30 days |
| PII-scrubbed audio transcripts | 60 days |
| Visual render snapshots | 30 days |
| Aggregated consumption telemetry | Permanent |

---

> This schema is the minimum viable logging specification. Add product-specific fields as needed. Never remove fields referenced by active evaluators or monitoring alerts.
