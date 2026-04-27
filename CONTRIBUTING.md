# Contributing to the Multimodal AI Evaluation Template Library

Thank you for taking the time to contribute. This library exists because evaluation discipline is a shared problem — no single team has solved it alone, and every practitioner who has shipped a multimodal AI product has learned something the templates don't yet capture. Your contributions make the library more honest, more complete, and more useful to teams building in the real world.

---

## What This Library Is

This repository contains 18 production-ready templates (T-01 through T-18) that cover the full lifecycle of multimodal AI evaluation — from pre-launch alignment and architecture trade-offs through to quarterly governance audits. The templates are designed to be filled in, not admired. They are opinionated by design: the opinions come from failure patterns observed across real products, not from theory.

---

## What We Welcome

### High-Value Contributions

- **Real failure patterns not yet in the taxonomy** — If you encountered a failure mode in production that doesn't map cleanly to the 23 standard tags in T-11/T-16/T-18, open an issue with a description and proposed tag name. Taxonomy gaps are blind spots for everyone using the suite.
- **Threshold calibration data** — The reference quality bars in T-02 are starting points. If you have validated bars from a production deployment (domain, source type, and bar), share them. Annotate with context — a bar that works for clean enterprise PDFs does not work for noisy field audio.
- **Domain-specific zero-tolerance events** — The templates name generic examples. Medical, legal, financial, compliance, and other high-stakes domains each have failure types that belong in the zero-tolerance section. Additions here protect users across the community.
- **Evaluator calibration examples** — T-05 through T-09 each require 3–5 calibration examples before deployment. Anonymised, domain-agnostic examples that demonstrate pass/fail distinctions clearly are directly usable by other teams.
- **Architecture patterns and cost data** — The cost reference table in T-03 goes stale quickly. Corrections and additions with verified pricing and source date are welcome.
- **Corrections to any factual claim** — If a threshold, formula, or process description is wrong, say so. Open an issue with the specific claim, why it is wrong, and what the correct version is.

### Contributions We Do Not Accept

- Threshold suggestions not grounded in production experience or cited research
- Changes that soften zero-tolerance language — zero-tolerance means exactly that
- Additions that make templates longer without making them more actionable
- Generic "best practices" content that duplicates what is already here
- Promotional content for specific vendors or products

---

## How to Contribute

### Reporting an Issue

Open a GitHub Issue and use one of the following labels:

| Label | Use For |
|---|---|
| `taxonomy-gap` | A failure mode not covered by the 23 standard tags |
| `threshold-correction` | A reference bar that is wrong or outdated |
| `template-bug` | A field, formula, or instruction that is incorrect |
| `template-enhancement` | A structural addition that improves usability |
| `cost-data-update` | Pricing corrections for the T-03 reference table |
| `domain-addition` | Domain-specific zero-tolerance events or calibration examples |
| `question` | A usage question that might indicate a documentation gap |

For every issue, include:
1. Which template(s) are affected (e.g., T-02, T-11)
2. The specific section or field
3. What is currently there
4. What you believe it should say, and why

### Submitting a Pull Request

1. **Fork the repository** and create a branch named `template/T-XX-description` or `taxonomy/tag-name-description`
2. **Make the smallest change that addresses the issue** — do not bundle unrelated edits
3. **Update the version field** in the affected template's Document Header (increment the minor version, e.g. v1.0 → v1.1)
4. **Add an entry to the template's version history table** describing what changed and why
5. **Open the PR against `main`** with the issue number in the description
6. **Do not edit threshold values retroactively** — if a threshold changes, the change applies from the PR merge date forward; prior evaluation runs referenced the old threshold

### PR Description Template

```
## Summary
[One paragraph: what changed and why]

## Template(s) Affected
- T-XX — [Template Name]

## Type of Change
☐ Taxonomy addition
☐ Threshold correction
☐ Template bug fix
☐ Structural enhancement
☐ Cost data update
☐ Domain-specific addition

## Grounding
[What production experience, cited source, or validated data supports this change?]

## Backward Compatibility
☐ This change does not affect teams currently using the existing template
☐ This change requires teams to update existing fills — describe impact below:

## Checklist
☐ Version field updated in affected template(s)
☐ Version history table updated
☐ No unrelated changes included
☐ Zero-tolerance language preserved or strengthened (not softened)
```

---

## Template Versioning Rules

These rules mirror the versioning rules stated in the templates themselves. Contributors must follow them.

- Increment the **minor version** (v1.0 → v1.1) for any field addition, instruction clarification, or non-breaking structural change
- Increment the **major version** (v1.x → v2.0) for changes to the formula, contract structure, or any change that requires teams to re-run evaluations against the new version
- **Never edit a threshold retroactively** after evaluation runs have referenced it
- **Tag each version** in the PR with the template name and change summary
- The `CHANGELOG.md` in this repository is the authoritative record of all version changes across all templates

---

## Taxonomy Contribution Guidelines

The failure taxonomy (used in T-11, T-16, T-17, and T-18) is the backbone of the evaluation program. New tags require more justification than other contributions because every tag added becomes a minimum-5-case requirement in the regression suite for every team using the library.

To propose a new taxonomy tag, open an issue with:

1. **Proposed tag name** — follow the `layer.subtype.failure_mode` naming convention (e.g., `ingestion.pdf.table_merge`, `output.visual.legend_mismatch`)
2. **Definition** — one sentence describing the failure precisely enough that two engineers independently labelling examples would agree ≥ 80% of the time
3. **Production evidence** — describe a real failure instance (anonymised) that this tag would have captured
4. **Causal chain** — what upstream failures cause this, and what downstream failures it causes
5. **Why existing tags don't cover it** — map it against the 23 standard tags and explain the gap

Tags will not be added if they are redundant with existing tags, too vague to label consistently, or not grounded in an observed failure pattern.

---

## Style Guide

All templates are written in GitHub-flavoured Markdown. When editing:

- Use `##` for top-level sections and `###` for subsections — do not add heading levels beyond `###`
- Use pipe tables for all structured data — do not use HTML tables
- Use `☐` for unchecked checkboxes and `☑` for always-active items (copy from existing templates)
- Use `≥`, `≤`, `→` rather than `>=`, `<=`, `->`
- Use `_____` (five underscores) as the standard fill-in placeholder
- Keep instructional callouts in blockquotes (`>`) with a `⚠️` prefix for warnings
- Keep code blocks (YAML schema, judge prompts) in fenced code blocks with the appropriate language tag
- Do not add emojis outside of the `⚠️` warning convention already established in the templates

---

## Code of Conduct

This is a practitioner library. Contributions are evaluated on whether they make teams more effective at catching failures before users do — not on seniority, affiliation, or how confidently a claim is stated. Be specific, be grounded, and be willing to be wrong. That is what the templates ask of the teams that use them, and it is what we ask of contributors.

Disrespectful behaviour, promotional contributions, and bad-faith edits will result in removal from the contributor list without discussion.

---

## Questions

If you are unsure whether a contribution fits, open an issue with the `question` label before writing any code or prose. A short conversation upfront saves everyone time.

---

## Acknowledgements

Every production failure that informed these templates was caught — or missed — by a real team. Contributors who share what they learned from real deployments are the reason this library improves. Your name will appear in the `CHANGELOG.md` entry for every template version your contribution touches.
