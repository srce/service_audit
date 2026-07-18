# Improvement backlog

Planned improvements, roughly ordered by value. Items that add or change
assessment questions ship as a MINOR release per the [versioning policy](CHANGELOG.md).

## Coverage mappings to add (`coverage/`)

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

## Tooling

- [ ] `scripts/bump-version.sh` — rewrite all version stamps in one go
  (currently ~12 manual locations; only the bundle picks the version up
  automatically).
- [ ] Rename the repository (title is already "Software Project Maturity
  Assessment"; repo slug still `service_audit`) and update the two hardcoded
  URLs in README's Quick start.
- [ ] GitHub Release for tagged versions (`gh release create` with the
  CHANGELOG section as notes).
