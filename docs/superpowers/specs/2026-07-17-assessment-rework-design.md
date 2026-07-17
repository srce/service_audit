# Design: Software Engineering Maturity Assessment — v0.1.0 Rework

**Date:** 2026-07-17
**Status:** Approved

## Goal

Turn the current two-file question list into a usable, versioned assessment
framework that (a) teaches assessors why each item matters and how to probe it,
(b) produces importance-weighted scores and a gap-based improvement roadmap,
and (c) can be run as an interview by any LLM agent, producing a standard report.

## Repo structure

```
README.md               # positioning, philosophy, how to use, version
CHANGELOG.md            # Keep-a-Changelog format
LICENSE                 # full CC BY 4.0 legal text
ASSESSMENT.md           # index: categories, scoring scales, links to category files
AGENT.md                # self-contained prompt for any LLM to run the assessment
assessment/
  01-product-vision.md
  02-processes-collaboration.md
  03-architecture-design.md
  04-code-quality.md
  05-practices-delivery.md
  06-security-compliance.md
  07-culture.md
templates/
  report.md             # blank assessment report
```

Markdown is the single source of truth; no generated/machine-readable
duplicate. The LLM reads the category files directly.

## Item format

Every assessment item keeps a stable ID (`<category>.<number>`, e.g. `4.8`) so
reports can reference items across versions. Each item is a structured block:

```markdown
### 4.8 Unit Tests

**Why it matters:** 1–2 sentences on the risk/value.

**What good looks like:** 1–2 sentences describing a healthy state.

**Questions to ask:**
- 3–5 diagnostic questions (these double as the LLM interview script).
- Prefer reality-revealing questions ("what was the last bug tests should
  have caught?") over yes/no checklist questions.

**Red flags:** short bullet list of warning signs.
```

Each category file ends with an "Other" item inviting free-form additions
(preserving the current convention).

## Scoring model

Two ratings per item, given by the team being assessed:

| Rating | Scale | Meaning |
|---|---|---|
| Importance | 1–3 or N/A | 1 Low, 2 Medium, 3 Critical for this team; N/A skips the item (reason recorded) |
| Current state | 0–4 | 0 Absent, 1 Ad-hoc, 2 Defined, 3 Managed, 4 Optimizing |

Derived values in the report:

- **Gap priority** per item = `importance × (4 − state)`. Sorted descending,
  this list is the improvement roadmap. Max value 12 (critical + absent).
- **Category score** = `Σ(importance × state) / Σ(importance × 4)` over scored
  items, shown as a percentage: "how close you are to where you said you need
  to be." N/A items are excluded from both sums. A category where every item
  is N/A is reported as "not assessed" rather than a number.

Philosophy (README): scores show a team its own gap between importance and
reality and track its own progress over time. They are never for comparing
teams or grading people. This replaces the current "no scores" statement.

## Content fixes

- Item 2.14 (Team Health & Culture) moves to Section 7, resolving duplication
  and Section 7's thinness.
- Item 1.8 (Compliance & Legal) stays product-focused (which obligations
  exist) and cross-references 6.10 (how compliance/retention is operated).
- Typo fixes: "13" numbering in Section 2, "Feedbacks" → "Feedback",
  "Groundrules" → "Ground Rules", "Unit-tests" → "Unit Tests", README ISO
  link spacing.

## AGENT.md interview flow

Self-contained prompt usable with any LLM that can read the repo files
(pasted or attached). The agent must:

1. **Setup:** ask team/product name, which categories to include, who is
   answering, target report language.
2. **Interview:** category by category, item by item. For each item: ask for
   the importance rating first (or N/A). Only when importance is 1–3, use the
   item's "Questions to ask" to interview — one question at a time,
   conversational, skipping questions already answered implicitly. The agent
   then proposes a state rating with a one-sentence rationale; the engineer
   confirms or corrects it. The confirmed value is recorded.
3. **Report:** fill in `templates/report.md` with: spec version, date,
   participants, per-item table (importance / state / notes), category scores,
   top-10 gap-priority list, and 3–5 narrative recommendations.

## Report template (`templates/report.md`)

Sections: header (team, date, spec version, participants), per-category item
tables, category score summary, top gaps, recommendations, appendix for N/A
reasons and free-form notes.

## Versioning

- SemVer for the spec: **MAJOR** = items removed/renumbered/restructured
  (breaks report comparability), **MINOR** = items or questions added,
  **PATCH** = wording fixes.
- Version stated in README and ASSESSMENT.md; releases tagged in git;
  CHANGELOG.md maintained.
- Every report records the spec version it ran against.
- This rework ships as **v0.1.0**; v1.0.0 when the item set stabilizes.

## Out of scope

- Claude Code skill / slash command packaging (decided: prompt file only).
- Machine-readable YAML/JSON spec.
- Automated repo inspection by the agent (interview-only for now).

## Implementation notes

- ~70 items × structured block is the bulk of the effort (~80%); write
  category by category so each file is reviewable on its own.
- Scaffolding (LICENSE, CHANGELOG, README rewrite, AGENT.md, template,
  ASSESSMENT.md index) is the remaining ~20%.
