# 4. Code & Quality

Part of the [Software Project Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.1.

### 4.1 Relevance of Codebase

**Why it matters:** Code that no longer reflects current requirements or domain understanding forces every change to fight the existing structure instead of building on it.

**What good looks like:** The codebase's structure and domain models track the business as it exists today, and stale code or abandoned approaches are removed rather than left to confuse the next reader.

**Questions to ask:**
- Does the code's structure still match how the team talks about the domain, or has the business moved on without it?
- What's the last feature that was hard to build because the existing code assumed an old version of the business?
- How much of the codebase is dead or vestigial, and does anyone know which parts?
- When requirements change significantly, does the code get restructured or does a new layer get bolted on top?

**Red flags:** entire modules nobody can explain the purpose of; "legacy" code that's actually still load-bearing but treated as untouchable; the domain model in code contradicts how the business actually operates now.

### 4.2 Patterns

**Why it matters:** Consistent use of architectural and design patterns lets engineers transfer intuition from one part of the codebase to another; inconsistency means every module has to be learned from scratch.

**What good looks like:** A small set of patterns is used deliberately and consistently for recurring problems, the team can name them, and deviations are exceptions with a reason rather than the norm.

**Questions to ask:**
- What patterns does the team say it uses, and does a walk through a few modules confirm it?
- When a new problem looks like one already solved elsewhere in the codebase, does it get solved the same way?
- How many different ways does the codebase solve the same kind of problem — e.g., data fetching, validation, error propagation?
- Who decides when a new pattern is warranted versus reusing an existing one?

**Red flags:** the same problem is solved a different way in every module; patterns were copied from a tutorial without adaptation to this codebase; no one can name the patterns in use without looking them up.

### 4.3 Code Style

**Why it matters:** Inconsistent formatting and style turn every code review into a debate about tabs and semicolons instead of substance, and make diffs noisier than the actual change.

**What good looks like:** A style guide exists, is enforced automatically by tooling rather than by reviewer memory, and the whole codebase reads as if one disciplined person wrote it.

**Questions to ask:**
- Is formatting enforced by a tool, or does it depend on the reviewer catching it?
- Can you point to the style guide, and does the codebase actually match it?
- How much review time gets spent on style comments instead of logic or design?
- What happens when a new contributor's editor uses different defaults — does CI catch it or does it slip through?

**Red flags:** style arguments recur in every PR; formatting is "whatever your editor does"; different files clearly reflect different eras or authors with no unifying convention.

### 4.4 Engineering Principles

**Why it matters:** Principles like SOLID, KISS, and DRY exist to keep change cheap; applied as slogans without judgment they produce as much harm as ignoring them — over-abstraction is as costly as duplication.

**What good looks like:** The team applies these principles with judgment, can explain a specific tradeoff they made, and neither duplicates logic carelessly nor abstracts prematurely to satisfy a rule.

**Questions to ask:**
- Can you point to a place where the team deliberately chose duplication over a premature abstraction, or vice versa?
- What's the most over-engineered part of the codebase, and how did it get that way?
- How is adherence to these principles discussed in code review — as a checklist or as a judgment call?
- What's a rule the team used to follow rigidly that they've since relaxed, and why?

**Red flags:** abstractions with a single implementation "in case we need it later"; the same business rule duplicated in five places with no plan to unify it; principles cited as absolute rules rather than tradeoffs.

### 4.5 Error Handling

**Why it matters:** How a system handles the unexpected — a failed call, a bad input, a timeout — determines whether a small problem stays small or cascades into an incident nobody can diagnose.

**What good looks like:** Errors are handled deliberately at the right layer, logged with enough context to diagnose without reproducing, and surfaced to the right audience — user, operator, or nobody — rather than swallowed or dumped as a stack trace.

**Questions to ask:**
- When something fails, is that visible anywhere, or does it just disappear silently?
- Can you find an example of an error caught and logged with enough context to actually debug it later?
- What's the team's convention for when to retry, fail fast, or degrade gracefully?
- What's the last incident that was hard to diagnose because the error handling didn't capture what actually happened?

**Red flags:** empty catch blocks; errors logged with no context beyond "something went wrong"; the same failure produces a different, inconsistent response depending on which code path hit it.

### 4.6 Technical Debt

**Why it matters:** Debt taken on knowingly to move fast is a legitimate tradeoff; debt that's invisible or unmanaged compounds until it silently caps how fast the team can ship.

**What good looks like:** Debt is tracked somewhere visible, prioritized against feature work with real tradeoffs made explicit, and paid down deliberately rather than only when it causes an outage.

**Questions to ask:**
- Where is technical debt tracked, and when was it last reviewed as a group?
- Can you name the three biggest pieces of debt right now and what each is costing the team?
- Has debt ever been prioritized over a feature, or does feature work always win by default?
- What's the last piece of debt that caused an incident before anyone acted on it?

**Red flags:** debt lives only in tribal memory or scattered TODO comments; debt is never paid down until it causes a production incident; every retro mentions the same unaddressed debt as last time.

### 4.7 Package Management

**Why it matters:** Dependencies are code the team didn't write but is still responsible for; unmanaged versions, unpinned ranges, and unclear ownership of what's installed create both stability and security exposure.

**What good looks like:** Dependency versions are pinned or deliberately ranged, lockfiles are committed and respected, and someone can explain why each major dependency is there and what would happen if it went unmaintained.

**Questions to ask:**
- Are dependency versions pinned, and is the lockfile actually checked into version control and honored?
- Who decides when to add a new dependency, and what's the bar for adding one versus writing it in-house?
- Can you name a dependency that's now unmaintained or deprecated, and is there a plan for it?
- What happened the last time a dependency upgrade broke something — was it caught before or after release?

**Red flags:** no lockfile, or a lockfile that's routinely out of sync with what's actually installed; dependencies added on a whim with no review; a dependency the team knows is abandoned but has no plan to replace.

### 4.8 Unit Tests

**Why it matters:** Tests are the only scalable defense against regressions; without them every change carries hidden risk and refactoring stalls.

**What good looks like:** Tests run on every commit, fail the build, finish in minutes, and the team trusts them. Coverage is tracked but not worshipped.

**Questions to ask:**
- Can you run all tests locally with one command? How long does it take?
- When a test fails, do people fix it or re-run it? How are flaky tests handled?
- Can someone merge with failing tests — is it technically possible?
- What was the last bug that tests *should* have caught but didn't?

**Red flags:** tests skipped in CI; coverage targets without enforcement; "we test manually before release"; flaky tests tolerated for months.

### 4.9 Integration & E2E Testing

**Why it matters:** Unit tests verify pieces in isolation, but most real failures happen at the seams — between services, with the database, through the UI — where only integration and end-to-end tests can catch them.

**What good looks like:** Key user journeys and cross-service interactions are covered by tests that run against realistic environments, run often enough to catch regressions quickly, and are stable enough that failures are trusted signal.

**Questions to ask:**
- What critical user journeys are actually covered by integration or E2E tests, and what's still untested?
- How close to production do these tests' environment and data look?
- How long do these tests take to run, and does that delay affect whether people run them?
- What's the last production bug that only an integration or E2E test could have caught?

**Red flags:** integration tests run against mocks so thoroughly they no longer test integration; E2E suite is so slow or flaky it's routinely skipped; critical user journeys have no test coverage at all.

### 4.10 Scaffolding / Project Layout

**Why it matters:** A confusing or inconsistent repository structure slows down every new contributor and every routine task, long after the people who set it up have moved on.

**What good looks like:** The project layout is predictable, documented, and supported by scripts that make common tasks — setup, running locally, adding a new module — a single command rather than tribal knowledge.

**Questions to ask:**
- Could a new engineer find where a given piece of functionality lives without asking someone?
- Is there a documented convention for where new code should go, and is it actually followed?
- How much tribal knowledge is required to set up a local dev environment from scratch?
- What's the last time someone put code in the "wrong" place because the right place wasn't obvious?

**Red flags:** project structure contradicts its own documentation; setup requires a person to walk you through undocumented steps; similar functionality is scattered across the repo with no consistent home.

### 4.11 Documentation & Domain Language

**Why it matters:** Code that uses the same words the business uses is self-documenting; a mismatch between code vocabulary and domain vocabulary means every conversation requires mental translation and invites misunderstanding.

**What good looks like:** Class, function, and variable names mirror the language the business actually uses, key concepts are documented where the code lives, and a domain expert reading the code (or its docs) would recognize the concepts.

**Questions to ask:**
- Do the names in the code match the words used in planning meetings and by the business, or is there a translation layer in everyone's head?
- Where does domain knowledge live — in the code and its docs, or only in a few people's heads?
- Can you find an example of a term that means one thing to the business and another thing in the code?
- When domain understanding changes, does the code's vocabulary get updated, or does it drift further from reality?

**Red flags:** engineers and product routinely have to "translate" between what they call something and what the code calls it; core domain concepts have no documentation anywhere; the same concept has several different names across the codebase.

### 4.12 Static Analysis / Linting

**Why it matters:** Static analysis catches whole classes of bugs and inconsistencies before a human ever has to look at the code, freeing review time for things a machine can't judge.

**What good looks like:** Linting and static analysis run automatically on every change, block merges on real violations, and the ruleset is tuned deliberately rather than left at defaults or silenced wholesale.

**Questions to ask:**
- What static analysis or linting runs today, and is it enforced in CI or only advisory?
- How many warnings or violations are currently suppressed, and does anyone know why?
- Has static analysis ever caught a bug before it reached production — can you name one?
- Who owns the linting configuration, and when was it last reviewed?

**Red flags:** linter warnings routinely ignored or suppressed with blanket disables; static analysis exists but isn't wired into CI; the ruleset hasn't been touched since the project started and no longer fits how the team writes code.

### 4.13 Code Ownership & Review Process Quality

**Why it matters:** Clear ownership means someone is accountable for a piece of code's health; meaningful review is the primary mechanism for catching problems and spreading knowledge before code ships.

**What good looks like:** Every part of the codebase has a clear owner or owning team, reviews are substantive rather than rubber-stamped, and review feedback covers correctness and design, not just style.

**Questions to ask:**
- For any given file, could you name who owns it or who to ask about it?
- How long does a typical review take, and what kind of feedback does it actually contain?
- Is there a part of the codebase nobody wants to own or touch?
- What's the last bug that review should have caught but didn't, and why did it slip through?

**Red flags:** reviews routinely approved within minutes with no comments; large areas of the codebase have no clear owner; review feedback is almost entirely style nitpicks rather than logic or design concerns.

### 4.14 Dependency Security & Updates

**Why it matters:** Vulnerable or outdated dependencies are one of the most common ways systems get compromised, and the risk is invisible until it's exploited or flagged.

**What good looks like:** Dependencies are scanned for known vulnerabilities on a regular cadence, updates — especially security patches — are applied promptly, and there's a clear process for what happens when a critical vulnerability is found.

**Questions to ask:**
- Is there automated scanning for vulnerable dependencies, and who actually looks at the results?
- What's the typical time between a critical vulnerability being disclosed and it being patched here?
- How far behind are the major dependencies from their latest stable versions, and is that a deliberate choice?
- What's the last security patch that was delayed, and what caused the delay?

**Red flags:** vulnerability scan results exist but nobody acts on them; dependencies are years behind current versions with no plan to catch up; a known critical vulnerability has sat unpatched for months.

### 4.15 Copyright & Licenses

**Why it matters:** Every dependency and piece of borrowed code carries a license with real legal obligations; getting this wrong can create liability that surfaces only during an acquisition, audit, or lawsuit.

**What good looks like:** Dependency licenses are tracked and checked automatically, incompatible or high-risk licenses are flagged before they're merged in, and the project's own licensing is clear and intentional.

**Questions to ask:**
- Is there an automated check for dependency license compatibility, or does it rely on someone noticing?
- Can anyone explain what license the project itself is under and why that was chosen?
- Has a dependency with a restrictive or incompatible license ever made it into the codebase?
- Who would know what to do if legal asked for a full accounting of third-party licenses in use?

**Red flags:** no one has ever checked dependency licenses; copy-pasted code of unknown origin exists in the codebase; the project's own license file is missing, wrong, or was never deliberately chosen.

### 4.16 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
