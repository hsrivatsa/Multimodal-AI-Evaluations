# T-13 — Driver Analysis Template
**Multimodal AI Feature Evaluation**

> **Purpose:** Structured root-cause analysis for any monitoring alert or metric change.  
> **When to use:** Every time a monitoring alert fires. Do not skip this template in favour of an intuitive fix — the template exists because the intuitive fix is wrong approximately one time in three.  
> **Key rule:** Fill in Step 1 before opening any production logs. Write all five hypotheses before converging on a cause.

---

## The Three-Phase Protocol

| Phase | What You Do | Common Mistake to Avoid |
|---|---|---|
| 1 — Characterise | Describe what changed, by how much, in which segment, and when — before forming any hypothesis | Skipping straight to logs and forming a hypothesis from the first thing you see |
| 2 — Hypothesise | Generate ≥ 4 competing hypotheses spanning all pipeline layers | Generating only one hypothesis — the one that matches your instinct |
| 3 — Test | Test each hypothesis systematically; confirm root cause before proposing any intervention | Proposing a fix before ruling out competing causes |

---

## Document Header

| Field | Entry |
|---|---|
| Analyst | |
| Incident ID | |
| Date | |
| Metric | |

---

## Step 1 — Observed Pattern

> ⚠️ Fill this in **before opening any production logs**.

| Field | Entry |
|---|---|
| Magnitude of change | _____% |
| Direction | ☐ Up &nbsp; ☐ Down |
| Output modality / pipeline junction affected | |
| Segments affected | |
| Segments NOT affected | |
| Time window of change | |
| Coinciding deploy, provider update, or event | |

**Characterisation sentence** *(fill in before proceeding to Step 2):*

> "[Metric] dropped from _____% to _____% — a _____-point decline — on [segment]. The drop appeared in the [N]-day window following [event]. [Other segments] were unaffected."

---

## Step 2 — Hypotheses

> ⚠️ Write **all five hypotheses** before opening production logs.

---

### H1 — Ingestion Layer
*(Parser version, OCR/ASR update, caption drop rate, scanned content handling, new file type distribution)*

| Field | Entry |
|---|---|
| Hypothesis | |
| Test | |
| Result | |

---

### H2 — Retrieval / RAG
*(Modality distribution of retrieved chunks, retrieval recall by content type, embedding model update, chunking boundary behaviour)*

| Field | Entry |
|---|---|
| Hypothesis | |
| Test | |
| Result | |

---

### H3 — Generation / Prompt
*(System prompt change, model update, temperature, context window truncation, token budget change)*

| Field | Entry |
|---|---|
| Hypothesis | |
| Test | |
| Result | |

---

### H4 — Output Synthesis
*(TTS model update, voice update, renderer version, cross-modal branch consistency, speaker assignment)*

| Field | Entry |
|---|---|
| Hypothesis | |
| Test | |
| Result | |

---

### H5 — Distribution Shift
*(New source types, new user segments, new languages, new input complexity, new query patterns)*

| Field | Entry |
|---|---|
| Hypothesis | |
| Test | |
| Result | |

---

## Step 3 — Root Cause Confirmation

| Field | Entry |
|---|---|
| Confirmed cause | |
| Evidence that confirms this cause | |
| H1 ruled out because | |
| H2 ruled out because | |
| H3 ruled out because | |
| H4 ruled out because | |
| H5 ruled out because | |
| Remaining uncertainty | |

---

## Step 4 — Intervention

| Field | Entry |
|---|---|
| Proposed action | |
| Fix Surface (from the 13 fix surfaces) | |
| Expected metric movement if fix works | |
| Owner | |
| Target date | |

---

## Step 5 — Validation Plan

| Field | Entry |
|---|---|
| How will we confirm the fix worked | |
| Metric and threshold that confirms success | |
| Observation window | _____ days after deploy |

---

## Step 6 — Rollback Plan

| Field | Entry |
|---|---|
| If fix makes things worse, the action is | |
| Rollback owner | |

---

## Post-Resolution Record

| Field | Entry |
|---|---|
| Resolution date | |
| Metric restored to | _____% (baseline was _____%) |
| Root cause added to taxonomy | ☐ Yes &nbsp; ☐ No |
| Regression case added to suite | ☐ Yes &nbsp; ☐ No |
| Post-mortem note | |

---

## Routing: Confirmed Cause → Fix Surface

| Confirmed Cause Origin | First-Line Fix Surface | Second-Line Surface |
|---|---|---|
| Parser drops content | Ingestion / Parsing | Data Prep |
| OCR wrong at character level | OCR / ASR | Ingestion / Parsing |
| ASR wrong at word level | OCR / ASR | Data Prep (vocabulary) |
| ASR invented content during silence | OCR / ASR | Guardrails (silence gate) |
| Retriever misses visual content | Reranking | RAG |
| Model fabricates quotes | Guardrails | Prompt Engineering |
| Speaker attribution wrong | Topology | Agents |
| Two output modalities contradict | Topology | Tools |
| TTS mispronounces entity | Voice / TTS | Data Prep (lexicon) |
| Visual taxonomy wrong | Prompt Engineering | Visual Grounding |

---

## Common Driver Analysis Mistakes

| Mistake | Cost | Fix |
|---|---|---|
| Defaulting to prompt engineering first | Papers over real cause; failure re-emerges in 1–2 sprints | Always write H1 (ingestion) before any prompt hypothesis |
| Skipping the ingestion diff | Stage 1 failures are invisible to product dashboards | Check ingestion metrics first, every time |
| Single-modality blame | Misses cross-modal junction as origin | Trace the full causal chain across all output modalities |
| Acting before the hypothesis list is complete | Fixes symptom, not root cause | Complete all five hypotheses before opening logs |

---

> Archive completed driver analysis templates alongside the incidents they resolved. The post-resolution checklist closes the loop from production failure to evaluation suite coverage.
