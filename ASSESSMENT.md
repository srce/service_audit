# Software Project Maturity Assessment

**Spec version: 0.1.1** — see [CHANGELOG.md](CHANGELOG.md) for the versioning policy.

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
