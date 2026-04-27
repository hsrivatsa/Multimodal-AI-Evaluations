# Multimodal AI Evaluations

> **A practitioner's framework for testing AI products that see, hear, read, and speak.**

Built from applied evaluation practice on real multimodal AI products. Not theory — a working operational system with 18 production-ready templates, a complete governance layer, and evaluation reports across multiple products.

---

## The Problem This Solves

Text-only AI evaluation is hard. Multimodal AI evaluation is harder in one specific, dangerous way.

A confident, smooth, well-produced audio output **sounds trustworthy even when it is wrong.** A beautiful diagram **looks authoritative even when it misrepresents the data.** Production quality bypasses critical judgment before accuracy is assessed.

And the failure is usually invisible at the output — because approximately **34% of multimodal failures originate at the ingestion layer** (Stage 1 of 9), before the AI model has been involved at all. Evaluating only the final output means measuring symptoms, not causes.

This framework teaches you to find failures where they originate, not where they appear.

---

## What Is In This Repository

| Directory | Contents |
|---|---|
| [`/guides`](./guides) | 101 Guide · Getting Started Guide · Practitioner's Field Manual (20 chapters) |
| [`/templates`](./templates) | 18 production-ready evaluation templates (T-01 through T-18) |
| [`/reports`](./reports) | Evaluation reports applying this framework to real multimodal AI products |
| [`/implementations`](./implementations) | Platform-specific implementations using Braintrust, Arize, Comet Opik, LangSmith |

---

## The Five Quality Contracts

Multimodal AI products must be evaluated across five separate, independently failing contracts. A single accuracy score hides too much — always evaluate them separately.

| # | Contract | The Core Question |
|---|---|---|
| 1 | **Ingestion Fidelity** | Did the pipeline faithfully extract what was in the source? |
| 2 | **Faithfulness** | Is the output traceable to the sources? |
| 3 | **Factuality** | Is the output correct about the real world? |
| 4 | **Cross-Modal Consistency** | Do the output modalities agree with each other? |
| 5 | **Output Quality** | Is the production quality adequate per medium? |

> **Ingestion Fidelity is the most commonly missed contract.** In text-only AI it can be folded into faithfulness. In multimodal AI — where PDFs drop figure captions, ASR hallucinates during silence, and retrievers ignore image-bearing chunks — it earns its own contract, its own evaluator, its own canary monitor, and a 15% floor in every test suite at every lifecycle stage.

---

## The Nine-Stage Pipeline

Every multimodal failure originates at a specific stage. This framework evaluates all nine.

```
Stage 1 — Ingestion       ← ~34% of all failures start here
Stage 2 — Normalization
Stage 3 — Indexing
Stage 4 — Retrieval
Stage 5 — Reasoning
Stage 6 — Generation
Stage 7 — Synthesis       ← ~18% of failures start here
Stage 8 — Guardrails
Stage 9 — Delivery        ← where most teams only evaluate
```

---

## The 18 Templates

Every template is production-ready. Copy, adapt to your product, fill in before running any evaluations.

| Template | Purpose | When to Use |
|---|---|---|
| [T-01 Evaluation Brief](./templates/T-01-evaluation-brief.md) | Team alignment on five contracts before work begins | Start of every feature |
| [T-02 Quality Statement](./templates/T-02-quality-statement.md) | Technical spec for monitoring and CI systems | After T-01 is signed |
| [T-03 Architecture Worksheet](./templates/T-03-architecture-worksheet.md) | Cost vs. faithfulness trade-off documentation | Before committing to a stack |
| [T-04 Logging Schema](./templates/T-04-logging-schema.md) | Complete YAML spec for all four logging layers | Before going to production |
| [T-05 Ingestion Fidelity Evaluator](./templates/T-05-ingestion-fidelity-evaluator.md) | LLM judge prompt for Contract 1 | After error analysis |
| [T-06 Faithfulness Evaluator](./templates/T-06-faithfulness-evaluator.md) | LLM judge prompt for Contract 2 | After error analysis |
| [T-07 Factuality Evaluator](./templates/T-07-factuality-evaluator.md) | LLM judge prompt for Contract 3 | After error analysis |
| [T-08 Audio Quality Evaluator](./templates/T-08-audio-quality-evaluator.md) | LLM judge prompt for Contract 5 — four independent dimensions | After error analysis |
| [T-09 Cross-Modal Consistency Evaluator](./templates/T-09-cross-modal-consistency-evaluator.md) | LLM judge prompt for Contract 4 | After error analysis |
| [T-10 Gate Thresholds and Alert Rules](./templates/T-10-gate-thresholds-alert-rules.md) | Per-metric monitoring configuration with escalation policy | Before production monitoring |
| [T-11 Regression Suite Coverage Audit](./templates/T-11-regression-suite-coverage-audit.md) | Coverage gap identification per taxonomy tag + media blob registry | Building and maintaining test suite |
| [T-12 CI Gate Policy](./templates/T-12-ci-gate-policy.md) | Blocking conditions + false positive protocol | Before wiring CI |
| [T-13 Driver Analysis Template](./templates/T-13-driver-analysis-template.md) | Structured root-cause analysis for any monitoring alert | Every time an alert fires |
| [T-14 Decision Memo](./templates/T-14-decision-memo.md) | Evidence-backed Ship / Ramp / Hold / Rollback record | Every ship/hold decision |
| [T-15 Experiment Pre-Registration](./templates/T-15-experiment-pre-registration.md) | Hypothesis, metric, and decision rule before data collection | Before any A/B experiment |
| [T-16 Dataset Record](./templates/T-16-dataset-record.md) | Versioned dataset metadata with media blob registry | Creating or versioning datasets |
| [T-17 Backlog Prioritization Table](./templates/T-17-backlog-prioritization-table.md) | Six-dimension priority formula with blast radius scoring | After error analysis |
| [T-18 Evaluation Debt Register](./templates/T-18-evaluation-debt-register.md) | Quarterly governance audit across all seven debt categories | First week of every quarter |

---

## The Backlog Priority Formula

An original contribution of this framework. Rewards upstream, high-blast-radius fixes over visible downstream symptoms.

```
Priority Score = (S × F × C × B × U) ÷ TTL

S   = Severity       High=3 · Medium=2 · Low=1
F   = Frequency      % of traces as decimal (15% = 0.15)
C   = Confidence     High=3 · Medium=2 · Low=1
B   = Blast Radius   Count of downstream failure tags resolved by one fix
U   = Upstream-ness  Ingestion=5 · Retrieval=4 · Generation=3 · Synthesis=2 · Delivery=1
TTL = Time to deploy in days
```

**Why Blast Radius changes everything:** A parser fix that resolves a dropped-caption failure simultaneously resolves downstream faithfulness breaks and TTS mispronunciations sitting in the same causal chain. Blast radius is why an ingestion fix almost always outranks a prompt engineering fix — even when the prompt fix deploys faster.

| Example Fix | S | F | C | TTL | B | U | Score |
|---|---|---|---|---|---|---|---|
| Parser upgrade — drops captions | 3 | 0.15 | 3 | 3d | 3 | 5 | **6.75** |
| Pronunciation lexicon update | 2 | 0.12 | 3 | 1d | 1 | 2 | 1.44 |
| Cross-modal consistency check | 3 | 0.08 | 2 | 7d | 2 | 3 | 0.41 |

---

## Eval Test Case Distribution Across the Lifecycle

The distribution of your evaluation test cases should change as your product matures. Using the same eval mix in development, release, and production is a quiet mistake — it hides the wrong failures at the wrong time.

| Case Type | Development | Release (Gate) | Production |
|---|---|---|---|
| Happy Paths | 15% | 35% | 45% |
| Edge Cases | 30% | 20% | 5% |
| **Ingestion Failures** | **25%** | **15% floor** | **15% floor** |
| Safety Cases | 15% | 15% | 10% |
| Regressions | 15% | 15% | 25% |
| **Suite size** | **40–80** | **60–300** | **100–500+** |
| **Primary purpose** | Discovery | Enforcement | Monitoring |

> **The ingestion floor never drops below 15% at any lifecycle stage.** Multimodal pipelines fail silently upstream. Your eval suite must be able to see it.

---

## The AMI Cycle

The evaluation discipline runs on three continuous phases:

```
ANALYZE ──► MEASURE ──► IMPROVE ──► (repeat)
   │              │            │
Surface Map    Quality       Driver Analysis
Error Analysis Contracts     Fix Surfaces
               Evaluators    Prioritization
               Monitoring
```

Each cycle tightens your taxonomy, improves your evaluators, and reduces the time between a failure appearing in production and a fix landing.

---

## Evaluation Reports

Applying this framework to real multimodal AI products in the wild.

| Product | Category | Report |
|---|---|---|
| Huxe | Document-to-audio AI | [View report](./reports/huxe-evaluation/) |
| Google NotebookLM | Document-to-audio AI | Coming soon |
| HeyGen | AI video generation | Coming soon |
| Synthesia | Enterprise AI video | Coming soon |
| Loom AI | Async video + AI summary | Coming soon |
| Descript | Multimodal audio/video editing | Coming soon |
| Adobe Firefly | Generative image AI | Coming soon |

---

## Platform Implementations

Working implementations of this framework's evaluators on major evaluation platforms.

| Platform | Best For | Implementation |
|---|---|---|
| Braintrust | Dataset versioning, offline evaluation | [View](./implementations/braintrust/) |
| Arize Phoenix | Embedding drift, production monitoring | [View](./implementations/arize-phoenix/) |
| Comet Opik | Teams using Comet for ML tracking | [View](./implementations/comet-opik/) |
| LangSmith | LangChain-native, audio playback in traces | [View](./implementations/langsmith/) |

---

## Evaluation Maturity Model

Where is your team today?

| Level | Status | Description |
|---|---|---|
| 1 | Ad Hoc | No taxonomy. Decisions made by whoever argues most confidently. |
| 2 | Instrumented | Logging live. At least one evaluator with documented kappa ≥ 0.70. |
| 3 | Systematic | All five contracts have evaluators. CI gate blocking. Written decision memos. |
| 4 | Closed Loop | Production failures feed the regression suite. Driver analysis is the default response to every alert. |
| 5 | Self-Improving | New failure modes are taxonomized and in the regression suite within one sprint of discovery. |

> **You have reached Level 5 when:** a new team member can pick up any failing eval, find its taxonomy tag, look up its causal chain, route it to the correct fix surface, apply the T-17 prioritization formula, and propose an evidence-backed intervention — all without asking anyone.

---

## Where to Start

| You are... | Start here |
|---|---|
| New to multimodal AI evaluation | [`guides/101-guide.md`](./guides/101-guide.md) |
| Building an evaluation program from scratch | [`guides/getting-started-guide.md`](./guides/getting-started-guide.md) → [`T-01`](./templates/T-01-evaluation-brief.md) |
| Looking for a specific template | [`/templates`](./templates) directory |
| Responding to a production alert right now | [`T-13 Driver Analysis`](./templates/T-13-driver-analysis-template.md) |
| Making a ship/hold decision | [`T-14 Decision Memo`](./templates/T-14-decision-memo.md) |
| Running a quarterly program review | [`T-18 Evaluation Debt Register`](./templates/T-18-evaluation-debt-register.md) |
| Evaluating a specific platform | [`/implementations`](./implementations) directory |
| Reading evaluation reports | [`/reports`](./reports) directory |

---

## Key Concepts

**Ingestion Fidelity** — The most commonly missed contract. ~34% of multimodal failures originate at the ingestion layer before the model sees anything.

**Blast Radius** — The number of downstream failure tags resolved by a single upstream fix. The most underweighted dimension in standard backlog prioritization.

**Causal Chain** — A sequence where one upstream failure causes multiple downstream failures. Fix the root; resolve the chain.

**Canary Corpus** — A fixed set of 20 documents with known ground truth, checked daily against the ingestion pipeline. Never refreshed — stability is what makes it useful.

**Zero-Tolerance Event** — A failure that triggers immediate rollback regardless of all other scores. Named before any evaluation runs, not after.

**Judge Drift** — When the AI model powering your evaluators is silently updated by its provider. Evaluators become more lenient; metrics look like they're improving when they're not. Caught by monthly kappa recalibration on 20 fresh labeled examples.

**Consumption Drift** — Same technical output quality, declining user engagement. A cluster of listeners dropping off at the same audio timestamp is a precision failure detector that no LLM judge can replicate.

---

## The Failure Mode Library

Thirteen named failure patterns with pipeline origins and fix surfaces.

| Pattern | Description | Origin | Fix Surface |
|---|---|---|---|
| The Missing Caption | Parser drops figure caption; AI invents content | Stage 1 | Ingestion/Parsing |
| Careless Whisper | ASR hallucinates words during silence | Stage 1 | OCR/ASR + Silence Gate |
| Modality Bias Retrieval | Retriever returns only text chunks in figure-heavy corpus | Stage 4 | Reranking + RAG |
| Progressive Textual Drift | AI shifts from actual visual content to language priors over long output | Stage 6 | Visual Grounding |
| Speaker Identity Collapse | Multi-speaker audio: speakers converge, differentiation lost | Stage 7 | Voice/TTS + Topology |
| Narration-Visual Inversion | Audio says X increased; visual shows X decreased | Stages 6–7 | Topology + Cross-modal |
| Chunk Boundary Claim Split | Key claim split across chunk boundary; half retrieved | Stage 2 | Data Prep |
| Entity Mispronunciation Cascade | Domain term mispronounced; drop-off timestamps spike | Stage 7 | Voice/TTS + Data Prep |
| Scanned Document Blindness | Scanned content mangled; output discusses source in generalities | Stage 1 | OCR/ASR |
| Judge Drift | Evaluators green; user satisfaction declining; kappa decayed | Measurement | Monthly recalibration |
| Novelty Decay | Engagement high days 1–7; sharp decline by day 30 | Post-synthesis | Re-examine user job-to-be-done |
| Fabricated Disagreement | Critique format: counter-argument paraphrases original claim | Stage 6 | Prompt Engineering + Guardrails |
| Cross-Lingual Bleed | Non-primary language audio contains primary language phrases | Stage 7 | Voice/TTS + Model Routing |

---

## Citation

If you use this framework in your work:

```
Srivatsa, H. (2026). Multimodal AI Evaluations: A Practitioner's Framework.
GitHub: https://github.com/hsrivatsa/Multimodal-AI-Evaluations
```

---

## Author

**Harsha Srivatsa**
AI Solutions Architect · AI Product Leader
Founder, Indriya Innovations & NanoKernel
Creator of the Council of Councils architecture and Agent Genesis framework
Instructor to students across 90+ countries

[LinkedIn](https://www.linkedin.com/in/hsrivatsa) · [GitHub](https://github.com/hsrivatsa)

---

## Contributing

Contributions welcome. See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for guidelines.

Priority areas: product evaluation reports · platform implementation notebooks · translations

---

## License

MIT License — see [`LICENSE`](./LICENSE) for details.
Free to use, adapt, and build upon with attribution.

---

*The best multimodal AI evaluation program is the one your team actually runs.*

