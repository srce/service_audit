# Assessment v0.1.0 Rework Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Turn the two-file question list into a versioned assessment framework with structured items, importance/state scoring, and an LLM interview prompt that produces a standard report.

**Architecture:** Pure-Markdown documentation project. `assessment/` holds 7 category files (the content), `ASSESSMENT.md` is the index with scoring scales, `AGENT.md` is a self-contained LLM prompt, `templates/report.md` is the report skeleton. No code, no build step; verification is structural (grep counts, link checks).

**Tech Stack:** Markdown, git, `curl` (LICENSE download only).

**Spec:** `docs/superpowers/specs/2026-07-17-assessment-rework-design.md`

## Global Constraints

- Spec version being produced: **0.1.0**. It appears verbatim in README.md, ASSESSMENT.md, AGENT.md, templates/report.md, CHANGELOG.md, and the final git tag `v0.1.0`.
- Every scored item uses stable ID `<category>.<number>` (e.g. `4.8`) as a `###` heading: `### 4.8 Unit Tests`.
- **Item block format** (canonical example — every item in every category file follows exactly this shape):

  ```markdown
  ### 4.8 Unit Tests

  **Why it matters:** Tests are the only scalable defense against regressions; without them every change carries hidden risk and refactoring stalls.

  **What good looks like:** Tests run on every commit, fail the build, finish in minutes, and the team trusts them. Coverage is tracked but not worshipped.

  **Questions to ask:**
  - Can you run all tests locally with one command? How long does it take?
  - When a test fails, do people fix it or re-run it? How are flaky tests handled?
  - Can someone merge with failing tests — is it technically possible?
  - What was the last bug that tests *should* have caught but didn't?

  **Red flags:** tests skipped in CI; coverage targets without enforcement; "we test manually before release"; flaky tests tolerated for months.
  ```

- **Authoring rules for blocks:** "Why it matters" and "What good looks like" are 1–2 sentences each. 3–5 questions per item; prefer reality-revealing questions ("what was the last time X failed?") over yes/no compliance questions. "Red flags" is a single semicolon-separated line or up to 4 short bullets. No block may be left as a bare heading.
- The final item of every category file is `### <n>.<last> Other` with only this line under it: `Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.` ("Other" items get no why/what/questions/red-flags block.)
- Scoring scales (used verbatim wherever scales are described): Importance — `1 Low, 2 Medium, 3 Critical, N/A skipped (reason recorded)`. Current state — `0 Absent, 1 Ad-hoc, 2 Defined, 3 Managed, 4 Optimizing`. Gap priority = `importance × (4 − state)`. Category score = `Σ(importance × state) / Σ(importance × 4)` as a percentage; a category where every item is N/A is reported as "not assessed".
- Source material: the one-line descriptions in the current `ASSESSMENT.md` (git HEAD) are the topical seed for each block; expand them, don't contradict them.
- Commit after every task. Commit messages end with `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`.

---

### Task 1: LICENSE and CHANGELOG scaffolding

**Files:**
- Create: `LICENSE`
- Create: `CHANGELOG.md`

**Interfaces:**
- Produces: `CHANGELOG.md` with an `[Unreleased]` section that Task 12 converts to `[0.1.0]`.

- [ ] **Step 1: Download the CC BY 4.0 legal text**

Run: `curl -fsSL https://creativecommons.org/licenses/by/4.0/legalcode.txt -o LICENSE`
Expected: file exists, `head -3 LICENSE` mentions "Creative Commons Attribution 4.0".
Fallback if the URL fails: copy the full legal text from https://creativecommons.org/licenses/by/4.0/legalcode into `LICENSE` manually.

- [ ] **Step 2: Create CHANGELOG.md**

```markdown
# Changelog

All notable changes to this assessment are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/) —
MAJOR = items removed/renumbered/restructured (breaks report comparability),
MINOR = items or questions added, PATCH = wording fixes.

## [Unreleased]

### Added
- Structured item blocks (why it matters, what good looks like, questions to ask, red flags) for all categories.
- Importance/state scoring model with gap priority and category scores.
- `AGENT.md` LLM interview prompt and `templates/report.md` report template.
- LICENSE file (CC BY 4.0), this changelog, versioning policy.

### Changed
- Split `ASSESSMENT.md` into per-category files under `assessment/`; `ASSESSMENT.md` is now the index.
- Moved "Team Health & Culture" from Processes (2.14) to Culture (7.5).
- Scoped 1.8 Compliance & Legal to product obligations; cross-referenced 6.10 for operations.

### Fixed
- Numbering and wording defects ("13" item, "Feedbacks", "Groundrules", "Unit-tests", README link spacing).
```

- [ ] **Step 3: Verify and commit**

Run: `head -3 LICENSE && grep -c "## \[Unreleased\]" CHANGELOG.md`
Expected: CC BY 4.0 header visible; count is `1`.

```bash
git add LICENSE CHANGELOG.md
git commit -m "Add CC BY 4.0 license file and changelog"
```

---

### Task 2: Category file 1 — Product & Vision

**Files:**
- Create: `assessment/01-product-vision.md`

**Interfaces:**
- Produces: item IDs `1.1`–`1.9` referenced by ASSESSMENT.md (Task 10) and reports.

- [ ] **Step 1: Write the file**

File starts with:

```markdown
# 1. Product & Vision

Part of the [Software Engineering Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.0.
```

Then one item block (Global Constraints format) per item:

| ID | Title | Seed (from current ASSESSMENT.md) |
|---|---|---|
| 1.1 | Product Overview | product, core users, problem space |
| 1.2 | Product Vision / Mission | long-term direction and intent |
| 1.3 | Project Goals | short-/mid-term objectives tied to outcomes |
| 1.4 | Functional and Non-Functional Requirements | what it must do and how it must perform |
| 1.5 | Product Roadmap | planned initiatives, dependencies, timing |
| 1.6 | User Research & Feedback Loops | how insights are gathered and acted on |
| 1.7 | Product Metrics & Analytics | signals for success, adoption, quality |
| 1.8 | Compliance & Legal Requirements | which obligations apply (GDPR, accessibility, industry). Block must include the sentence: "How compliance is operated day-to-day is assessed in [6.10](06-security-compliance.md#610-compliance--data-retention-policies)." |
| 1.9 | Other | (Other-line only, per Global Constraints) |

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 1\.' assessment/01-product-vision.md && grep -c '\*\*Why it matters:\*\*' assessment/01-product-vision.md`
Expected: `9` then `8`.

- [ ] **Step 3: Commit**

```bash
git add assessment/01-product-vision.md
git commit -m "Add structured Product & Vision category (1.1-1.9)"
```

---

### Task 3: Category file 2 — Processes & Collaboration

**Files:**
- Create: `assessment/02-processes-collaboration.md`

**Interfaces:**
- Produces: item IDs `2.1`–`2.14`. Note: Team Health & Culture is REMOVED from this category (moves to 7.5, Task 8); "Other" is `2.14`.

- [ ] **Step 1: Write the file**

Same header pattern as Task 2 (`# 2. Processes & Collaboration`, spec-version line). Item blocks:

| ID | Title |
|---|---|
| 2.1 | Onboarding Process |
| 2.2 | Roles and Responsibilities |
| 2.3 | Methodologies and Frameworks |
| 2.4 | Communications |
| 2.5 | Task Management |
| 2.6 | Prioritization and Decision Making |
| 2.7 | Project Estimation |
| 2.8 | Code Reviews |
| 2.9 | Retrospectives and Feedback |
| 2.10 | Ground Rules |
| 2.11 | Decision Records (ADR) |
| 2.12 | Cross-Team Collaboration |
| 2.13 | Stakeholder Management |
| 2.14 | Other |

Seeds are the corresponding one-liners in current `ASSESSMENT.md` §2 (with "Feedbacks"→"Feedback", "Groundrules"→"Ground Rules" fixed).

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 2\.' assessment/02-processes-collaboration.md && grep -c '\*\*Why it matters:\*\*' assessment/02-processes-collaboration.md && grep -ci 'team health' assessment/02-processes-collaboration.md`
Expected: `14`, `13`, `0`.

- [ ] **Step 3: Commit**

```bash
git add assessment/02-processes-collaboration.md
git commit -m "Add structured Processes & Collaboration category (2.1-2.14)"
```

---

### Task 4: Category file 3 — Architecture & Systems Design

**Files:**
- Create: `assessment/03-architecture-design.md`

**Interfaces:**
- Produces: item IDs `3.1`–`3.9`.

- [ ] **Step 1: Write the file**

Header `# 3. Architecture & Systems Design` + spec-version line. Items (seeds from current §3): 3.1 System Documentation, 3.2 Tech Stack, 3.3 Architecture Patterns, 3.4 Loose Coupling / High Cohesion, 3.5 Scalability & Performance, 3.6 Resilience & Fault Tolerance, 3.7 Data Architecture, 3.8 APIs & Integrations, 3.9 Other.

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 3\.' assessment/03-architecture-design.md && grep -c '\*\*Why it matters:\*\*' assessment/03-architecture-design.md`
Expected: `9` then `8`.

- [ ] **Step 3: Commit**

```bash
git add assessment/03-architecture-design.md
git commit -m "Add structured Architecture & Systems Design category (3.1-3.9)"
```

---

### Task 5: Category file 4 — Code & Quality

**Files:**
- Create: `assessment/04-code-quality.md`

**Interfaces:**
- Produces: item IDs `4.1`–`4.16`. `4.8 Unit Tests` must be exactly the canonical block from Global Constraints.

- [ ] **Step 1: Write the file**

Header `# 4. Code & Quality` + spec-version line. Items (seeds from current §4): 4.1 Relevance of Codebase, 4.2 Patterns, 4.3 Code Style, 4.4 Engineering Principles, 4.5 Error Handling, 4.6 Technical Debt, 4.7 Package Management, 4.8 Unit Tests (canonical block verbatim), 4.9 Integration & E2E Testing, 4.10 Scaffolding / Project Layout, 4.11 Documentation & Domain Language, 4.12 Static Analysis / Linting, 4.13 Code Ownership & Review Process Quality, 4.14 Dependency Security & Updates, 4.15 Copyright & Licenses, 4.16 Other.

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 4\.' assessment/04-code-quality.md && grep -c '\*\*Why it matters:\*\*' assessment/04-code-quality.md && grep -c '### 4.8 Unit Tests' assessment/04-code-quality.md`
Expected: `16`, `15`, `1`.

- [ ] **Step 3: Commit**

```bash
git add assessment/04-code-quality.md
git commit -m "Add structured Code & Quality category (4.1-4.16)"
```

---

### Task 6: Category file 5 — Engineering Practices & Delivery

**Files:**
- Create: `assessment/05-practices-delivery.md`

**Interfaces:**
- Produces: item IDs `5.1`–`5.16`.

- [ ] **Step 1: Write the file**

Header `# 5. Engineering Practices & Delivery` + spec-version line. Items (seeds from current §5): 5.1 Version Control System, 5.2 Project Installation, 5.3 Project Launch, 5.4 Project Build, 5.5 Project Testing, 5.6 Automation, 5.7 Optimizations, 5.8 Multiple Environments, 5.9 Release Management Process, 5.10 Recovery Plan, 5.11 Observability, 5.12 Monitoring & Alerting Quality, 5.13 CI/CD, 5.14 Infrastructure as Code (IaC), 5.15 Cost Efficiency / Cloud Optimization (FinOps), 5.16 Other.

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 5\.' assessment/05-practices-delivery.md && grep -c '\*\*Why it matters:\*\*' assessment/05-practices-delivery.md`
Expected: `16` then `15`.

- [ ] **Step 3: Commit**

```bash
git add assessment/05-practices-delivery.md
git commit -m "Add structured Practices & Delivery category (5.1-5.16)"
```

---

### Task 7: Category file 6 — Security & Compliance

**Files:**
- Create: `assessment/06-security-compliance.md`

**Interfaces:**
- Produces: item IDs `6.1`–`6.11`. `6.10` must cross-reference `1.8`.

- [ ] **Step 1: Write the file**

Header `# 6. Security & Compliance` + spec-version line. Items (seeds from current §6): 6.1 Security Requirements, 6.2 Sensitive Data Protection, 6.3 Input Validation, 6.4 Authentication / Authorization, 6.5 Credentials, 6.6 Key Management, 6.7 Vulnerability Management & Dependency Scanning, 6.8 Penetration Testing / Audits, 6.9 Incident Response Process, 6.10 Compliance & Data Retention Policies, 6.11 Other.

The 6.10 block must include the sentence: "Which obligations apply to the product is assessed in [1.8](01-product-vision.md#18-compliance--legal-requirements); this item covers how retention and compliance are operated."

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 6\.' assessment/06-security-compliance.md && grep -c '\*\*Why it matters:\*\*' assessment/06-security-compliance.md && grep -c '01-product-vision.md#18' assessment/06-security-compliance.md`
Expected: `11`, `10`, `1`.

- [ ] **Step 3: Commit**

```bash
git add assessment/06-security-compliance.md
git commit -m "Add structured Security & Compliance category (6.1-6.11)"
```

---

### Task 8: Category file 7 — Culture & External Factors

**Files:**
- Create: `assessment/07-culture.md`

**Interfaces:**
- Produces: item IDs `7.1`–`7.6`, including `7.5 Team Health & Culture` (moved from old 2.14).

- [ ] **Step 1: Write the file**

Header `# 7. Culture & External Factors` + spec-version line. Items: 7.1 Working Conditions, 7.2 Remote Work / Hybrid Efficiency, 7.3 HR & Recruiting Alignment, 7.4 Continuous Learning & Growth, 7.5 Team Health & Culture (seed: old 2.14 — morale, psychological safety, DEI, wellbeing), 7.6 Other.

- [ ] **Step 2: Verify structure**

Run: `grep -c '^### 7\.' assessment/07-culture.md && grep -c '\*\*Why it matters:\*\*' assessment/07-culture.md && grep -c '### 7.5 Team Health & Culture' assessment/07-culture.md`
Expected: `6`, `5`, `1`.

- [ ] **Step 3: Commit**

```bash
git add assessment/07-culture.md
git commit -m "Add structured Culture category (7.1-7.6), absorb Team Health from 2.14"
```

---

### Task 9: Report template

**Files:**
- Create: `templates/report.md`

**Interfaces:**
- Produces: the report structure AGENT.md (Task 11) instructs the LLM to fill. `{{...}}` placeholders are deliberate template slots.

- [ ] **Step 1: Write the template**

```markdown
# Engineering Maturity Assessment Report

| | |
|---|---|
| **Team / Product** | {{TEAM_NAME}} |
| **Date** | {{DATE}} |
| **Spec version** | 0.1.0 |
| **Participants** | {{NAMES_AND_ROLES}} |
| **Categories assessed** | {{LIST_OR_ALL}} |

## Scoring key

Importance: 1 Low, 2 Medium, 3 Critical, N/A skipped (reason recorded).
Current state: 0 Absent, 1 Ad-hoc, 2 Defined, 3 Managed, 4 Optimizing.
Gap priority = importance × (4 − state), max 12. Category score = Σ(importance × state) / Σ(importance × 4), as a percentage. A category where every item is N/A is "not assessed".

## Summary

| Category | Score | Top gap |
|---|---|---|
| 1. Product & Vision | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 2. Processes & Collaboration | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 3. Architecture & Systems Design | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 4. Code & Quality | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 5. Engineering Practices & Delivery | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 6. Security & Compliance | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |
| 7. Culture & External Factors | {{PCT_OR_NOT_ASSESSED}} | {{ITEM}} |

## Top gaps (improvement roadmap)

Up to 10 items, sorted by gap priority descending.

| Rank | Item | Importance | State | Gap priority | Note |
|---|---|---|---|---|---|
| 1 | {{ID_AND_TITLE}} | {{1-3}} | {{0-4}} | {{N}} | {{ONE_LINE}} |

## Recommendations

3–5 short narrative recommendations, each tied to the gaps above: what to do first, why, and what "better" would look like in 3–6 months.

1. {{RECOMMENDATION}}

## Detailed results

One table per assessed category; repeat this structure for each.

### {{N}}. {{CATEGORY_NAME}} — {{PCT_OR_NOT_ASSESSED}}

| Item | Importance | State | Gap | Notes |
|---|---|---|---|---|
| {{ID_AND_TITLE}} | {{1-3_OR_N/A}} | {{0-4_OR_DASH}} | {{N_OR_DASH}} | {{NOTES}} |

## Appendix

- **N/A items and reasons:** {{LIST}}
- **Free-form notes ("Other" items):** {{LIST}}
```

- [ ] **Step 2: Verify and commit**

Run: `grep -c '{{' templates/report.md`
Expected: a number ≥ 15 (placeholders present).

```bash
git add templates/report.md
git commit -m "Add assessment report template"
```

---

### Task 10: ASSESSMENT.md index rewrite

**Files:**
- Modify: `ASSESSMENT.md` (full replacement)

**Interfaces:**
- Consumes: category files from Tasks 2–8 (links must resolve).

- [ ] **Step 1: Replace ASSESSMENT.md content**

```markdown
# Engineering Assessment Guide

**Spec version: 0.1.0** — see [CHANGELOG.md](CHANGELOG.md) for the versioning policy.

This guide evaluates software engineering maturity across seven categories. Each item has a stable ID (e.g. `4.8`), an explanation of why it matters, what good looks like, questions to ask, and red flags. Items live in per-category files:

1. [Product & Vision](assessment/01-product-vision.md)
2. [Processes & Collaboration](assessment/02-processes-collaboration.md)
3. [Architecture & Systems Design](assessment/03-architecture-design.md)
4. [Code & Quality](assessment/04-code-quality.md)
5. [Engineering Practices & Delivery](assessment/05-practices-delivery.md)
6. [Security & Compliance](assessment/06-security-compliance.md)
7. [Culture & External Factors](assessment/07-culture.md)

## How to score

Rate every item twice:

| Rating | Scale |
|---|---|
| **Importance** — how much this matters for *your* team | 1 Low · 2 Medium · 3 Critical · N/A skipped (record the reason) |
| **Current state** — where you are today | 0 Absent · 1 Ad-hoc · 2 Defined · 3 Managed · 4 Optimizing |

Derived values:

- **Gap priority** = importance × (4 − state). Highest first = your improvement roadmap (max 12: critical and absent).
- **Category score** = Σ(importance × state) / Σ(importance × 4), shown as a percentage — how close you are to where *you* said you need to be. A category where every item is N/A is "not assessed", not a number.

Scores exist to show a team its own gap between importance and reality and to track its own progress across assessments. They are not for comparing teams or grading people.

## How to run an assessment

- **Manually:** walk the category files with the team, record ratings and notes in a copy of [templates/report.md](templates/report.md).
- **With an LLM:** give your AI assistant [AGENT.md](AGENT.md) plus the `assessment/` files and let it interview the team and produce the report. See AGENT.md for instructions.

Every report records the spec version it was produced against.
```

- [ ] **Step 2: Verify links resolve**

Run: `for f in assessment/01-product-vision.md assessment/02-processes-collaboration.md assessment/03-architecture-design.md assessment/04-code-quality.md assessment/05-practices-delivery.md assessment/06-security-compliance.md assessment/07-culture.md templates/report.md CHANGELOG.md; do test -f "$f" || echo "MISSING $f"; done`
Expected: no output.

- [ ] **Step 3: Commit**

```bash
git add ASSESSMENT.md
git commit -m "Rewrite ASSESSMENT.md as index with scoring model"
```

---

### Task 11: AGENT.md interview prompt

**Files:**
- Create: `AGENT.md`

**Interfaces:**
- Consumes: category files (Tasks 2–8), `templates/report.md` (Task 9), scales (Global Constraints).

- [ ] **Step 1: Write AGENT.md**

```markdown
# LLM Assessment Agent Instructions

You are an experienced engineering consultant running a Software Engineering Maturity Assessment (spec version 0.1.0). Your job: interview the team, rate each item with them, and produce a report.

**You need these files** (ask for any that are missing): the seven files in `assessment/`, and `templates/report.md`.

## Ground rules

- Ask **one question at a time**. Be conversational, not bureaucratic.
- Never invent answers. If the person doesn't know, record "unknown" in the notes and move on.
- You propose ratings; the human confirms them. Only confirmed ratings go into the report.
- Skip aggressively: low-importance items deserve one question, not five.

## Phase 1 — Setup

Ask, one at a time:
1. Team / product name, and a one-sentence description.
2. Who is answering (names and roles)?
3. Which categories to assess (default: all seven)?
4. Language for the final report (default: the language the person is using)?

## Phase 2 — Interview

For each chosen category, in order, read its file in `assessment/` and go item by item:

1. State the item's title and its one-line "why it matters".
2. Ask for **importance**: 1 Low, 2 Medium, 3 Critical, or N/A (record the reason). If N/A, move to the next item.
3. Interview using the item's "Questions to ask". Skip questions already answered implicitly. For importance 1, ask at most one question.
4. Compare answers against "What good looks like" and "Red flags", then **propose a current-state rating** — 0 Absent, 1 Ad-hoc, 2 Defined, 3 Managed, 4 Optimizing — with a one-sentence rationale. Ask the person to confirm or correct. Record the confirmed value and a one-line note.
5. At the category's "Other" item, ask whether anything important was missed; if yes, record it with its own importance/state ratings.

After each category, give a two-sentence summary of what you heard before moving on.

## Phase 3 — Report

Fill in `templates/report.md` exactly:

- Gap priority per item = importance × (4 − state). Category score = Σ(importance × state) / Σ(importance × 4) as a percentage; all-N/A categories are "not assessed". Compute carefully; show max 10 rows in Top gaps, sorted by gap priority descending, ties broken by importance.
- Write 3–5 recommendations tied to the top gaps: what to do first, why, what "better" looks like in 3–6 months.
- Keep every participant note you recorded in the Detailed results tables.
- Record spec version 0.1.0, the date, and participants in the header.

Deliver the completed report as a single Markdown document.
```

- [ ] **Step 2: Verify and commit**

Run: `grep -c '0.1.0' AGENT.md && grep -c 'Phase' AGENT.md`
Expected: `2` (or more) and ≥ `3`.

```bash
git add AGENT.md
git commit -m "Add LLM interview agent instructions"
```

---

### Task 12: README rewrite, version finalization, tag

**Files:**
- Modify: `README.md` (full replacement)
- Modify: `CHANGELOG.md` (`[Unreleased]` → `[0.1.0]`)

**Interfaces:**
- Consumes: everything above; this task releases v0.1.0.

- [ ] **Step 1: Replace README.md content**

```markdown
# Software Engineering Maturity Assessment

**Spec version: 0.1.0**

A practical framework for assessing the engineering maturity of a software team — by humans, or by an LLM agent interviewing the team.

## Philosophy

Every team is different, so the assessment scores two things: how **important** each practice is for *your* team, and where you **currently stand**. The gap between the two is your improvement roadmap. Scores track a team's own progress over time — they are never for comparing teams or grading people.

## How to use it

1. Read [ASSESSMENT.md](ASSESSMENT.md) — the index, scoring scales, and links to the seven category files in [assessment/](assessment/).
2. Run the assessment:
   - **Manually:** walk the categories with your team and fill in [templates/report.md](templates/report.md).
   - **With an LLM:** give your AI assistant [AGENT.md](AGENT.md) and the `assessment/` files; it interviews the team one question at a time and produces the report.
3. Re-run it periodically (e.g. every 6–12 months) with the same spec version to track progress.

## Versioning

The spec follows [SemVer](https://semver.org/): MAJOR versions change or remove items (reports stop being comparable), MINOR versions add items or questions, PATCH versions fix wording. See [CHANGELOG.md](CHANGELOG.md). Reports record the spec version they were produced with.

## Related frameworks

- [The Joel Test: 12 Steps to Better Code](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/)
- [The Twelve-Factor Methodology](https://www.12factor.net/)
- [Open Software Assurance Maturity Model (OpenSAMM)](https://owaspsamm.org/)
- [ISO 25010 Software Quality Model](https://iso25000.com/en/iso-25000-standards/iso-25010)

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/legalcode) — see [LICENSE](LICENSE).
```

- [ ] **Step 2: Finalize CHANGELOG**

In `CHANGELOG.md`, change the line `## [Unreleased]` to `## [0.1.0] - <today's date in YYYY-MM-DD>`.

- [ ] **Step 3: Full-repo verification**

Run:
```bash
ls assessment/ | wc -l
grep -L '0\.1\.0' README.md ASSESSMENT.md AGENT.md templates/report.md
grep -c '\*\*Why it matters:\*\*' assessment/*.md | awk -F: '{s+=$2} END {print s}'
```
Expected: `7`; no files listed by the grep -L; total why-blocks = `74` (8+13+8+15+15+10+5).

- [ ] **Step 4: Commit and tag**

```bash
git add README.md CHANGELOG.md
git commit -m "Rewrite README for v0.1.0; finalize changelog"
git tag v0.1.0
```
