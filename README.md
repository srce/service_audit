# Software Project Maturity Assessment

**Spec version: 0.1.1**

A structured framework for auditing the maturity of a software project. The team first sets its own bar — how important each engineering practice is for this project — then measures where it currently stands against that bar. The gap between the two becomes a scored, prioritized improvement roadmap. The audit can be conducted manually by an assessor, or an LLM agent can take the assessor's role: it interviews the team and produces the report.

## Quick start

**With a coding agent (Claude Code, Cursor, etc.):**

```bash
git clone https://github.com/srce/service_audit.git
cd your-project
claude "Read ../service_audit/AGENT.md and run the assessment interview with me"
```

**With a web chat (claude.ai, ChatGPT, etc.):** attach [service-audit-full.md](service-audit-full.md) — the whole assessment in one file — to a conversation and say "Run this assessment with me." To download it directly:

```bash
curl -O https://raw.githubusercontent.com/srce/service_audit/main/service-audit-full.md
```

The agent interviews your team one question at a time and produces a report you can keep next to your repo and compare against future runs.

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

After changing any assessment content, regenerate the single-file bundle with `./scripts/build-bundle.sh`.

## Related frameworks

How this assessment covers each framework is documented point-by-point in [coverage/](coverage/).

- [The Joel Test: 12 Steps to Better Code](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/) — [coverage](coverage/joel-test.md)
- [The Twelve-Factor Methodology](https://www.12factor.net/) — [coverage](coverage/twelve-factor.md)
- [Open Software Assurance Maturity Model (OpenSAMM)](https://owaspsamm.org/) — [coverage](coverage/opensamm.md)
- [ISO 25010 Software Quality Model](https://iso25000.com/en/iso-25000-standards/iso-25010)

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/legalcode) — see [LICENSE](LICENSE).
