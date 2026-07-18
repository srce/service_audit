# Improvement backlog

Planned improvements, roughly ordered by value within each section. Items that
add or change assessment questions ship as a MINOR release per the
[versioning policy](CHANGELOG.md).

## Adoption & interview experience

First-time users and full runs are the biggest friction points today: the
framework is complete, but there is no worked example and a full interview
covers ~80 items.

- [ ] **Sample filled report** — one anonymized end-to-end report next to
  `templates/report.md` (or under `examples/`) so teams can calibrate
  importance/state ratings and see gap priority, category scores, and
  recommendations in context.
- [ ] **Lite / abbreviated profile** — a documented subset of items (or
  category-skip guidance) for a 30–60 minute first pass. Full assessment
  remains the default; lite is for discovery or re-checks between major runs.
- [ ] **Scoring spreadsheet** (or simple calculator) — same item IDs as the
  report template; auto-computes gap priority and category % so manual runs
  do not require hand math.
- [ ] **Web form / product shell** (later) — optional UI on top of the same
  item IDs for guided interviews and exportable Markdown reports. Not a
  substitute for the agent path; an alternative entry point.

## Content quality

The item set is coherent at v0.1.x; a pass for consistency will make agent
interviews shorter and ratings more stable across assessors.

- [ ] **Wording consistency pass** — align tone, tense, and terminology across
  all seven category files (e.g. "Feedbacks", historical numbering fixes were
  one-offs; scan for remaining awkward titles and uneven "What good looks
  like" depth).
- [ ] **Overlap / boundary review** — where adjacent items share ground
  (e.g. 4.14 vs 6.7 dependency security, 1.8 vs 6.10 compliance, 4.13 vs 2.8
  reviews), tighten scopes and cross-references so the same practice is not
  scored twice without intent.
- [ ] **Interview length audit** — count questions per item; flag items with
  more than ~4 questions for trim or "ask only if importance ≥ 2" notes in
  AGENT.md guidance.

## Coverage mappings to add (`coverage/`)

When a mapping ships, list it in the [coverage index](coverage/README.md)
table and in README's [Related frameworks](README.md#related-frameworks)
section, and remove it here.

- [ ] **DORA metrics / Accelerate** — the four key delivery metrics
  (deployment frequency, lead time, change failure rate, time to restore).
  Maps onto 5.9, 5.10, 5.12, 5.13. The most influential modern framework we
  don't yet cover; also note how DORA numbers can be recorded as evidence in
  item notes. Fold Google SRE practices (SLOs, error budgets, toil) into
  this mapping — they overlap heavily.
- [ ] **AWS Well-Architected Framework** (+ Azure/GCP equivalents) — six
  pillars mapping onto categories 3, 5, 6, including FinOps (5.15).
- [ ] **CMMI** — short lineage note: our 0–4 Absent→Optimizing scale is the
  CMMI-style maturity ladder without the process bureaucracy.
- [ ] **SPACE framework** (second tier) — developer-productivity research;
  complements categories 2 and 7.

## Candidate items and questions for v0.2.0 (from the coverage series)

- [ ] **New item: UX & Accessibility** (category 1) — the largest genuine
  gap found; usability practice is currently unassessed
  (see [coverage/iso-25010.md](coverage/iso-25010.md)).
- [ ] 5.8: question on how non-secret configuration is managed and injected
  per environment (see [coverage/twelve-factor.md](coverage/twelve-factor.md)).
- [ ] 4.6: question "does new feature work start while known bugs sit
  unfixed?" (see [coverage/joel-test.md](coverage/joel-test.md)).
- [ ] 3.6: question on startup/shutdown discipline — clean drain on deploy
  (see [coverage/twelve-factor.md](coverage/twelve-factor.md)).
- [ ] 7.3: question on interview practices — do candidates demonstrate real
  work (see [coverage/joel-test.md](coverage/joel-test.md)).
- [ ] 6.1: questions on security strategy & metrics and secure-coding
  training (see [coverage/opensamm.md](coverage/opensamm.md)).
- [ ] Secure Build: question on supply-chain integrity — artifact signing,
  provenance (see [coverage/opensamm.md](coverage/opensamm.md)).
- [ ] 7.4: question on coaching/mentoring relationships (seed mentions
  coaching; currently unasked).

## Tooling & release hygiene

- [ ] `scripts/bump-version.sh` — rewrite all version stamps in one go
  (currently ~12 manual locations; only the bundle picks the version up
  automatically).
- [ ] **CI version / bundle check** — on PR: run `scripts/build-bundle.sh`
  (or a dry-run check) so version stamps stay aligned and
  `service-audit-full.md` is never committed stale.
- [ ] **Cut a release for existing coverage maps** — Joel Test, Twelve-Factor,
  OpenSAMM, and ISO 25010 mappings are in-tree under CHANGELOG `[Unreleased]`;
  ship a PATCH (or MINOR if preferred) so consumers have a tagged baseline.
- [ ] Rename the repository (title is already "Software Project Maturity
  Assessment"; repo slug still `service_audit`) and update the two hardcoded
  URLs in README's Quick start.
- [ ] GitHub Release for tagged versions (`gh release create` with the
  CHANGELOG section as notes).
