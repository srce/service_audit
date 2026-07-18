# 3. Architecture & Systems Design

Part of the [Software Project Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.1.

### 3.1 System Documentation

**Why it matters:** A system that only lives in the heads of its original authors becomes unmaintainable the moment they're unavailable; documentation is what lets someone new reason about the system without archaeology.

**What good looks like:** Architecture diagrams, runbooks, and onboarding docs exist, are findable in one obvious place, and are updated as part of making a change rather than as an afterthought months later.

**Questions to ask:**
- Where's the current architecture diagram, and does it match what's actually deployed?
- When was a system doc last updated alongside a code change, versus discovered stale during an incident?
- Could a new engineer trace how a request flows through the system using only the docs?
- What's the last time outdated documentation sent someone down the wrong path?

**Red flags:** the only diagram is a whiteboard photo from two years ago; docs describe a service that was decommissioned; "just ask So-and-so" is the actual onboarding path for understanding the system.

### 3.2 Tech Stack

**Why it matters:** Every language, framework, and platform choice carries a long-term maintenance and hiring cost; a stack chosen for the wrong reasons — or never revisited — quietly taxes every future change.

**What good looks like:** The team can explain why each major piece of the stack was chosen, those choices are still defensible given current needs, and the stack is small enough that no one is maintaining expertise in five ways of doing the same thing.

**Questions to ask:**
- Why was each major technology in the stack chosen, and by whom?
- Has anything in the stack been added or replaced in the last year, and what drove that?
- Are there multiple tools doing the same job because of historical accident rather than deliberate choice?
- If you were starting today with what you now know, what would you choose differently?

**Red flags:** "it's what the founding engineer knew" as the only rationale still offered; the stack keeps growing but nothing is ever retired; nobody can name a technology that was deliberately rejected and why.

### 3.3 Architecture Patterns

**Why it matters:** The chosen architectural style — monolith, microservices, event-driven, layered — shapes how easily the system can change; a pattern applied inconsistently or adopted by trend rather than fit creates friction everywhere it's violated.

**What good looks like:** The team can name the architectural pattern in use, explain why it fits the problem and team size, and point to the pattern actually being followed in the code rather than just described in a diagram.

**Questions to ask:**
- What architectural pattern does the team say the system follows, and does a walk through the codebase confirm it?
- Why was this pattern chosen over the alternatives at the time?
- Where does the codebase visibly violate the stated pattern, and is that tracked as debt or just accepted?
- Has the pattern been revisited as the system or team has grown?

**Red flags:** the system is called "microservices" but every service shares a database; the pattern was copied from a conference talk without evaluating fit; boundaries exist on a diagram but not in the actual code.

### 3.4 Loose Coupling / High Cohesion

**Why it matters:** Tightly coupled modules turn small changes into system-wide events; when responsibilities are scattered instead of cohesive, understanding or safely changing any one piece requires understanding all of them.

**What good looks like:** Modules have clear, narrow interfaces, a change inside one rarely forces changes in unrelated ones, and each module's responsibility can be described in a single sentence.

**Questions to ask:**
- What's the last change that "should" have touched one module but ended up rippling through several?
- Can you name a module's responsibility in one sentence, or does explaining it require several caveats?
- How are module boundaries enforced — convention, code review, or something structural like package boundaries?
- What's the most tangled part of the system, and does everyone agree on which part that is?

**Red flags:** a one-line change routinely requires touching a dozen files across unrelated areas; shared mutable state or global objects are the main way modules communicate; nobody can draw the module boundaries without arguing about where they actually are.

### 3.5 Scalability & Performance

**Why it matters:** Systems that aren't built or tested against real load expectations tend to work fine in demos and fail exactly when success — a traffic spike, a big customer — makes failure most costly.

**What good looks like:** Load expectations are explicit, the system has been tested against them (not just assumed to hold), and there's a known plan for what breaks first as load grows and what to do about it.

**Questions to ask:**
- What load is the system actually designed to handle, and where is that number written down?
- When was the last load or performance test, and what did it find?
- What's the first thing that breaks as traffic doubles — is that known, or a guess?
- Can you point to a real incident caused by scale, and what changed afterward?

**Red flags:** "it's fine, we've never had a problem" as the entire performance strategy; no load testing has ever been run; performance work only happens reactively, during or after an incident.

### 3.6 Resilience & Fault Tolerance

**Why it matters:** Dependencies fail — networks drop, third-party APIs time out, instances crash — and a system that assumes everything downstream always works will eventually take a partial failure and turn it into a total outage.

**What good looks like:** Failure modes are anticipated, isolated so they don't cascade, and the system degrades gracefully — with retries, timeouts, and circuit breakers used deliberately rather than as an afterthought bolted on after an incident.

**Questions to ask:**
- What happens right now if the system's most critical dependency goes down for five minutes?
- Are there timeouts and retries on external calls, and were they set deliberately or left at library defaults?
- What's the last outage caused by a single point of failure, and has that class of failure been addressed since?
- Has failure injection or chaos testing ever been run, or is resilience purely theoretical?

**Red flags:** a single dependency failing takes down unrelated functionality; retries with no backoff turn a blip into a self-inflicted overload; nobody knows what the actual blast radius of a given failure would be.

### 3.7 Data Architecture

**Why it matters:** Data models and ownership decisions are among the hardest things to change after the fact; unclear ownership or inconsistent guarantees produce corruption, duplicated sources of truth, and migrations everyone dreads.

**What good looks like:** Each piece of data has one clear owner, schemas evolve through a deliberate migration process, and consistency guarantees are understood and matched to what each use case actually needs.

**Questions to ask:**
- For any given piece of data, who or what system owns it, and is that ownership documented?
- What's the process for a schema migration — is it tested, reversible, and does it have a rollback plan?
- Where does the system rely on eventual consistency, and does everyone touching that data know it?
- What's the last data integrity issue, and what allowed it to happen?

**Red flags:** the same piece of data is written by multiple services with no clear source of truth; migrations are run manually against production with no rollback plan; nobody can say with confidence whether a given read is strongly or eventually consistent.

### 3.8 APIs & Integrations

**Why it matters:** APIs are contracts other teams and systems depend on; breaking one silently — or having no versioning strategy at all — turns an internal change into someone else's outage.

**What good looks like:** External and internal contracts are documented, versioned deliberately, and changes are tested against real consumers before they ship, with a clear deprecation path when something has to change.

**Questions to ask:**
- Is there a versioning strategy for APIs, and has it ever actually been exercised for a breaking change?
- How would the team find out if a change broke a consumer — proactively, or when that consumer complains?
- Are integration contracts documented somewhere a consumer could find without asking a person?
- What's the last integration that broke in production, and why wasn't it caught earlier?

**Red flags:** breaking changes ship without notice to consumers; no integration tests exist against real or realistic dependencies; API documentation is stale or doesn't exist, so consumers reverse-engineer behavior from the code.

### 3.9 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
