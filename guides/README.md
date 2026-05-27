# Guides

This directory contains the foundational documents of the **Multimodal AI Evaluation Framework** — a progressive learning and doing system designed to take any practitioner from first principles to a production-grade evaluation program that learns on purpose rather than by accident.

The collection is organized in two layers:

- **The foundational trilogy** (Guides 1–3) builds the operational discipline: how to think about multimodal evaluation, how to navigate a program, and how to run one end-to-end.
- **The extension pair** (Guides 4–5) turns that discipline into a *measurement system* (Statistical Aspects) and a *learning system* (Experimentation and Hypothesis-Driven Evaluation).

---

## Reading Order

The guides are designed to be read in sequence. Each builds on the previous one.

| Step | Guide | What You Get | Time |
| --- | --- | --- | --- |
| 1 | [101 Guide](./Multimodal%20AI%20Product%20Evaluation%20%E2%80%94%20101%20Guide%20-%20Enhanced.pdf) | The mental model — concepts, failure modes, and why multimodal evaluation is different | 2–3 hrs read |
| 2 | [Getting Started Guide](./Multimodal%20AI%20Product%20Evaluation%20-%20Getting%20Started.pdf) | The navigation layer — where to start, how to move through the framework, phase-by-phase steps | 1 hr read |
| 3 | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) | The complete operational discipline — 20 chapters, all five contracts, every fix surface, full governance | Reference |
| 4 | [Statistical Aspects (Three-Volume Guide)](./Statistical%20Aspects%20for%20Multimodal%20AI%20Evaluations%20-%20Three%20Volume%20Guide.pdf) | The statistical layer — how to read, produce, and institutionalize trustworthy eval evidence | 3–4 hrs read |
| 5 | [Experimentation and Hypothesis-Driven Evaluation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) | The learning layer — turning eval evidence into causal learning through CLAIM, the Experiment Portfolio, and the Learning Archive | 1–2 hrs read |

---

## Guide 1 — 101 Guide

**File:** [`Multimodal AI Product Evaluation — 101 Guide - Enhanced.pdf`](./Multimodal%20AI%20Product%20Evaluation%20%E2%80%94%20101%20Guide%20-%20Enhanced.pdf)

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

**File:** [`Multimodal AI Product Evaluation - Getting Started.pdf`](./Multimodal%20AI%20Product%20Evaluation%20-%20Getting%20Started.pdf)

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
| --- | --- |
| Per-Modality, Per-Contract Thinking | Never ask "is this output good?" Ask five separate questions — one per contract |
| Pipeline-First Diagnosis | Trace every failure to its origin stage before proposing any intervention |
| Reading Real Traces | Plan for 60–80% of development time to go to error analysis |
| Pre-Committed Thresholds | Set every quality bar before any evaluation runs — not after |

---

## Guide 3 — Practitioner's Field Manual

**File:** [`Multimodal AI Product Evaluation - The Practioner's Field Manual - v2.1.pdf`](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf)

**Who it is for:** Practitioners building or running a production multimodal AI evaluation program. The complete reference.

**What it covers — 20 chapters across 17 parts:**

| Part | Chapters | Focus |
| --- | --- | --- |
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
| --- | --- |
| A | Template Pack Quick Reference (T-01 through T-18) |
| B | Ten Starter Kit Artifacts with time estimates |
| C | Multimodal Failure Mode Library (13 named patterns) |
| D | Red Flags Checklist (run quarterly — 40+ checks) |
| E | The Five Gulfs and where each is bridged in the manual |
| F | Evaluation Maturity Model (Levels 1–5) |
| G | Benchmark Reference Map (MMDocBench, OCRBench, ChartQA, PodEval, and more) |
| H | Glossary of 30+ key terms in plain English |

---

## Guide 4 — Statistical Aspects for Multimodal AI Evaluations

**File:** [`Statistical Aspects for Multimodal AI Evaluations - Three Volume Guide.pdf`](./Statistical%20Aspects%20for%20Multimodal%20AI%20Evaluations%20-%20Three%20Volume%20Guide.pdf)

**Who it is for:** Practitioners who have built the foundational evaluation discipline (Guides 1–3) and now need to make their evaluation evidence statistically defensible. ML engineers, applied scientists, eval engineers, AI Solutions Architects, and the leaders who consume their reports.

**What it covers — three progressive volumes:**

| Volume | Focus | Core Question |
| --- | --- | --- |
| Volume 1 — Statistical Literacy | How to *read* eval evidence responsibly | When does an eval report deserve my trust? |
| Volume 2 — Statistical Practice | How to *produce* eval evidence defensibly | How do I run an eval whose results would survive an audit? |
| Volume 3 — Statistical Frameworks | How to *institutionalize* eval evidence at scale | How does an organization make statistical rigor repeatable? |

**Topics covered across the three volumes:**

- Confidence intervals, effect sizes, sample-size intuition — what a "statistically significant" lift actually means and when it does not warrant a decision
- Judge calibration discipline, inter-rater agreement (Cohen's kappa and multimodal variants), drift monitoring
- Paired comparison design, stratification by slice, holdout integrity, multiple-comparison correction
- The Quality Contract registry, decision gates, and pre-registered minimum meaningful effects
- The Statistical Debt Register — making deferred statistical work visible and payable
- The Risk-Aware Operating Loop — five questions that turn statistical discipline into governance
- EvalOps as the operating model that holds it all together

**Key insight from this guide:**
> *An eval result is not a fact until it carries its uncertainty with it. Sample size, confidence intervals, judge calibration, and slice stratification are not statistical formalities — they are the difference between evidence and decoration.*

---

## Guide 5 — Experimentation and Hypothesis-Driven Evaluation

**File:** [`Experimentation and Hypothesis-Driven Multimodal AI Evaluation.pdf`](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf)

**Who it is for:** Practitioners with statistically sound measurements (via Guides 1–4) who now need to turn measurements into *causal learning* about what actually moves quality. AI Product Managers, AI Solutions Architects, Eval Engineers, ML Engineers, Applied Scientists, AI governance leaders, and technical founders building multimodal AI products.

**What it covers:**

- **The central distinction.** Evaluation measures quality. Statistics tells us whether to trust the measurement. Experimentation tells us what actually changes quality.
- **The CLAIM framework** — a five-part hypothesis template (Change · Logic · Assessment · Impact · Mitigation) that makes every release-decision hypothesis explicit and testable.
- **A six-type hypothesis taxonomy** — Quality, Risk, Slice, Architecture, Judge, UX — that prevents teams from running the wrong experimental design for the question being asked.
- **The nine-layer Multimodal Experimentation Stack** — from Risk Language at the bottom to Learning Archive at the top.
- **Hypotheses for Agentic Systems** — four new hypothesis shapes (Trajectory, Tool-Selection, Multi-Turn Consistency, Failure-Recovery) that emerge when the system plans, calls tools, and reflects.
- **The eight experiment types** — offline paired, online A/B, shadow, canary, ablation, perturbation, preference, synthetic — with a risk-vs-decision selection matrix and the typical ramp sequence.
- **The Experiment Portfolio** — Confirmatory / Exploratory / Monitoring, with a 70/20/10 default mix and explicit budget framing.
- **The Experimentation Maturity Model** — a five-level self-assessment ladder from Reactive to Self-Improving.
- **The T-19 Hypothesis-Driven Multimodal Evaluation Brief** — a one-page release-decision artifact, with a fully populated worked example.
- **The Learning Archive discipline** — the post-experiment artifact that turns single experiments into organizational memory, with a worked archive entry.
- **Thirteen named failure patterns** with prevention practices, including agentic-specific patterns (trajectory hooks not wired, agent state non-determinism, judge drift mid-experiment, HARKing, eval-set co-evolution).
- **The Risk-Aware Operating Loop extension** — four new questions that turn the governance loop into a learning loop.

**Key insight from this guide:**
> *A good multimodal experiment does not end with a p-value. It ends with a decision and a learning artifact. The future of multimodal AI evaluation is not only better measurement. It is better learning.*

---

## Quick Navigation by Situation

| You are... | Go here |
| --- | --- |
| Encountering multimodal AI evaluation for the first time | [101 Guide](./Multimodal%20AI%20Product%20Evaluation%20%E2%80%94%20101%20Guide%20-%20Enhanced.pdf) Part 1 |
| Confused about why one accuracy score is not enough | [101 Guide](./Multimodal%20AI%20Product%20Evaluation%20%E2%80%94%20101%20Guide%20-%20Enhanced.pdf) Part 5 — The Four Contracts |
| Trying to understand where failures actually come from | [101 Guide](./Multimodal%20AI%20Product%20Evaluation%20%E2%80%94%20101%20Guide%20-%20Enhanced.pdf) Part 3 — The Pipeline |
| Ready to build an evaluation program | [Getting Started Guide](./Multimodal%20AI%20Product%20Evaluation%20-%20Getting%20Started.pdf) — Phase 1 |
| Mid-program and need to build evaluators | [Getting Started Guide](./Multimodal%20AI%20Product%20Evaluation%20-%20Getting%20Started.pdf) — Phase 3 |
| Running a production alert investigation | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) Chapter 12 — Driver Analysis |
| Making a ship/hold/rollback decision | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) Chapter 14 — Decision-Making |
| Planning a quarterly governance review | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) Chapter 18 — Governance |
| Looking for the right tool for your situation | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) Chapter 19 — Build vs. Buy |
| Starting from zero with 12 weeks ahead | [Field Manual](./Multimodal%20AI%20Product%20Evaluation%20-%20The%20Practioner's%20Field%20Manual%20-%20v2.1.pdf) Chapter 20 — The 12-Week Plan |
| Reading an eval report and unsure whether to trust the headline number | [Statistical Aspects](./Statistical%20Aspects%20for%20Multimodal%20AI%20Evaluations%20-%20Three%20Volume%20Guide.pdf) — Volume 1 |
| Calibrating an LLM judge or measuring inter-rater agreement | [Statistical Aspects](./Statistical%20Aspects%20for%20Multimodal%20AI%20Evaluations%20-%20Three%20Volume%20Guide.pdf) — Volume 2 |
| Setting up Quality Contract gates and the Statistical Debt Register | [Statistical Aspects](./Statistical%20Aspects%20for%20Multimodal%20AI%20Evaluations%20-%20Three%20Volume%20Guide.pdf) — Volume 3 |
| Writing the CLAIM brief that gates your next release | [Experimentation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) — §6 and §20 |
| Designing your experiment portfolio mix (Confirmatory / Exploratory / Monitoring) | [Experimentation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) — §13 |
| Self-assessing your team's experimentation maturity | [Experimentation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) — §14 |
| Running an experiment on an agentic system | [Experimentation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) — §11 |
| Filing a Learning Archive entry after a release decision | [Experimentation](./Experimentation%20and%20Hypothesis-Driven%20Multimodal%20AI%20Evaluation.pdf) — §21 |

---

## How the Guides Connect to the Templates

Every chapter in the Field Manual that has an associated template includes a reference callout. The templates live in [`/templates`](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates).

| Guide section | Template |
| --- | --- |
| Getting Started Phase 1 — Evaluation Brief | [T-01](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-01-evaluation-brief.md) |
| Getting Started Phase 1 — Architecture | [T-03](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-03-architecture-worksheet.md) |
| Getting Started Phase 1 — Logging | [T-04](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-04-logging-schema.md) |
| Getting Started Phase 3 — Evaluator Prompts | [T-05](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-05-ingestion-fidelity-evaluator.md) through [T-09](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-09-cross-modal-consistency-evaluator.md) |
| Getting Started Phase 3 — CI Gating | [T-11](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-11-regression-suite-coverage-audit.md) · [T-12](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-12-ci-gate-policy.md) |
| Field Manual Ch 5 — Quality Statement | [T-02](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-02-quality-statement.md) |
| Field Manual Ch 9 — Monitoring | [T-10](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-10-gate-thresholds-alert-rules.md) |
| Field Manual Ch 12 — Driver Analysis | [T-13](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-13-driver-analysis-template.md) |
| Field Manual Ch 14 — Decisions | [T-14](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-14-decision-memo.md) |
| Field Manual Ch 15 — Experiments | [T-15](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-15-experiment-pre-registration.md) |
| Field Manual Ch 16 — Datasets | [T-16](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-16-dataset-record.md) |
| Field Manual Ch 17 — Prioritization | [T-17](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-17-backlog-prioritization-table.md) |
| Field Manual Ch 18 — Governance | [T-18](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-18-evaluation-debt-register.md) |
| Statistical Aspects Vol 3 — Decision Gates | [T-14](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-14-decision-memo.md) |
| Statistical Aspects Vol 3 — Pre-registration & Quality Contract Registry | [T-15](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-15-experiment-pre-registration.md) |
| Statistical Aspects Vol 3 — Statistical Debt Register | [T-18](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-18-evaluation-debt-register.md) |
| Experimentation — Hypothesis Brief (CLAIM + T-19) | [T-15](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-15-experiment-pre-registration.md) *(extends with CLAIM, slice plan, judge calibration status, Learning Archive pointer)* |
| Experimentation — Decision Rules | [T-14](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-14-decision-memo.md) |
| Experimentation — Experiment Budget / Right-Sizing | [T-17](https://github.com/hsrivatsa/Multimodal-AI-Evaluations/blob/main/templates/T-17-backlog-prioritization-table.md) |

*Note: the Experimentation guide references a "T-19 Hypothesis-Driven Multimodal Evaluation Brief." Operationally, this maps to T-15 (Experiment Pre-Registration) extended with the CLAIM framework, an explicit slice plan, judge calibration status, and a Learning Archive entry pointer. Future repo iterations may split this into a standalone T-19 template; for now, treat it as T-15 v2.*

---

*Read the **101 Guide** to understand the map. Read the **Getting Started Guide** to plan your route. Use the **Field Manual** to walk it. Read the **Statistical Aspects** to know whether your steps are real. Read **Experimentation and Hypothesis-Driven Evaluation** to know why you took them.*
