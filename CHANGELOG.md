# Changelog

All notable changes to this assessment are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/) —
MAJOR = items removed/renumbered/restructured (breaks report comparability),
MINOR = items or questions added, PATCH = wording fixes.

## [0.1.0] - 2026-07-18

### Added
- Structured item blocks (why it matters, what good looks like, questions to ask, red flags) for all categories.
- Importance/state scoring model with gap priority and category scores.
- `AGENT.md` LLM interview prompt and `templates/report.md` report template.
- LICENSE file (CC BY 4.0), this changelog, versioning policy.
- Quick start instructions and single-file bundle `service-audit-full.md` (built by `scripts/build-bundle.sh`) for attaching the whole assessment to a web-based LLM chat.

### Changed
- Split `ASSESSMENT.md` into per-category files under `assessment/`; `ASSESSMENT.md` is now the index.
- Moved "Team Health & Culture" from Processes (2.14) to Culture (7.5).
- Scoped 1.8 Compliance & Legal to product obligations; cross-referenced 6.10 for operations.
- Rescoped 6.7 to the org-wide vulnerability scanning and triage program; day-to-day dependency patching hygiene cross-referenced to 4.14.

### Fixed
- Numbering and wording defects ("13" item, "Feedbacks", "Groundrules", "Unit-tests", README link spacing).
