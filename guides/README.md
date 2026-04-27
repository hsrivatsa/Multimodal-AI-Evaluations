# Guides

This directory contains the three foundational documents of the Multimodal AI Evaluation Framework — a progressive learning and doing system designed to take any practitioner from first principles to a production-grade evaluation program.

---

## Reading Order

The guides are designed to be read in sequence. Each builds on the previous one.

| Step | Guide | What You Get | Time |
|---|---|---|---|
| 1 | [101 Guide] | The mental model — concepts, failure modes, and why multimodal evaluation is different | 2–3 hrs read |
| 2 | [Getting Started Guide]) | The navigation layer — where to start, how to move through the framework, phase-by-phase steps | 1 hr read |
| 3 | [Field Manual] | The complete operational discipline — 20 chapters, all five contracts, every fix surface, full governance | Reference |

---

## Guide 1 — 101 Guide

**File:** [`Multimodal AI Product Evaluation — 101 Guide - Enhanced.pdf`]

**Who it is for:** Anyone new to multimodal AI evaluation. No prior evaluation experience assumed.

**What it covers:**

- Why multimodal AI evaluation is harder than text-only evaluation — and why polished audio bypasses critical judgment in a way that text never does
- The nine-stage pipeline and where failures actually originate (~34% at Stage 1)
- The Five Quality Contracts and why collapsing them into one score hides failures
- The Five Gulfs — five fundamental gaps between what your team intends and what your system does
- The AMI Cycle: Analyze → Measure → Improve
- The hallucination detection toolkit: decompose-then-verify, NLI approach, key benchmarks
- Seven common misconceptions that consistently cause wasted months
- The evaluation tool ecosystem: when to reach for Galileo, Arize, Braintrust, LangSmith, Comet Opik, Patronus, Langfuse
- Where to start — whether you have a live product or are pre-launch

**Key insight from this guide:**

> *A multimodal AI product is a chain. Its strength is determined by its weakest link — and that weakest link is almost always invisible in the final output.*

---

## Guide 2 — Getting Started Guide

**File:** [`Multimodal AI Product Evaluation - Getting Started.pdf`]

**Who it is for:** Practitioners ready to build or improve an evaluation program. Assumes the 101 Guide has been read, or that you have some evaluation background.

**What it covers:**

- **Who Are You? Start Here** — a navigation table matching your situation to your entry point, with estimated time to first value
- **The Mindset Before Everything Else** — four pre-commitments that determine whether your evaluation program produces signal or noise
- **The 12-Week Phase-by-Phase Plan** with completion criteria for each phase:
  - Phase 1 — Foundation (Weeks 1–2): Judge Panel, Evaluation Brief, Ten-Trace Exercise
  - Phase 2 — Error Analysis (Weeks 2–5): Traces Coding, Tagged Coding, Causal Chains
  - Phase 3 — Measurement Layer (Weeks 5–8): Human Labels, Evaluator Building, CI Gating
- **Adapting for your team size** — solo practitioner through enterprise context
- **Getting organizational buy-in** — three arguments that consistently work, plus the fastest path to a yes

**The four commitments introduced in this guide:**

| Commitment | The Core Discipline |
|---|---|
| Per-Modality, Per-Contract Thinking | Never ask "is this output good?" Ask five separate questions — one per contract |
| Pipeline-First Diagnosis | Trace every failure to its origin stage before proposing any intervention |
| Reading Real Traces | Plan for 60–80% of development time to go to error analysis |
| Pre-Committed Thresholds | Set every quality bar before any evaluation runs — not after |

---

## Guide 3 — Practitioner's Field Manual

**File:** [`Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdf`]

**Who it is for:** Practitioners building or running a production multimodal AI evaluation program. The complete reference.

**What it covers — 20 chapters across 17 parts:**

| Part | Chapters | Focus |
|---|---|---|
| I — Foundation | Ch 1–2 | Evaluation Mindset · Evaluation Brief |
| II — Mapping | Ch 3 | Surface Mapping · Nine-Stage Pipeline |
| III — Error Analysis | Ch 4 | Error Analysis Protocol · Taxonomy Building · Causal Chains |
| IV — Quality Contracts | Ch 5 | Per-Contract Quality Statements · Reference Thresholds |
| V — Architecture | Ch 6 | Cost–Latency–Quality–Fidelity Trade-offs · Cascade Pattern |
| VI — Instrumentation | Ch 7 | Logging for Evaluability · Four Logging Layers · Drop-off Timestamps |
| VII — Evaluators | Ch 8 | Evaluator-Building Protocol · Cohen's Kappa · Slice Analysis |
| VIII — Production | Ch 9–11 | Production Monitoring · CI Gating · Progressive Rollout Gates |
| IX — Diagnosis | Ch 12 | Driver Analysis · Five Pipeline Hypotheses |
| X — Fixing | Ch 13 | The Thirteen Fix Surfaces · Routing Quick Reference |
| XI — Decisions | Ch 14 | Decision Rubric · Decision Memo · Reversal Conditions |
| XII — Experiments | Ch 15 | Randomisation Unit · Novelty Effect · Pre-Registration |
| XIII — Data | Ch 16 | Dataset Lifecycle · Leakage Vectors · Media Blob Management |
| XIV — Prioritization | Ch 17 | Six-Dimension Priority Formula · Blast Radius Worksheet |
| XV — Governance | Ch 18 | RACI · Prompt Review Board · Cadence Calendar · Debt Register |
| XVI — Tooling | Ch 19 | Build vs. Buy · Scenario-Based Tool Selection |
| XVII — Quarter 1 Plan | Ch 20 | 12-Week Action Plan · Quarter 2 and 3 Outlook |

**Appendices:**

| Appendix | Contents |
|---|---|
| A | Template Pack Quick Reference (T-01 through T-18) |
| B | Ten Starter Kit Artifacts with time estimates |
| C | Multimodal Failure Mode Library (13 named patterns) |
| D | Red Flags Checklist (run quarterly — 40+ checks) |
| E | The Five Gulfs and where each is bridged in the manual |
| F | Evaluation Maturity Model (Levels 1–5) |
| G | Benchmark Reference Map (MMDocBench, OCRBench, ChartQA, PodEval, and more) |
| H | Glossary of 30+ key terms in plain English |

---

## Quick Navigation by Situation

| You are... | Go here |
|---|---|
| Encountering multimodal AI evaluation for the first time | Start at [Multimodal AI Product Evaluation — 101 Guide - Enhanced.pdf] Part 1 |
| Confused about why one accuracy score is not enough | [Multimodal AI Product Evaluation — 101 Guide - Enhanced.pdf] Part 5 — The Four Contracts |
| Trying to understand where failures actually come from | [Multimodal AI Product Evaluation — 101 Guide - Enhanced.pdf] Part 3 — The Pipeline |
| Ready to build an evaluation program | [Multimodal AI Product Evaluation - Getting Started.pdf] — Phase 1 |
| Mid-program and need to build evaluators | [Multimodal AI Product Evaluation - Getting Started.pdf] — Phase 3 |
| Running a production alert investigation | [Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdf] Chapter 12 — Driver Analysis |
| Making a ship/hold/rollback decision | [Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdf] Chapter 14 — Decision-Making |
| Planning a quarterly governance review | [Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdfl] Chapter 18 — Governance |
| Looking for the right tool for your situation | [Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdfl] Chapter 19 — Build vs. Buy |
| Starting from zero with 12 weeks ahead | [Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdf] Chapter 20 — The 12-Week Plan |

---

## How the Guides Connect to the Templates

Every chapter in the Field Manual that has an associated template includes a reference callout. The templates live in [`/templates`](../templates).

| Guide section | Template |
|---|---|
| Getting Started Phase 1 — Evaluation Brief | [T-01](../templates/T-01-evaluation-brief.md) |
| Getting Started Phase 1 — Architecture | [T-03](../templates/T-03-architecture-worksheet.md) |
| Getting Started Phase 1 — Logging | [T-04](../templates/T-04-logging-schema.md) |
| Getting Started Phase 3 — Evaluator Prompts | [T-05](../templates/T-05-ingestion-fidelity-evaluator.md) through [T-09](../templates/T-09-cross-modal-consistency-evaluator.md) |
| Getting Started Phase 3 — CI Gating | [T-11](../templates/T-11-regression-suite-coverage-audit.md) · [T-12](../templates/T-12-ci-gate-policy.md) |
| Field Manual Ch 5 — Quality Statement | [T-02](../templates/T-02-quality-statement.md) |
| Field Manual Ch 9 — Monitoring | [T-10](../templates/T-10-gate-thresholds-alert-rules.md) |
| Field Manual Ch 12 — Driver Analysis | [T-13](../templates/T-13-driver-analysis-template.md) |
| Field Manual Ch 14 — Decisions | [T-14](../templates/T-14-decision-memo.md) |
| Field Manual Ch 15 — Experiments | [T-15](../templates/T-15-experiment-pre-registration.md) |
| Field Manual Ch 16 — Datasets | [T-16](../templates/T-16-dataset-record.md) |
| Field Manual Ch 17 — Prioritization | [T-17](../templates/T-17-backlog-prioritization-table.md) |
| Field Manual Ch 18 — Governance | [T-18](../templates/T-18-evaluation-debt-register.md) |

---

*Read the 101 Guide to understand the map. Read the Getting Started Guide to plan your route. Use the Field Manual to walk it.*
