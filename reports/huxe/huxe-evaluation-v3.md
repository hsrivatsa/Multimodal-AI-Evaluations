# Huxe Audio Intelligence
## Multimodal AI Product Evaluation Report — v3 Pilot Protocol
### Applying the Practitioner's Field Manual · Tooling: Braintrust
*April 2026 — Evaluator: AI Solutions Architect*

---

## A Note on Evidence Provenance

Every score, kappa value, count, and percentage in this report carries one of four evidence labels. This labeling is not a disclaimer — it is a methodological commitment. A simulated score treated as empirical data is worse than no score, because it gives false confidence.

| Label | What It Means |
|---|---|
| **[SIM]** | Simulated — derived from structured reasoning about the product, not actual trace access |
| **[EST]** | Estimated — calibrated against public data sources (reviews, architecture patterns, industry benchmarks) |
| **[REV]** | Review-derived — directly supported by published App Store, Google Play, or press reviews |
| **[INF]** | Architectural inference — derived from known patterns in similar multimodal pipeline systems |

**Why this matters for Huxe specifically:** This evaluation was conducted without production trace access. The failure patterns, taxonomy, and causal chains are architecturally credible and grounded in public evidence — but the specific percentages and counts should be treated as *calibrated starting hypotheses for a real pilot*, not as audited product metrics. When Huxe's team runs this protocol with real traces, these numbers will change. The framework will hold.

---

## Executive Summary

This report documents a structured evaluation of **Huxe**, the audio-first personal intelligence platform built by the former NotebookLM team. Huxe ingests a user's emails, calendar, news feeds, and interest topics, then synthesizes them into personalized multi-speaker audio briefings users can interrupt and interact with in real-time.

The evaluation follows the Multimodal AI Product Evaluation Field Manual end-to-end, using **Braintrust** as the no-code evaluation platform for dataset management, evaluator deployment, scoring, and trace review.

**The central architectural insight driving this evaluation:** Huxe is not a closed-world faithfulness system like NotebookLM. NotebookLM operates on user-selected documents — the source material is known, bounded, and controlled. Huxe operates on a user's entire inbox, calendar, and live news feeds — the source material is open-world, highly variable, personally sensitive, and constantly changing. This distinction changes the evaluation method entirely. Standard source-grounding checks are necessary but not sufficient. Huxe also requires temporal accuracy checks, personalization fidelity tests, privacy appropriateness evaluation, and audio-native review that goes beyond transcript analysis.

**Overall finding:** Huxe's audio quality and interactive experience are genuinely competitive, but the product carries structurally significant risks in its primary trust surface — the user's inbox. The ingestion, faithfulness, and privacy contracts are under the most pressure and deserve the deepest evaluation investment before any major ramp.

---

## Section 1: Product Understanding

### What Huxe Is

Huxe is an audio-first personal intelligence platform. It does three things:

| Feature | What It Does |
|---|---|
| **Daily Briefings** | Synthesizes emails, calendar events, and news into a personalized morning audio session |
| **Live Stations** | User-defined topic channels (e.g., "AI News," "My Industry") that update continuously |
| **On-Demand Podcasts** | User asks about any topic; Huxe generates a dual-host conversational podcast on it |

The interactive interruption layer is what sets Huxe apart: users can interrupt mid-audio to ask questions, redirect the hosts, or request simpler explanations — and the audio responds in real-time without repeating already-covered content. This is a live generative system, not a pre-rendered file, which creates evaluation surfaces that don't exist in most audio products.

### Huxe vs. NotebookLM — Why the Distinction Matters for Evaluation

| Dimension | NotebookLM | Huxe |
|---|---|---|
| **Source material** | User-selected documents (closed world) | User's entire inbox + calendar + live news (open world) |
| **Source variability** | Low — user controls what goes in | Extreme — every user has a completely different email mix |
| **Primary faithfulness risk** | Misrepresenting a document the user uploaded | Misrepresenting something the user received but didn't consciously "add" |
| **Privacy surface** | User-uploaded content only | Personal communications, financial data, medical info, legal matters |
| **Temporal accuracy** | Static documents | Live calendar events with specific dates, times, and attendees |
| **Evaluation approach** | Source-grounding checks primary | Source-grounding + temporal accuracy + personalization fidelity + contextual privacy |

This comparison explains why the evaluation design here differs substantially from a standard audio summarization eval.

### The Multimodal Profile

| Dimension | Details |
|---|---|
| **Input modalities** | Email (text/HTML), Calendar (structured), News feeds (web text), Twitter/X (social), User voice interruptions |
| **Output modalities** | Audio (primary — dual-speaker synthesized podcast), Synchronized on-screen transcript overlay |
| **Cross-modal contract** | Audio narration must match the on-screen transcript updating in real-time |
| **Interaction layer** | Live voice/text interruption mid-stream — a real-time generative system with state memory |

### The Nine-Stage Pipeline Mapped to Huxe

```
Stage 1 — Ingestion:     Read emails (plain text + HTML), calendar
                          entries, RSS/news feeds, Twitter feed,
                          user interest settings
Stage 2 — Normalization: Chunk email threads; extract calendar
                          context; rank by relevance and recency;
                          deduplicate cross-source stories
Stage 3 — Indexing:      Store processed content in vector store
Stage 4 — Retrieval:     Find relevant content for today's briefing
                          based on user profile and interest graph
Stage 5 — Reasoning:     Assemble script context; resolve what's
                          "new" vs. "already covered today"
Stage 6 — Generation:    Generate dual-host podcast script
Stage 7 — Synthesis:     Convert script to audio via TTS;
                          maintain host voice consistency
Stage 8 — Guardrails:    PII detection; content filtering;
                          copyright detection; privacy screening
Stage 9 — Delivery:      Stream audio to iOS/Android; sync
                          transcript display; handle interruptions
                          and maintain state post-interruption
```

---

## Section 2: The Judge Panel — With Full Multi-Rater Protocol

The v1 report named four judges but acknowledged that one evaluator played all four roles in the exercise. This section describes how a production-grade multi-rater protocol would be structured, including the adjudication process that matters most when judges disagree.

### The Four Judges

| Role | Profile | Jurisdiction | What They Are NOT Judging |
|---|---|---|---|
| **Content Judge** | Senior journalist or editor with AI coverage experience | Factual accuracy; claim grounding; calendar accuracy; tense fidelity; sender attribution | Audio naturalness; transcript timing |
| **Ingestion Judge** | ML/data engineer with email parsing and NLP pipeline experience | Email thread retention; HTML parsing; calendar completeness; ranking signal quality | Audio quality; factual accuracy |
| **Audio Judge** | Podcast producer with AI-generated audio production experience | Voice naturalness; host differentiation; prosodic appropriateness; pronunciation; interruption recovery feel; pacing | Factual claims; transcript timing |
| **Visual/UX Judge** | Mobile UX designer with real-time media experience | Transcript-audio sync timing; readability of on-screen updates; visual pacing relative to speech | Audio quality; content accuracy |
| **Tiebreaker** | Product Lead | Final authority when panel disagrees; also names zero-tolerance thresholds | — |

### The Multi-Rater Labeling Protocol

This is the protocol for the exercise. In a real evaluation, each judge works independently on their contract domain.

**Step 1 — Blind independent labeling.** Each judge labels 60 traces within their jurisdiction without seeing other judges' labels or automated scorer outputs.

**Step 2 — Agreement measurement.** Cohen's kappa measured per judge pair for any claim that overlaps jurisdiction (e.g., the Content Judge and Ingestion Judge may both flag the same email faithfulness failure but for different reasons).

**Step 3 — Disagreement review.** Any trace where two judges give conflicting labels goes to a 30-minute structured adjudication session. The adjudication outcome and rationale are logged in the dataset record — disagreements are treated as the most valuable signal for rubric refinement.

**Step 4 — Tiebreaker escalation.** If adjudication doesn't resolve the disagreement (rare — typically < 5% of traces), the Product Lead makes the final call and documents why.

**Why this matters for Huxe:** The Content Judge and Audio Judge are likely to disagree on tense-collapse failures. The Content Judge will flag "the email says future tense; the audio said past tense" as a faithfulness failure. The Audio Judge may flag the same event as a "natural narrative simplification." That disagreement is not noise — it is a specification question about what Huxe promises users, and it needs to be resolved before any evaluator is deployed.

---

## Section 3: The Evaluation Brief

*Completed before running a single evaluation. All thresholds below are [SIM] — set before seeing any scores, based on product analysis and industry reference bars from the Field Manual.*

```
╔══════════════════════════════════════════════════════════╗
║            HUXE EVALUATION BRIEF — v1.0                  ║
╠══════════════════════════════════════════════════════════╣
║ Feature: Daily Briefing + Live Stations + On-Demand      ║
║ Date: April 2026                                          ║
╠══════════════════════════════════════════════════════════╣
║ JUDGE PANEL                                               ║
║   Content: Senior Journalist / News Editor               ║
║   Ingestion: ML Engineer (email/web parsing)             ║
║   Audio: Podcast Producer (AI audio experience)          ║
║   Visual: Mobile UX Designer                             ║
║   Tiebreaker: Product Lead                               ║
╠══════════════════════════════════════════════════════════╣
║ MODALITIES                                                ║
║   Inputs:  [x] Email  [x] Calendar  [x] Web/News         ║
║            [x] Social (Twitter/X)  [x] User voice         ║
║   Outputs: [x] Audio  [x] Text (transcript overlay)      ║
╠══════════════════════════════════════════════════════════╣
║ USER JOB:                                                 ║
║ "When I start my day or commute, I want a personalized   ║
║ audio briefing that covers what matters to me — my       ║
║ emails, my calendar, and the news I care about — so I    ║
║ can stay informed and prepared without looking at a      ║
║ screen."                                                  ║
╠══════════════════════════════════════════════════════════╣
║ WHAT "GOOD" FEELS LIKE:                                   ║
║   Audio: "Two knowledgeable colleagues discussing my     ║
║   day — not a robot reading my inbox."                   ║
║   Transcript: "The words on screen match what I'm        ║
║   hearing, appearing exactly when they're spoken."        ║
╠══════════════════════════════════════════════════════════╣
║ CONTRACT 1 — INGESTION FIDELITY                          ║
║   Email parse (plain text):        ≥ 97%                 ║
║   Email parse (HTML newsletters):  ≥ 90%                 ║
║   Calendar event accuracy:         ≥ 99%                 ║
║   Thread context retention:        ≥ 85%                 ║
║   Zero-tolerance: Any HIPAA-class data, financial        ║
║   account numbers, or passwords passing through          ║
║   to audio output                                         ║
╠══════════════════════════════════════════════════════════╣
║ CONTRACT 2 — FAITHFULNESS (output ↔ sources)             ║
║   Email content faithfulness:      ≥ 95%                 ║
║   News content faithfulness:       ≥ 93%                 ║
║   Calendar accuracy:               ≥ 99%                 ║
║   Zero-tolerance:                                         ║
║     1. Invented meeting not in calendar spoken as fact   ║
║     2. Fabricated quote attributed to a named sender     ║
╠══════════════════════════════════════════════════════════╣
║ CONTRACT 3 — FACTUALITY (output ↔ world)                 ║
║   News factual accuracy:           ≥ 92%                 ║
║   Named entity accuracy:           ≥ 97%                 ║
║   Zero-tolerance: Wrong date/time for a user's actual    ║
║   calendar event stated in the briefing                  ║
╠══════════════════════════════════════════════════════════╣
║ CONTRACT 4 — CROSS-MODAL CONSISTENCY                     ║
║   Audio-transcript sync offset:    ≤ 1.5 seconds        ║
║   Audio-transcript content match:  ≥ 98%                ║
║   Zero-tolerance: Transcript and audio state different   ║
║   substantive facts (not just timing difference)         ║
╠══════════════════════════════════════════════════════════╣
║ CONTRACT 5 — OUTPUT QUALITY                              ║
║   Audio MOS target:                ≥ 4.0                 ║
║   Proper noun pronunciation:       ≥ 88%                 ║
║   Audio glitch rate:               ≤ 1 per 10 min       ║
║   Host voice consistency:          ≥ 95% (no drift)     ║
║   Interruption recovery quality:   ≥ 85% (audio-native) ║
╠══════════════════════════════════════════════════════════╣
║ CONSUMPTION TARGETS                                       ║
║   Daily briefing listen-through:   ≥ 65% (7-day cohort) ║
║   Live station session length:     ≥ 5 minutes           ║
║   Return next morning:             ≥ 50%                 ║
╠══════════════════════════════════════════════════════════╣
║ DECISION IN NEXT 2–4 WEEKS: HOLD                         ║
╠══════════════════════════════════════════════════════════╣
║ RISKIEST ASSUMPTION:                                      ║
║ "If users don't trust that their email content is        ║
║ handled accurately and privately, the product is         ║
║ useless."                                                ║
║ Test method: Beta survey after 7 days + PII audit on     ║
║ 50 sessions + faithfulness eval on email summaries      ║
╚══════════════════════════════════════════════════════════╝
```

---

## Section 4: Surface Mapping

*Output of the Ten-Trace Exercise. Evidence label: [SIM] for failure descriptions; [REV] where confirmed by App Store or press reviews.*

### The Full Surface Map

| Surface | Modality | Most Likely Failure | Evidence Label | Owner |
|---|---|---|---|---|
| Email Parser | Text | Thread collapse — only last message read; HTML newsletter formatting garbles extraction | [SIM]+[REV] | Ingestion Eng |
| Calendar Parser | Structured | Attendee list dropped; timezone errors on recurring events | [SIM] | Ingestion Eng |
| News Feed Fetcher | Web | Stale articles; paywalled content partially extracted | [INF] | Ingestion Eng |
| Content Ranker | Cross | Promotional emails ranked over high-signal personal ones | [REV] | ML Eng |
| Chunker | Cross | Long threads split mid-argument; context lost across boundary | [INF] | Data Eng |
| Generator | Text | Gap-filling when context thin; invents bridging content | [SIM] | ML Eng |
| Script Deduplication | Text | Same story from multiple sources appears twice mid-briefing | [REV] | ML Eng |
| TTS Synthesis | Audio | Mispronounces sender names, VC firm names, tech terms | [REV] | Audio Eng |
| Host Voice Drift | Audio | Host A and Host B become indistinguishable over long sessions | [SIM] | Audio Eng |
| Interruption Handler | Cross | Hosts repeat content already covered after user interrupts | [REV] | ML Eng |
| Transcript Sync | Cross-modal | On-screen text lags or leads audio by > 1.5 seconds | [SIM] | Mobile Eng |
| PII Guardrail | Safety | Financial data, contact details, sensitive context from email passes to audio | [REV]+[SIM] | Safety/Policy |
| CDN Delivery | Audio | Audio stops around 2/3 mark | [REV] | Platform Eng |

### Top 5 Highest-Risk Surfaces

| Surface | Why High-Risk | Early Warning Signal |
|---|---|---|
| **Email Parser** | The most variable, sensitive input in any consumer app — threads, HTML, attachments, every format imaginable | Faithfulness drops on email-heavy sessions vs. news-only sessions |
| **PII Guardrail** | Professional users explicitly cited security concerns; lawyers, doctors noted they wouldn't connect work email | Any PII instance in audio = zero-tolerance breach |
| **Generator (Gap-Filling)** | When email context is thin, the model bridges gaps with plausible-sounding invented details | "Unsupported" label rate > 5% on email briefings |
| **Interruption Handler** | Real-time interruption is the core product differentiator — if it repeats or loses thread, the moat disappears | Duplicate content rate > 10% after interruption [REV] |
| **TTS Pronunciation** | User briefings contain sender names and niche company names the TTS model has never seen | Entity pronunciation accuracy below 85% [REV] |

---

## Section 5: Error Analysis — The Taxonomy

*Based on 30 structured trace simulations [SIM] across three user profiles, calibrated against published reviews [REV] and pipeline architecture patterns [INF].*

**User profiles:**
- **Profile A:** Heavy email professional (lawyer) — 40+ emails/day, calendar-dense, multiple threads
- **Profile B:** News junkie — Twitter connected, 5 RSS feeds, light personal email
- **Profile C:** Casual user — personal Gmail, no work email, 2–3 interest topics

### Open Coding Highlights (Selected Notes)

*All notes below are [SIM] unless marked [REV]. They represent architecturally plausible failure patterns, not transcripts of actual Huxe sessions.*

- *"Briefing described a meeting as 'your 3pm call with the team' — it is actually a 1:1 with a named person. Calendar event title was read; attendee list dropped."* → Stage 1; appears in: Audio [SIM]
- *"Host A said 'the company announced record profits.' The email said 'expects to announce results next quarter.' Classic tense collapse."* → Stage 6; appears in: Audio [SIM]
- *"Same AI product launch covered twice, six minutes apart, by two different newsletter sources. No deduplication."* → Stage 5; appears in: Audio [REV — confirmed by user reviews]
- *"Host said 'Andreessen Horowitz' as four unrelated syllables. Jarring and trust-damaging."* → Stage 7; appears in: Audio [REV — name-pronunciation failures widely noted]
- *"Transcript showed 'GPT-5 announced' while audio said 'GPT-4 announced.' Content mismatch, not timing."* → Stage 6/7; appears in: Audio + Transcript [SIM]
- *"After user interrupted to ask a question, hosts restarted: 'So as we were saying about the Fed rate decision...' and repeated three sentences verbatim."* → Stage 9; appears in: Audio [REV — confirmed in reviews]
- *"Email newsletter contained user's account balance. It was read aloud in the briefing."* → Stage 8; appears in: Audio [SIM — ZERO-TOLERANCE BREACH]*

### Huxe Failure Taxonomy v0.1

```
INGESTION LAYER
  ingestion.email.thread_collapse    — only last message read; full context lost [SIM]
  ingestion.email.html_garble        — HTML formatting disrupts extraction [INF]
  ingestion.email.attachment_blind   — PDF/doc attachments not ingested [INF]
  ingestion.calendar.attendee_drop   — attendee list absent; only title/time retained [SIM]
  ingestion.calendar.timezone_error  — wrong timezone applied to event [INF]

RETRIEVAL + GROUNDING
  retrieval.email_ranking_noise      — promotional email ranked over personal [REV]
  retrieval.dedup_failure            — same story appears twice mid-session [REV]
  grounding.email_faithfulness_break — audio claim not traceable to email [SIM]
  grounding.calendar_invented        — meeting detail not in calendar stated as fact [SIM]
  grounding.tense_collapse           — future event stated as past/present fact [SIM]

GENERATION
  generation.gap_fill                — model invents context to bridge thin email content [SIM]
  generation.sender_attribution      — claim attributed to wrong sender [SIM]

CROSS-MODAL
  cross_modal.transcript_content_mismatch — transcript and audio state different facts [SIM]
  cross_modal.transcript_sync_lag    — transcript visibly lags audio > 1.5 seconds [SIM]
  cross_modal.interruption_repeat    — hosts repeat covered content post-interruption [REV]

OUTPUT SYNTHESIS
  output.audio.entity_mispronunciation  — names, VC firms, tech terms mispronounced [REV]
  output.audio.host_voice_drift         — Host A and B become indistinguishable [SIM]
  output.audio.delivery_drop            — audio stops ~2/3 mark [REV]
  output.audio.pacing_flat              — both hosts deliver in identical monotone [SIM]
  output.audio.interruption_recovery_lag — post-interruption audio feels awkward [SIM]

SAFETY
  safety.pii_hard_pattern            — financial data, passwords, phone numbers in audio [SIM]
  safety.pii_contextual_leakage      — sensitive relationship/health/legal context in audio [SIM]
  safety.contact_detail_exposure     — sender address or phone read aloud [SIM]
```

### Count — By Junction (30 traces) [SIM]

*All counts are simulation-derived estimates. In a real pilot, recalibrate against actual trace data before acting on these proportions.*

| Junction | Count [SIM] | % of Failures | Implication |
|---|---|---|---|
| Ingestion layer | 28 | 31% | Email parsing is the primary battleground |
| Retrieval + grounding | 22 | 24% | Faithfulness and deduplication are systematic |
| Generation | 14 | 15% | Gap-filling is a real risk on thin email content |
| Output synthesis | 18 | 20% | TTS entity pronunciation consistently flagged |
| Cross-modal | 9 | 10% | Transcript sync and interruption repeats visible |
| Safety | 2 | 2% | Low frequency, catastrophic when it occurs |
| **Total** | **93** | **100%** | |

### Top 10 Failure Tags [SIM]

| Tag | Count [SIM] | % of Traces | In a Causal Chain? |
|---|---|---|---|
| `output.audio.entity_mispronunciation` | 19 | 63% | Sometimes |
| `ingestion.email.thread_collapse` | 16 | 53% | Yes — feeds faithfulness_break |
| `retrieval.dedup_failure` | 14 | 47% | No — standalone |
| `grounding.email_faithfulness_break` | 12 | 40% | Yes — downstream of thread_collapse |
| `output.audio.delivery_drop` | 11 | 37% | No — infrastructure |
| `grounding.tense_collapse` | 10 | 33% | No — standalone |
| `cross_modal.interruption_repeat` | 9 | 30% | No — state management |
| `ingestion.calendar.attendee_drop` | 8 | 27% | Yes — feeds calendar_invented |
| `cross_modal.transcript_sync_lag` | 7 | 23% | No — delivery/sync |
| `safety.pii_hard_pattern` | 2 | 7% | No — zero-tolerance override |

### Key Causal Chain [SIM]

```
Chain HC-01 (estimated in 12 of 30 simulated traces):
  ingestion.email.thread_collapse
    → grounding.email_faithfulness_break

  Story: Huxe reads only the last message in a thread,
  losing earlier context. The generator produces a summary
  of "what this email is about" that is accurate for the
  final message but misrepresents the full exchange.
  A user hears a confident summary that omits the most
  important prior context.

  FIX AT: ingestion.email.thread_collapse
  Expected lift: ~70% of email faithfulness failures
  resolve simultaneously [SIM — to be validated in pilot]
```

---

## Section 6: Evaluators in Braintrust

*Evaluator designs below are [SIM] — structured protocol designs that have not yet been run against real Huxe traces. Kappa values marked [SIM-EST] are calibrated estimates based on analogous evaluator performance in similar multimodal products.*

### How Braintrust Would Be Configured

- **Dataset:** All traces stored as Braintrust Datasets with structured input/output columns
- **Scorers:** Four evaluators deployed as Braintrust custom Scorers
- **Kappa measurement:** Inter-rater agreement measured using Braintrust's comparison view against human judge labels
- **Trace review:** Braintrust trace view used to walk each session span-by-span, including audio playback alongside transcript

### Evaluator 1 — Email Faithfulness Scorer

```
Scorer name: huxe_email_faithfulness_v1
Model:        claude-3-5-sonnet
              (different family from Huxe's assumed generator)
Input fields: email_content, audio_claim, claim_timestamp
Output:       {label: "supported"|"contradicted"|"unsupported",
               reasoning: str, evidence: str}
Calibration:  5 examples (supported, fabricated meeting,
               tense collapse, thread miss, sender attribution)
```

**Kappa estimate:** ~0.80 [SIM-EST — based on analogous email faithfulness evaluators in similar pipelines]
*Target: ≥ 0.80 to clear for CI gating. This is a key threshold to validate in the real pilot.*

### Evaluator 2 — Entity Pronunciation Scorer

```
Scorer name: huxe_pronunciation_v1
Model:        GPT-4o (audio input capability)
Input fields: audio_clip_base64, entity_reference_list
Output:       {pass_fail: bool, mispronounced: [str],
               reasoning: str}
Entity list:  VC firm names, common sender surnames,
              tech company names, product acronyms
```

**Kappa estimate:** ~0.75 [SIM-EST — pronunciation evaluation is harder to calibrate than faithfulness; this is expected to need multiple calibration rounds]
*Deploy for monitoring only until ≥ 0.80 kappa is confirmed with human labels.*

### Evaluator 3 — Transcript-Audio Consistency Scorer

```
Scorer name: huxe_transcript_consistency_v1
Model:        claude-3-5-sonnet
Input fields: audio_transcript_text, screen_transcript_text,
              timestamp_window
Output:       {consistent: bool, content_mismatches: [str],
               severity: "central"|"peripheral"|"na"}
```

**Kappa estimate:** ~0.82 [SIM-EST — content mismatch detection is well-defined; higher kappa expected]
*Clear for CI gating if confirmed in pilot.*

### Evaluator 4 — PII Hard-Pattern Scorer (Rule-Based)

```
Scorer name: huxe_pii_hard_v1
Type:         Deterministic regex — not LLM-based
Patterns:     16-digit card numbers, "password:" prefix,
              dollar amounts > $1,000 in email context,
              phone numbers in signature context,
              email addresses in signature context
Sensitivity:  Designed to catch 10/10 planted instances [SIM]
```

*This evaluator handles hard-pattern PII only. See Evaluator 5 for contextual privacy.*

### Evaluator 5 — Contextual Privacy Scorer (NEW — not in v1)

*This evaluator did not exist in the previous version and addresses the most significant gap identified in peer review.*

**The gap Evaluator 4 doesn't cover:** Regex catches account numbers and passwords. It does not catch:
- A user's medical appointment details read aloud to anyone who can hear their phone
- An email thread about a strained relationship with a colleague, summarized as briefing content
- A legal dispute with a contractor, synthesized into a morning update
- A salary negotiation email, surfaced in a briefing
- An embarrassing personal email, discussed by AI hosts in podcast format

These are not hard-pattern PII. They are **contextually sensitive** — information the user might share in private but would not want synthesized into an audio experience audible to others.

```
Scorer name: huxe_pii_contextual_v1
Model:        claude-3-5-sonnet (with explicit sensitivity rubric)
Input fields: email_content_type, audio_segment_text,
              sensitivity_context (medical/legal/financial/
              personal/professional)
Output:       {appropriate_to_surface: bool,
               sensitivity_category: str,
               reasoning: str,
               recommended_handling: "summarize_abstract"|
                                     "skip"|"surface_with_consent"}
```

**Special handling options the evaluator scores for:**
- **Summarize abstract:** "You have a message about a health appointment" — not "your cardiologist appointment for Tuesday is at 2pm"
- **Skip entirely:** "There are messages in your inbox that I'll leave for you to review privately"
- **Surface with consent:** For borderline cases, Huxe could prompt: "I noticed some sensitive messages — include them in your briefing?"

**Kappa expectation:** 0.65–0.70 initially [SIM-EST]. Contextual privacy is harder to calibrate than factual accuracy. Multiple calibration rounds with real user feedback are needed before this evaluator is CI-gated. Start as a monitoring-only scorer.

---

## Section 7: Audio-Native Evaluation (NEW — not in v1)

*This entire section addresses the most substantive structural gap identified in peer review: the v1 report was too transcript-centered for an audio-first product.*

### Why Transcript Review Is Not Enough for Huxe

Evaluating Huxe only through its transcript is like reviewing a restaurant by reading the menu. The transcript tells you what was said. It does not tell you:

- Whether the interruption recovery sounds natural or robotic
- Whether the transition from Host A to Host B feels like a conversation or a handoff
- Whether the pacing after a topic change sounds fluent or stitched
- Whether the user's question was "heard" and responded to smoothly, or whether the response felt canned
- Whether a 12-minute briefing feels engaging at the 10-minute mark, or whether the energy has deflated

These are audio-native qualities that require **listening**, not reading.

### The Audio-Native Review Loop

This loop runs in parallel with the transcript-based evaluation. It requires the Audio Judge working with actual audio playback — in Braintrust, this means using the audio playback feature in the trace view to listen alongside the transcript.

**Audio-Native Evaluation Dimensions:**

| Dimension | What the Audio Judge Is Listening For | Scoring Method |
|---|---|---|
| **Interruption recovery naturalness** | After a user interrupts and asks a question, does the resumed audio sound like a natural continuation or an awkward restart? | Pass/Fail per interruption event |
| **Host differentiation over time** | At the 5-minute mark vs. the 10-minute mark, do the two hosts still sound like distinct personalities or have they converged? | Likert 1–5 per session |
| **Prosodic appropriateness** | Is emphasis placed on the right words? Does the audio feel like someone who understands what they're saying, or pattern-matched speech synthesis? | Pass/Fail per 60-second segment |
| **Conversational latency feel** | After a user question, does the answer feel responsive or delayed? Does the response pacing feel live or pre-recorded? | Likert 1–5 per interruption |
| **Topic transition smoothness** | When the briefing moves from emails to news to calendar, does it feel like a coherent conversation or a content dump with seams? | Pass/Fail per transition |
| **Energy arc** | Does the audio maintain engagement across a 10-minute session, or does it feel like energy deflates after the first few minutes? | Likert 1–5 per full session |

### Audio-Native Failure Tags (Added to Taxonomy)

```
OUTPUT SYNTHESIS (Audio-Native Additions)
  output.audio.interruption_recovery_lag  — post-interruption audio feels robotic/restarted
  output.audio.host_convergence           — hosts sound identical mid-session
  output.audio.prosody_mismatch           — emphasis on wrong words; unnatural delivery
  output.audio.topic_seam                 — transition between content types audibly stitched
  output.audio.energy_deflation           — engagement drops in second half of long sessions
  output.audio.response_latency_feel      — answer to interruption feels canned/delayed
```

### Why This Changes the Backlog

Adding audio-native evaluation often reveals failures that transcript review misses and vice versa. A response to a user question might be *transcriptly accurate* (says the right thing) but *audio-natively poor* (sounds like a script being read, not a conversation being had). That is a different failure requiring a different fix surface — Voice/TTS and Topology rather than Generation or Prompt Engineering.

---

## Section 8: Quality Contract Scores

*All scores below are [SIM-EST] — simulation-derived estimates calibrated against public evidence and architecture patterns. They are hypotheses for a real pilot evaluation, not audited product metrics.*

| Contract | Score [SIM-EST] | Threshold | Status | Primary Issue |
|---|---|---|---|---|
| Ingestion Fidelity (email) | ~78% | ≥ 90% | 🔴 FAIL | Thread collapse; HTML garble |
| Ingestion Fidelity (calendar) | ~94% | ≥ 99% | 🟡 WARN | Attendee drop in ~6% of events |
| Faithfulness (email content) | ~72% | ≥ 95% | 🔴 FAIL | Downstream of ingestion failures |
| Faithfulness (news content) | ~89% | ≥ 93% | 🟡 WARN | Gap-fill on thin summaries |
| Factuality (named entities) | ~91% | ≥ 97% | 🟡 WARN | Company names, dates |
| Cross-modal consistency | ~85% | ≥ 98% | 🔴 FAIL | Transcript content mismatches |
| Audio MOS [EST] | ~3.9 | ≥ 4.0 | 🟡 WARN | Pacing flat in host-B voice |
| Pronunciation accuracy [REV] | ~71% | ≥ 88% | 🔴 FAIL | VC names, sender surnames |
| PII hard-pattern guardrail [SIM] | ~93% | = 100% | 🔴 FAIL | 2 estimated leakages / 30 sessions |
| Contextual privacy appropriateness | Not yet measured | = 100% | ⚪ NOT EVALUATED | New evaluator not yet deployed |
| Interruption recovery quality [SIM] | ~68% | ≥ 85% | 🔴 FAIL | Robotic restarts; post-interruption repeats |
| Listen-through % [REV] | ~61% | ≥ 65% | 🟡 WARN | Delivery drop confirmed in reviews |

**Note on the contextual privacy row:** This was not measured in v1 and is not measured here. It is added to make the gap visible. Until it is measured, this contract has an unknown score — which is itself a risk signal.

**Contracts passing:** 0 of 5. All five contracts have at least one failing metric.
**Zero-tolerance breaches:** 2 estimated hard-pattern PII leakages. Contextual privacy not yet assessed.

---

## Section 9: The Five Drifts

| Drift | Risk Level | Observation | Evidence Label |
|---|---|---|---|
| **Input Drift** | 🔴 HIGH | Every user has a completely different email mix — this isn't drift over time, it's baseline variability from day one. Standard drift detection doesn't apply; what's needed is stratified profile coverage from the start. | [INF] |
| **Ingestion Drift** | 🟡 MEDIUM | Gmail and Outlook update their HTML rendering standards. Email API changes could silently break parsing without any code change on Huxe's side. A daily canary against fixed email corpus is essential. | [INF] |
| **Model Drift** | 🟡 MEDIUM | LLM and TTS providers update models. Pronunciation and generation behavior will change without warning. Monthly kappa recalibration is the early-detection mechanism. | [INF] |
| **Judge Drift** | 🟢 LOW | Evaluators just designed; no drift observed yet. Monthly recalibration scheduled. | [SIM] |
| **Consumption Drift** | 🔴 HIGH | App Store reviews show strong day-1 engagement but clear risk of novelty decay. The 21-day minimum experiment window from the Field Manual is critical for Huxe. | [REV] |

---

## Section 10: Prioritized Backlog

*Using the Priority Score Formula: (S × F × C × B × U) ÷ TTL. All scores [SIM-EST].*

| # | Fix | Tag | S | F [SIM] | C | TTL | B | U | Score | Rank |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | PII hard-pattern guardrail hardening | `safety.pii_hard_pattern` | 3 | 0.07 | 3 | 1d | 1 | 2 | 1.26 | **Override → TOP** |
| 0b | Contextual privacy evaluator (build first) | `safety.pii_contextual_leakage` | 3 | unknown | 3 | 3d | 1 | 2 | **Unscored** | **Override → TOP** |
| 1 | Email thread context retention | `ingestion.email.thread_collapse` | 3 | 0.53 | 3 | 5d | 3 | 5 | 5.72 | **1** |
| 2 | Tense collapse prompt fix | `grounding.tense_collapse` | 2 | 0.33 | 2 | 2d | 1 | 3 | 1.98 | **2** |
| 3 | Pronunciation lexicon (entities) | `output.audio.entity_mispronunciation` | 2 | 0.63 | 3 | 2d | 1 | 2 | 1.89 | **3** |
| 4 | Deduplication logic | `retrieval.dedup_failure` | 2 | 0.47 | 3 | 3d | 1 | 4 | 1.88 | **4** |
| 5 | Interruption state manager | `cross_modal.interruption_repeat` | 3 | 0.30 | 2 | 7d | 2 | 2 | 0.51 | **5** |
| 6 | CDN delivery fix | `output.audio.delivery_drop` | 3 | 0.37 | 2 | 4d | 1 | 1 | 0.56 | **6** |
| 7 | Calendar attendee retention | `ingestion.calendar.attendee_drop` | 2 | 0.27 | 3 | 3d | 2 | 5 | 1.80 | **7** |
| 8 | Transcript sync pipeline | `cross_modal.transcript_sync_lag` | 2 | 0.23 | 2 | 5d | 1 | 2 | 0.37 | **8** |
| 9 | HTML email parser upgrade | `ingestion.email.html_garble` | 2 | 0.30 | 2 | 7d | 2 | 5 | 0.86 | **9** |

**New to v3:** Contextual privacy evaluation is added as a co-equal override with the PII hard-pattern fix. You cannot harden one without understanding the other. The contextual scorer needs to be built and at least monitoring-deployed before the PII sprint is declared complete.

**The key formula insight holds:** Email thread context retention (score 5.72) beats the pronunciation lexicon (1.89) despite being slower to build — because fixing thread collapse resolves the entire downstream faithfulness chain at Stage 1, while the pronunciation fix resolves only a single leaf-node failure at Stage 7.

---

## Section 11: Driver Analysis — The Faithfulness Gap

*[SIM] — Structured hypothesis analysis based on architecture reasoning and profile data, not live trace investigation.*

```
DRIVER ANALYSIS — Email Faithfulness ~72% [SIM-EST]
Date: April 2026

OBSERVED PATTERN [SIM-EST]:
  Metric: Email Faithfulness (Braintrust scorer)
  Magnitude: ~72% vs. threshold of 95% — ~23pp below target
  Modality: Audio (email-derived claims)
  Segments most affected: Profile A (heavy email/professional)
  Segments least affected: Profile C (light email/casual)

H1 (Ingestion): Thread collapse removes context the
  generator needs.
  Test: Run faithfulness evaluator on single-email
  sessions vs. thread sessions separately.
  Simulated result: Thread sessions ~61% faithful;
  single-email sessions ~88% faithful. 27pp gap. [SIM-EST]
  → CONFIRMED as primary driver.

H2 (Retrieval): Wrong emails ranked most relevant;
  promotional content dominates.
  Test: Compare content ranker output vs. human-intuitive
  importance ranking for 10 sessions.
  Simulated result: Partially confirmed — explains
  ranking quality, not faithfulness directly. [SIM]

H3 (Generation): Gap-filling when email context thin.
  Test: Compare faithfulness on sessions with > 500 words
  of email content vs. < 200 words.
  Simulated result: Short emails ~68% faithful;
  long emails ~79% faithful. [SIM-EST]
  → CONFIRMED as secondary amplifier.

H4 (Output Synthesis): TTS paraphrasing script.
  Test: Compare generated script to audio transcript.
  Simulated result: Script-to-audio fidelity ~97%.
  Not confirmed — problem is upstream. [SIM]

H5 (Distribution Shift): Professional users have
  more complex email patterns than test corpus.
  Test: Compare thread depth metrics across profiles.
  Simulated result: Profile A averages ~3.2 messages
  per thread; test corpus averages ~1.4. [SIM-EST]
  → CONFIRMED as amplifier — real users harder than
  our simulated test set.

CONFIRMED CAUSE: ingestion.email.thread_collapse (H1)
SECONDARY CAUSE: generation.gap_fill (H3)
AMPLIFIER: Distribution shift — professional users
  have deeper, more complex thread patterns (H5)

PRIMARY FIX: Ingestion — ingest full thread with role
  labels (sender, recipient, date per message)
SECONDARY FIX: Prompt — add graceful uncertainty
  instruction: fail with "not enough detail" rather
  than inventing bridging content

EXPECTED LIFT [SIM-EST]:
  Thread fix alone: ~72% → ~87%
  Thread fix + prompt fix: ~87% → ~93%
  Gap to 95% threshold: ~2pp — addressable in sprint 3

VALIDATION: Re-run email faithfulness scorer on 20
fresh traces after thread fix deployment. Confirm
≥ 10pp lift before next ramp stage.

NOTE ON EVIDENCE: All figures above are simulated
estimates derived from structured reasoning. The
27pp thread vs. single-email gap and the projected
+15pp lift are calibrated hypotheses, not measured
results. The pilot protocol exists to validate these
estimates against real data.
```

---

## Section 12: Decisions and Recommendations

### Ship / Hold / Ramp Decision

**Recommendation: HOLD**

Two zero-tolerance breach events (estimated PII leakage) and a ~23pp faithfulness gap on the most trust-critical contract make this clear. This is not a product with rough edges — it has a structural gap between what users trust it with and what it can safely and faithfully deliver today.

### Specific Recommended Actions

**Before anything else — this sprint:**

1. **Harden the PII hard-pattern guardrail.** Deploy enhanced regex + LLM-as-safety-judge combination. Sensitivity test: 10 planted PII samples, require 10/10 catch before any user-facing session continues.

2. **Build and deploy the contextual privacy evaluator.** This is not optional. The regex-only approach catches passwords and account numbers; it does not catch a user's medical appointment, salary negotiation, or strained relationship being synthesized into podcast content. The contextual scorer needs to be monitoring-deployed and generating alerts before the PII sprint is considered closed.

3. **Fix email thread context retention.** Ingest the full thread with role labels (sender, recipient, timestamp per message). Re-run Braintrust evaluation after deployment.

**Sprint 2:**

4. **Add graceful uncertainty to the generation prompt.** When email context is thin, the model should say "I don't have enough detail from this thread to summarize accurately" rather than inventing connecting tissue.

5. **Build the pronunciation lexicon.** Collect the 200 most common sender surnames and organization names from the user corpus. Add to TTS custom dictionary.

6. **Fix CDN delivery drop.** The audio stops at ~2/3 mark is confirmed in reviews. Investigate buffer preloading, chunk size, and stream timeout. A briefing that stops mid-sentence is worse than no briefing.

7. **Add audio-native evaluation loop.** Deploy the Audio Judge role with actual listening sessions using Braintrust's audio playback in the trace view. Measure the six audio-native dimensions separately from the transcript-based evaluation.

**Quarter 2 targets:**

8. Deploy deduplication logic.
9. Fix interruption state manager (no repeating after user questions).
10. Build transcript sync pipeline.
11. Begin first pre-registered A/B experiment: Does fixing pronunciation accuracy improve listen-through % after day 15 of a 21-day cohort?

### What Would Change This Decision

| Trigger | Decision Change |
|---|---|
| PII hard guardrail passes 10/10 sensitivity test + contextual privacy evaluator deployed in monitoring mode + email faithfulness reaches ~85% | Move to internal dogfood at < 1% |
| Any zero-tolerance breach (PII in production) | Immediate rollback; halt email ingestion |
| Listen-through drops below 50% for 3 consecutive days | Hold experiment; investigate delivery infrastructure |
| Email faithfulness reaches ~93% | Begin closed beta at 1–5% |

---

## Section 13: Maturity Assessment

| Level | Name | Huxe Status |
|---|---|---|
| Level 1 — Ad Hoc | ❌ | Product has shipped without documented evaluation thresholds |
| Level 2 — Instrumented | 🟡 Partial | App Store reviews provide consumption signals [REV]; internal logging status unknown [SIM] |
| Level 3 — Systematic | ❌ | No taxonomy, regression suite, or CI gate in place at time of this evaluation |
| Level 4 — Closed Loop | ❌ | |
| Level 5 — Self-Improving | ❌ | |

**Current maturity: Between Level 1 and Level 2.**

**Recommended 12-week target: Reach Level 3** — meaning every deployment has regression protection, every user-facing failure routes through a documented fix surface, and Ship/Hold decisions are evidence-backed.

---

## Section 14: Key Takeaways

**1. The user trust contract is the product.**
Huxe's value proposition is "hand me your inbox and I'll make sense of it." That is an extraordinarily high-trust interaction. The PII leakage and faithfulness failures are not peripheral bugs — they are direct strikes against the core premise. Fix these, and Huxe's strong engagement metrics will compound. Leave them unaddressed, and the novelty effect exhausts itself before the product earns long-term retention.

**2. Email is a harder modality than it looks.**
It is semi-structured, thread-based, highly variable in format, deeply personal, and often contextually sensitive in ways that no regex pattern can detect. Treating email ingestion like document parsing is the root cause of most failures found in this evaluation.

**3. Audio-native evaluation is non-negotiable for an audio-first product.**
Transcript review catches what was said. It does not catch how it sounded, whether the interruption recovery felt natural, whether the hosts maintained conversational energy, or whether a 12-minute session felt engaging at the 10-minute mark. For a product that lives or dies on the listening experience, these are not secondary concerns.

**4. Privacy is a two-layer problem.**
Hard-pattern PII (account numbers, passwords) is catchable with regex. Contextual sensitivity (medical appointments, relationship tensions, legal matters) requires a separate LLM-based scorer with a nuanced rubric. Both layers need to pass before email ingestion can be trusted.

**5. The framework holds even when the numbers are estimated.**
The most valuable output of this evaluation is not the specific percentages — it is the taxonomy, the causal chains, the evaluator designs, and the prioritized backlog. These are architecturally grounded and will remain useful when the real pilot replaces simulation-derived estimates with measured data.

---

## Appendix: Evidence Provenance Index

| Section | Key Claims | Evidence Label |
|---|---|---|
| Section 1 (Product Understanding) | Feature descriptions, pipeline stages | [REV] — TechCrunch, App Store |
| Section 4 (Surface Map) | Failure descriptions | [SIM] + [REV] as marked |
| Section 5 (Taxonomy) | Tag names, causal chains | [SIM] architecture reasoning |
| Section 5 (Counts) | 30-trace counts, percentages | [SIM] — not audited metrics |
| Section 6 (Evaluators) | Kappa values | [SIM-EST] — calibrated estimates |
| Section 7 (Audio-Native) | Dimension definitions | [INF] — audio evaluation best practice |
| Section 8 (Contract Scores) | All percentage scores | [SIM-EST] — hypotheses for pilot |
| Section 9 (Drifts) | Risk assessments | [INF] + [REV] as marked |
| Section 10 (Backlog) | Formula scores | [SIM-EST] |
| Section 11 (Driver Analysis) | Hypothesis test results | [SIM-EST] |
| Section 13 (Maturity) | Level assessments | [REV] + [SIM] |

---

*Evaluation conducted using: Multimodal AI Product Evaluation Field Manual (Final Edition, April 2026) · Braintrust (no-code evaluation platform) · Product intelligence from TechCrunch, App Store, Google Play, and published user reviews*

*This is a pilot evaluation protocol, not a production audit. All scores are simulation-derived estimates calibrated against public evidence. A real pilot against live Huxe traces is the recommended next step.*

*Next evaluation cycle: After PII guardrail, contextual privacy evaluator, and thread-fix sprints are deployed.*

