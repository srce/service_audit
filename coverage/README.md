# Framework coverage

This directory documents how the Software Project Maturity Assessment covers
well-known external frameworks and checklists. Each file maps one framework's
points to our item IDs, states a coverage verdict per point, and is honest
about gaps.

| Framework | Coverage |
|---|---|
| [The Joel Test: 12 Steps to Better Code](joel-test.md) | 9/12 full, 3/12 partial |
| [The Twelve-Factor Methodology](twelve-factor.md) | 5/12 full, 6/12 partial, 1/12 not covered (deliberate) |
| [OWASP SAMM (OpenSAMM)](opensamm.md) | 6/15 full, 9/15 partial |

## Template for new mappings

Each mapping file follows this structure:

```markdown
# Coverage: <Framework Name>

**Source:** <URL>
**Mapped against spec version:** <X.Y.Z>
**Last reviewed:** <YYYY-MM-DD>

<One-paragraph summary: overall coverage and the framework's angle vs ours.>

| # | Framework point | Our item(s) | Coverage |
|---|---|---|---|
| 1 | ... | 4.8 Unit Tests | ✅ Full / ✅ Full (modernized) / ⚠️ Partial / ❌ Not covered |

## Notes on partial and missing coverage

<For each ⚠️/❌: what exactly is not asked, whether the gap is deliberate
(modern practice superseded the point) or a real candidate for a future
MINOR release.>
```

Coverage verdicts: **Full** — an item's questions probe the same ground;
**Full (modernized)** — covered by the practice that superseded the original
point; **Partial** — the theme is assessed but the framework's specific
question is not asked; **Not covered** — no equivalent anywhere in the items.

When assessment items change in a MINOR or MAJOR release, re-review the
mappings and update "Mapped against spec version".
