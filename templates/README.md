# Templates

18 production-ready templates for multimodal AI evaluation. Every template in this directory is a working document — copy it, adapt it to your product, and fill it in before running any evaluations.

> **How to use these templates:** Do not treat them as forms to complete after the fact. The value of each template comes from completing it *before* the activity it governs — before any evaluations run, before any gate fires, before any deployment decision is made. Templates completed after the fact anchor to what already happened. Templates completed before anchor to what should happen.

---

## Template Index

### Foundation

| Template | Purpose | Complete Before... |
|---|---|---|
| [T-01 Evaluation Brief](./T-01-evaluation-brief.md) | Team alignment on all five quality contracts, named thresholds, zero-tolerance events, and sign-off | Any evaluation work begins |
| [T-02 Quality Statement](./T-02-quality-statement.md) | Technical specification for monitoring systems and CI gates — translates T-01 into system-readable thresholds | Designing any evaluator or alert |
| [T-03 Architecture Trade-off Worksheet](./T-03-architecture-worksheet.md) | Documented comparison of three architecture options with cost, faithfulness, latency, and audio quality estimates | Committing to a pipeline stack |

### Instrumentation

| Template | Purpose | Complete Before... |
|---|---|---|
| [T-04 Minimum Logging Schema](./T-04-logging-schema.md) | Complete YAML logging spec covering all four layers — request identity, ingestion trace, retrieval and generation, output and consumption | Going to production |

### Evaluator Prompts — One Per Contract

| Template | Contract | Kappa for CI Gate | Kappa for Monitoring |
|---|---|---|---|
| [T-05 Ingestion Fidelity Evaluator](./T-05-ingestion-fidelity-evaluator.md) | Contract 1 — Ingestion Fidelity | ≥ 0.85 | ≥ 0.75 |
| [T-06 Faithfulness Evaluator](./T-06-faithfulness-evaluator.md) | Contract 2 — Faithfulness | ≥ 0.80 | ≥ 0.70 |
| [T-07 Factuality Evaluator](./T-07-factuality-evaluator.md) | Contract 3 — Factuality | ≥ 0.80 | ≥ 0.70 |
| [T-08 Audio Quality Evaluator](./T-08-audio-quality-evaluator.md) | Contract 5 — Output Quality (Audio) | ≥ 0.80 | ≥ 0.70 |
| [T-09 Cross-Modal Consistency Evaluator](./T-09-cross-modal-consistency-evaluator.md) | Contract 4 — Cross-Modal Consistency | ≥ 0.80 | ≥ 0.70 |

> **Why T-05 requires stricter kappa:** Ingestion failures cascade through the entire pipeline. A miscalibrated ingestion evaluator produces misleading scores across all downstream contracts simultaneously. Every other evaluator is downstream of it.

### Production and CI

| Template | Purpose | Complete Before... |
|---|---|---|
| [T-10 Gate Thresholds and Alert Rules](./T-10-gate-thresholds-alert-rules.md) | Per-metric monitoring configuration with gate thresholds, warning thresholds, named owners, and escalation policy | The first alert is configured |
| [T-11 Regression Suite Coverage Audit](./T-11-regression-suite-coverage-audit.md) | Coverage gap identification per taxonomy tag, suite tier configuration, and media blob registry with SHA-256 manifest | Wiring the CI gate |
| [T-12 CI Gate Policy](./T-12-ci-gate-policy.md) | Blocking conditions, review-flagged conditions, false positive handling protocol, and suppression log | The gate fires for the first time |

### Diagnosis and Decisions

| Template | Purpose | Use When... |
|---|---|---|
| [T-13 Driver Analysis Template](./T-13-driver-analysis-template.md) | Structured root-cause analysis — five pipeline hypotheses, confirmed cause, intervention, validation plan, rollback plan | Any monitoring alert fires |
| [T-14 Decision Memo](./T-14-decision-memo.md) | Evidence-backed Ship / Ramp / Hold / Rollback record with pre-committed reversal conditions | Any significant ship or ramp decision |

### Experiments and Data

| Template | Purpose | Complete Before... |
|---|---|---|
| [T-15 Experiment Pre-Registration](./T-15-experiment-pre-registration.md) | Committed hypothesis, randomisation unit, primary metric, novelty exclusion window, and decision rule | Any A/B experiment launches |
| [T-16 Dataset Record](./T-16-dataset-record.md) | Versioned dataset metadata including modality coverage, taxonomy coverage, source breakdown, and media blob registry | Creating or versioning any evaluation dataset |

### Prioritization and Governance

| Template | Purpose | Use When... |
|---|---|---|
| [T-17 Backlog Prioritization Table](./T-17-backlog-prioritization-table.md) | Six-dimension priority formula (Severity × Frequency × Confidence × Blast Radius × Upstream-ness ÷ TTL) with blast radius worksheet and sprint planning output | After error analysis is complete |
| [T-18 Evaluation Debt Register](./T-18-evaluation-debt-register.md) | Quarterly audit across seven debt categories — rubrics, evaluators, datasets, cadences, taxonomy gaps, production incident lag, gate suppressions | First week of every quarter |

---

## The Five Quality Contracts

Every evaluator template (T-05 through T-09) maps to one of the five contracts. Every other template references these contracts by number.

| Contract | The Core Question | Evaluator |
|---|---|---|
| 1 — Ingestion Fidelity | Did the pipeline faithfully extract what was in the source? | [T-05](./T-05-ingestion-fidelity-evaluator.md) |
| 2 — Faithfulness | Is the output traceable to the sources? | [T-06](./T-06-faithfulness-evaluator.md) |
| 3 — Factuality | Is the output correct about the real world? | [T-07](./T-07-factuality-evaluator.md) |
| 4 — Cross-Modal Consistency | Do the output modalities agree with each other? | [T-09](./T-09-cross-modal-consistency-evaluator.md) |
| 5 — Output Quality | Is the production quality adequate per medium? | [T-08](./T-08-audio-quality-evaluator.md) |

---

## How Templates Flow Together

The templates are not independent — they form a dependency chain. Completing them in order means each template has the information it needs.

```
T-01 Evaluation Brief
  └──► T-02 Quality Statement
         └──► T-10 Gate Thresholds and Alert Rules
         └──► T-14 Decision Memo (baseline values)
         └──► T-15 Experiment Pre-Registration (guardrail thresholds)

T-03 Architecture Worksheet
  └──► T-04 Logging Schema (fields depend on architecture choices)

T-04 Logging Schema
  └──► T-11 Regression Suite (media blob registry format)
  └──► T-16 Dataset Record (blob registry)
  └──► T-18 Debt Register Section 6 (instrumentation gaps)

Error Analysis (from guides/field-manual.md Ch 4)
  └──► T-05 through T-09 Evaluator Prompts (calibration examples)
  └──► T-11 Regression Suite Coverage Audit (taxonomy tags)
  └──► T-17 Backlog Prioritization (failure tags and causal chains)

T-05–T-09 Evaluator Prompts
  └──► T-10 Gate Thresholds (kappa requirements per evaluator)
  └──► T-12 CI Gate Policy (which evaluators run in fast vs full gate)
  └──► T-18 Debt Register Section 3 (evaluator calibration status)

T-12 CI Gate Policy
  └──► T-18 Debt Register Section 7 (suppression log review)

T-13 Driver Analysis
  └──► T-04 Logging Schema (instrumentation gaps identified)
  └──► T-11 Regression Suite (regression cases added post-resolution)
  └──► T-17 Backlog (confirmed interventions prioritized)
```

---

## Template Completion Rules

**Rule 1 — T-01 before everything.**
The Evaluation Brief must be signed before any other template is completed. Every threshold in every other template flows from the agreements made in T-01.

**Rule 2 — Thresholds before scores.**
Fill in T-02 (Quality Statement) before running any evaluations. Teams that measure first and set thresholds after anchor to what they already built — not to what users need.

**Rule 3 — T-12 before the gate fires.**
Document the CI Gate Policy before the first false positive occurs, not after. Once the gate fires and someone is under deadline pressure, the policy gets improvised. Improvised policies create undocumented suppressions.

**Rule 4 — T-15 before data is collected.**
The Experiment Pre-Registration must be archived with a timestamp before the experiment launches. Any deviation from the pre-committed decision rule must be documented and reviewed. The value of pre-registration collapses if results can change the rule.

**Rule 5 — T-18 every quarter without exception.**
The Evaluation Debt Register is the maintenance record of your evaluation program. A program that is not audited quarterly decays silently — judges go uncalibrated, regression suites go stale, and the taxonomy from three months ago stops reflecting current failures.

---

## The 23 Standard Failure Tags

These tags appear in T-11, T-16, and T-18. Every taxonomy-aware template uses this shared set. Add product-specific tags below these — do not replace them.

```
INGESTION LAYER
  ingestion.[type].dropped_caption
  ingestion.[type].layout_scramble
  ingestion.ocr.scanned_drop
  ingestion.ocr.handwriting
  ingestion.asr.term_miss
  ingestion.asr.silence_hallucination

RETRIEVAL + GROUNDING
  retrieval.modality_bias
  retrieval.visual_chunk_dropped
  grounding.faithfulness_break
  grounding.speaker_attribution
  grounding.cross_source_merge

GENERATION
  generation.fabricated_quote
  generation.invented_statistic

CROSS-MODAL
  cross_modal.output_mismatch
  cross_modal.speaker_drift

OUTPUT SYNTHESIS
  output.audio.mispronunciation
  output.audio.prosody_flat
  output.audio.script_drift
  output.visual.layout_overlap
  output.visual.taxonomic_error
  output.visual.concept_gap

SAFETY
  safety.pii_in_output
  safety.copyright_reproduction
```

---

## Reference Quality Bars

Use these as starting points. Set your own bars based on your domain and user stakes before running any evaluations.

| Contract | Baseline Bar | Strong Bar | Immediate Rollback Example |
|---|---|---|---|
| Ingestion Fidelity | ≥ 95% on clean docs | ≥ 98% | Parse failure on any supported file type |
| Faithfulness | ≥ 93% claims traceable | ≥ 97% | Fabricated quote with named attribution |
| Factuality | ≥ 90% verifiable claims | ≥ 97% | Domain-specific factual catastrophe |
| Cross-Modal Consistency | ≤ 2 mismatches / 10 min | ≤ 1 / 10 min | Both modalities assert the same fabricated finding |
| Audio Quality (MOS) | ≥ 3.8 | ≥ 4.2 | Silence gap > 5 seconds |

---

## Template Versioning

Every template you complete should be version-controlled alongside the evaluation run that used it.

- Tag each completed template with the feature name and date: `T-01_product-name_2026-04.md`
- Never edit a threshold retroactively after evaluation runs have referenced it
- Increment the version number any time a threshold changes
- Archive completed templates — they are the audit trail of your evaluation program

---

## Finding the Right Template Fast

| I need to... | Template |
|---|---|
| Align my team on what "good" means | [T-01](./T-01-evaluation-brief.md) |
| Specify thresholds for my monitoring system | [T-02](./T-02-quality-statement.md) |
| Compare architecture options before building | [T-03](./T-03-architecture-worksheet.md) |
| Know what to log and what to store | [T-04](./T-04-logging-schema.md) |
| Build an evaluator for ingestion quality | [T-05](./T-05-ingestion-fidelity-evaluator.md) |
| Build an evaluator for faithfulness | [T-06](./T-06-faithfulness-evaluator.md) |
| Build an evaluator for factuality | [T-07](./T-07-factuality-evaluator.md) |
| Build an evaluator for audio quality | [T-08](./T-08-audio-quality-evaluator.md) |
| Build an evaluator for cross-modal consistency | [T-09](./T-09-cross-modal-consistency-evaluator.md) |
| Set up production monitoring alerts | [T-10](./T-10-gate-thresholds-alert-rules.md) |
| Check regression suite coverage | [T-11](./T-11-regression-suite-coverage-audit.md) |
| Document my CI gate policy | [T-12](./T-12-ci-gate-policy.md) |
| Investigate a production alert | [T-13](./T-13-driver-analysis-template.md) |
| Document a ship/hold/rollback decision | [T-14](./T-14-decision-memo.md) |
| Run an A/B experiment on an output modality | [T-15](./T-15-experiment-pre-registration.md) |
| Track an evaluation dataset | [T-16](./T-16-dataset-record.md) |
| Prioritize my backlog of fixes | [T-17](./T-17-backlog-prioritization-table.md) |
| Run my quarterly governance review | [T-18](./T-18-evaluation-debt-register.md) |

---

*All templates are starting points. Adapt every threshold, rubric, and failure tag to your product, your domain, and your users. A template completed before the work is an anchor. A template completed after is a record.*

