# T-03 — Architecture Trade-off Worksheet
**Multimodal AI Feature Evaluation**

> **Purpose:** Document and compare architecture options before committing to a multimodal stack. Makes trade-offs between cost, faithfulness, audio quality, and latency explicit and visible.  
> **When to use:** Before finalizing the pipeline architecture. Even directional cost estimates reveal where your marginal dollar adds the most faithfulness.  
> **Key insight:** The first 20% of the budget allocated to ingestion buys more faithfulness than any other dollar spent.

---

## Document Header

| Field | Value |
|---|---|
| Feature | |
| Date | |
| Author | |

---

## Architecture A — Baseline

### Component Selection

| Component | Selection |
|---|---|
| Document Parser | |
| OCR Engine | |
| ASR Engine | |
| Embedding Model | |
| LLM | |
| TTS | |
| Vector DB | |

### Estimated Performance

| Metric | Estimate |
|---|---|
| Faithfulness score | _____% |
| Audio MOS | _____ |
| End-to-end latency | _____ s |
| Cost per output | $_____ |
| — of which: Ingestion | _____% |
| — of which: LLM / Reasoning | _____% |
| — of which: TTS | _____% |
| — of which: Vector DB / Other | _____% |

**Diagnosis:**

---

## Architecture B — Ingestion-First Variant

### Component Selection

| Component | Selection |
|---|---|
| Document Parser | |
| OCR Engine | |
| ASR Engine | |
| Embedding Model | |
| LLM | |
| TTS | |
| Vector DB | |

### Estimated Performance

| Metric | Estimate |
|---|---|
| Faithfulness score | _____% |
| Audio MOS | _____ |
| End-to-end latency | _____ s |
| Cost per output | $_____ |
| — of which: Ingestion | _____% |
| — of which: LLM / Reasoning | _____% |
| — of which: TTS | _____% |
| — of which: Vector DB / Other | _____% |

**Diagnosis:**

---

## Architecture C — Cascade Variant

### Routing Logic

| Trigger | Description |
|---|---|
| Fast-path trigger | |
| Escalation trigger | |

### Always-Applied Components

| Component | Selection |
|---|---|
| Document Parser | |
| OCR Engine | |
| ASR Engine | |

### Fast Path vs. Escalated Path

| Component | Fast Path | Escalated Path |
|---|---|---|
| LLM | | |
| TTS | | |

### Estimated Performance

| Metric | Estimate |
|---|---|
| Faithfulness score | _____% |
| Audio MOS | _____ |
| End-to-end latency | _____ s |
| Cost per output (blended) | $_____ |

**Diagnosis:**

---

## Comparison Summary

| Architecture | Faithfulness | MOS | Latency | Cost per Output |
|---|---|---|---|---|
| A — Baseline | _____% | _____ | _____ s | $_____ |
| B — Ingestion-First | _____% | _____ | _____ s | $_____ |
| C — Cascade | _____% | _____ | _____ s | $_____ |

---

## Recommendation

| Field | Entry |
|---|---|
| Recommended architecture | |
| Rationale | |
| Key trade-off accepted | |
| Key risk to monitor | |

---

## Architectural Self-Check

> ⚠️ If more than 60% of your per-output budget goes to the LLM and TTS while you are using a basic parser, you are in the most common architectural trap in multimodal AI. The first 20% of budget allocated to ingestion buys more faithfulness than any other dollar spent.

| Check | Status |
|---|---|
| Ingestion budget ≥ 20% of total per-output cost | ☐ Yes &nbsp; ☐ No |
| LLM + TTS combined ≤ 60% of total per-output cost | ☐ Yes &nbsp; ☐ No |
| Premium ingestion applied unconditionally (not only on escalation) | ☐ Yes &nbsp; ☐ No |

---

## Sign-Off

| Role | Name | Date |
|---|---|---|
| Engineering Lead | | |
| AI Reliability Lead | | |

---

## Architecture Pattern Reference

| Pattern | Faithfulness | Audio Quality | Latency | Cost |
|---|---|---|---|---|
| Basic parsers + small LLM + standard TTS | Low | Low | Fast | $ |
| Basic parsers + large LLM + premium TTS | Moderate | High | Moderate | $$$ |
| Premium ingestion + large LLM + premium TTS | High | High | Slow | $$$$ |
| Premium ingestion + cascade LLM + conditional TTS | Near-high | Good | Moderate | $$ |

---

## 2026 Cost Reference Points

> Verify current pricing before making architectural decisions — AI service costs change frequently.

| Component | Service Options | Unit | Cost Range |
|---|---|---|---|
| Document parsing (clean) | Google DocAI, Azure Form Recognizer, Docling | per page | $0.0015–$0.005 |
| OCR (scanned documents) | Google Cloud Vision, AWS Textract | per page | $0.0015–$0.003 |
| ASR (primary language) | Whisper Large-v3, Deepgram Nova-3 | per minute | $0.004–$0.025 |
| ASR (non-primary language) | Deepgram, AssemblyAI Universal-2 | per minute | $0.006–$0.030 |
| VLM reasoning (Gemini 2.5 Pro) | Google | per 1M tokens | $1.25–$2.50 |
| VLM reasoning (GPT-4o) | OpenAI | per 1M tokens | $2.50–$5.00 |
| TTS standard | Google TTS, Azure TTS | per 1M characters | $4–$16 |
| TTS podcast-grade | ElevenLabs, Cartesia | per minute output | $0.08–$0.30 |
| Vector DB (managed) | Pinecone, Weaviate | per 1M vectors/month | $70–$140 |

---

> Revisit this worksheet whenever a significant pipeline component changes. Archive completed versions — architecture decisions should be traceable.
