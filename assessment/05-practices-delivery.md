# 5. Engineering Practices & Delivery

Part of the [Software Project Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.1.

### 5.1 Version Control System

**Why it matters:** The branching strategy and history shape how safely and quickly changes move from a developer's machine to production; a confused strategy creates merge pain and hides what's actually deployed where.

**What good looks like:** A documented, consistently followed branching strategy maps cleanly to the release process, commit history is legible, and tags or version markers make it possible to know exactly what code is running anywhere.

**Questions to ask:**
- Can you describe the branching strategy from memory, and does the actual repo history match that description?
- How do you know, right now, exactly what code is deployed to production versus what's in the default branch?
- What happens when two people need to work on unrelated changes at the same time — does the workflow support that cleanly?
- What's the last time a merge went wrong, and what about the branching model made it possible?

**Red flags:** long-lived branches that drift for months before merging; tags that don't correspond to what's actually deployed; commit history full of "fix," "wip," and "asdf" with no way to reconstruct why a change was made.

### 5.2 Project Installation

**Why it matters:** How easily a new machine can be brought to a working local setup determines onboarding speed and how often "works on my machine" derails a debugging session.

**What good looks like:** A documented, scripted setup gets a new contributor from a clean checkout to a running local environment in one or two commands, with dependencies and prerequisites pinned and explicit.

**Questions to ask:**
- How long did it take the last new hire to get a fully working local environment, and how much of that required someone's help?
- Is setup a single documented command, or a checklist of steps that has to be followed exactly in order?
- What happens if you follow the setup instructions on a completely clean machine today — do they still work?
- How are OS or environment differences (Mac vs. Linux vs. containers) handled?

**Red flags:** setup docs that are known to be stale; "ask Dave" is the actual onboarding process; setup only works because of undocumented local state on existing developers' machines.

### 5.3 Project Launch

**Why it matters:** Standing up a new environment or deploying the product for the first time is a rare enough event that undocumented tribal knowledge disappears exactly when it's needed most.

**What good looks like:** A written, current playbook covers what it takes to launch the project into a new environment end-to-end, and someone outside the usual owner could follow it without live coaching.

**Questions to ask:**
- If the person who usually handles launches was unavailable, could someone else follow existing docs to stand up a new environment?
- When was this playbook last actually used, and did it work as written or need live fixes?
- What manual, undocumented steps still happen during a launch that live only in someone's head?
- What's the biggest surprise the last time this process ran?

**Red flags:** the playbook exists but hasn't been executed by anyone except its author; steps that only work because one person remembers an undocumented gotcha; no playbook at all — launches happen "by feel."

### 5.4 Project Build

**Why it matters:** The build is the boundary between source code and a deployable artifact; if it's slow, inconsistent, or opaque, every downstream step inherits that uncertainty.

**What good looks like:** Builds are reproducible from a clean checkout, fast enough not to bottleneck delivery, versioned and stored in a way that any past artifact can be retrieved, and their output is a known, verifiable unit.

**Questions to ask:**
- Can you rebuild last month's release artifact byte-for-byte from source, or has that become impossible?
- How long does a full build take, and has that time been trending up?
- Where are built artifacts stored, and how far back can you retrieve one?
- What's the last time a build succeeded locally but failed — or behaved differently — in CI or production?

**Red flags:** builds that only work on one person's machine; no artifact retention beyond the current release; build steps that silently depend on external network state or unpinned tool versions.

### 5.5 Project Testing

**Why it matters:** Regression and pre-release testing is the last line of defense before code reaches users, catching what unit and integration tests upstream in the codebase didn't — including interactions across the whole system as it will actually run.

**What good looks like:** A defined regression suite runs automatically before every release, covers the paths that matter most to users, and a release doesn't ship until it passes — with clear ownership for maintaining and triaging it.

**Questions to ask:**
- What runs automatically between "code is merged" and "release goes out," and what still requires a human to click through manually?
- Has a release ever shipped with the regression suite red, and if so, under what justification?
- How is this regression testing different from the unit/integration tests that already run in CI — what does it catch that they don't?
- What's the last regression that reached production because pre-release testing didn't cover that path?

**Red flags:** "we do a manual pass before every release" as the entire strategy; regression suite is stale and no longer reflects current critical paths; releases proceed regardless of test results because "it's probably fine."

### 5.6 Automation

**Why it matters:** Manual, repetitive operational work is slow, inconsistent between people, and a constant source of small mistakes that automation would eliminate entirely.

**What good looks like:** Routine operational tasks — dependency bumps, changelogs, environment provisioning, repetitive checks — are automated with scripts or bots, and the team actively looks for the next manual task worth automating.

**Questions to ask:**
- What's a task the team does by hand every week that could plausibly be scripted, and why hasn't it been?
- What automation exists today (bots, scheduled jobs, GitHub Actions), and who maintains it when it breaks?
- How much of the release or deployment process still requires a human to run a manual command at the right time?
- What's the last piece of automation that broke silently and nobody noticed for a while?

**Red flags:** automation scripts nobody currently on the team understands or maintains; the same manual, error-prone task performed by hand every single release; bots or automation that fail silently with no alerting.

### 5.7 Optimizations

**Why it matters:** Without deliberate attention, systems tend toward accumulating waste — slow paths, redundant work, unnecessary resource use — that compounds as the system grows.

**What good looks like:** Performance and efficiency work is driven by measurement, not guesswork, targets the paths that actually matter to users or cost, and is revisited periodically rather than only after something breaks.

**Questions to ask:**
- What's the last performance or efficiency improvement made, and how was the target identified — measurement or hunch?
- Is there a known slow path or expensive operation everyone's aware of but nobody has prioritized fixing?
- How is performance regression caught — is it measured continuously or only noticed when a user complains?
- What tradeoffs were made the last time something was optimized — did it cost readability, flexibility, or reliability?

**Red flags:** optimization work driven entirely by anecdote rather than profiling or metrics; a known-slow critical path nobody has scheduled time to address; premature optimization that added complexity without measurable benefit.

### 5.8 Multiple Environments

**Why it matters:** The gap between staging (or any pre-production environment) and production is where "it worked in testing" bugs come from; the closer the parity, the more the team can trust results from earlier environments.

**What good looks like:** Environments are clearly defined with a real purpose each, configuration differences between them are minimal and explicit, and promotion between environments follows a consistent, known path.

**Questions to ask:**
- What environments exist today, and can everyone on the team name the purpose of each without hesitation?
- How different is staging's configuration, data, and scale from production — and does that difference ever cause surprises?
- What's the last bug that only showed up in production because an earlier environment didn't catch it?
- Is there an environment that's supposed to mirror production but has quietly drifted out of sync?

**Red flags:** staging configuration diverges so much from production that passing there means little; an environment that exists but no one remembers why or trusts; promotion between environments is ad hoc rather than a repeatable process.

### 5.9 Release Management Process

**Why it matters:** How a release gets approved, scheduled, and communicated determines whether shipping is a routine, low-stress event or a high-anxiety scramble every time.

**What good looks like:** Releases follow a known cadence or clear trigger, have defined approval gates appropriate to their risk, and produce release notes or communication that lets stakeholders know what changed.

**Questions to ask:**
- Who has to approve a release before it ships, and does that approval reflect real risk assessment or is it a formality?
- How often does the team release, and is that cadence a deliberate choice or just "whenever"?
- Where do release notes come from — are they written deliberately or reconstructed after the fact from commit messages?
- What's the last release that went out without anyone outside engineering knowing it happened?

**Red flags:** releases happen with no consistent process — different every time depending on who's driving; approval gates that exist on paper but are routinely skipped under deadline pressure; no communication to stakeholders about what shipped or when.

### 5.10 Recovery Plan

**Why it matters:** Every deployment pipeline eventually ships something broken; what separates a minor blip from a prolonged outage is whether rollback and recovery are rehearsed rather than improvised under pressure.

**What good looks like:** Rollback is a fast, well-understood, low-risk operation, hotfix paths exist for urgent patches without going through the full release cycle, and worst-case recovery procedures have actually been tested, not just documented.

**Questions to ask:**
- How long does it take to roll back a bad release right now, and when was that last actually exercised — not just discussed?
- Is there a fast path for an urgent hotfix, or does every fix have to go through the full normal release process?
- What's the worst-case recovery scenario (data loss, full outage), and has a plan for it ever been tested end-to-end?
- Who is authorized to trigger a rollback, and are they available outside business hours?

**Red flags:** rollback has never actually been tested, only assumed to work; recovery procedures exist only as a document nobody has rehearsed; a single person is the only one who knows how to execute recovery.

### 5.11 Observability

**Why it matters:** Without logs, traces, and dashboards that reflect what the system is actually doing, diagnosing a production problem becomes guesswork under pressure instead of a directed investigation.

**What good looks like:** Logging and tracing provide enough context to reconstruct what happened during an incident without reproducing it, dashboards reflect the metrics that actually matter to the business and system health, and instrumentation is added as a normal part of building a feature.

**Questions to ask:**
- When the last incident happened, could the team reconstruct the sequence of events from logs and traces alone, or did it require guesswork?
- Are dashboards something the team actually looks at day to day, or do they exist and go unopened?
- How is a new feature instrumented — is adding logging/tracing part of the definition of done, or an afterthought?
- Can you trace a single request across every service it touches, or does visibility stop at a service boundary?

**Red flags:** logs exist but lack the context needed to actually diagnose anything; dashboards that were built once and never revisited as the system changed; tracing that stops at the first service boundary with no cross-service visibility.

### 5.12 Monitoring & Alerting Quality

**Why it matters:** Monitoring and alerting are what turn observability data into action — the difference between a well-tuned alerting system and a noisy one is the difference between fast incident response and alert fatigue that causes real problems to be ignored.

**What good looks like:** Alerts map to defined SLOs/SLIs, firing on conditions that actually require human action, response workflows are clear about who gets paged and what they do next, and alert noise is actively tracked and reduced.

**Questions to ask:**
- What percentage of alerts in a typical week require real action versus getting dismissed or ignored?
- Are there defined SLOs/SLIs, and do alerts actually map to breaches of them?
- When an alert fires at 3am, does the responder know exactly what to do, or are they figuring it out live?
- What's the last real incident that didn't generate an alert until a user reported it?

**Red flags:** alert fatigue so bad that pages get muted or ignored by default; no defined SLOs, so "alert-worthy" is whatever someone decided in the moment; the same noisy alert firing for months with nobody fixing its root cause.

### 5.13 CI/CD

**Why it matters:** The CI/CD pipeline is the automated gate between a commit and a deployed change; how much it actually enforces — versus how much it merely reports — determines how much the team can trust "green" to mean "safe to ship."

**What good looks like:** Every change passes through automated quality gates (tests, linting, security checks) before merge, deployment is automated and repeatable rather than a manual sequence of commands, and pipeline failures block progress rather than being routinely overridden.

**Questions to ask:**
- What quality gates actually block a merge or deploy, versus which ones just report status that people ignore?
- How much of deployment is a single automated action versus a human running commands in a particular order?
- How often is a pipeline failure overridden or bypassed to ship anyway, and by whom?
- What's the time from merge to production right now, and where does most of that time go?

**Red flags:** pipeline failures routinely overridden under deadline pressure; deployment still requires a human to run manual steps in the right order; quality gates exist but are advisory rather than blocking.

### 5.14 Infrastructure as Code (IaC)

**Why it matters:** Infrastructure that exists only as manual console clicks is undocumented, unreviewable, and impossible to reliably reproduce; treating infrastructure as versioned code brings it the same rigor as application code.

**What good looks like:** Infrastructure is defined declaratively in version-controlled code, changes go through the same review process as application code, and environments can be reliably recreated from that code alone.

**Questions to ask:**
- Could the production environment be recreated from code alone, or does it depend on manual configuration nobody wrote down?
- Do infrastructure changes go through code review the same way application changes do?
- What's the last infrastructure change made directly in a cloud console rather than through code?
- Is there drift between what the IaC defines and what's actually running — has anyone checked recently?

**Red flags:** critical infrastructure configured by hand and never captured in code; infrastructure changes made directly in a console with no review trail; known drift between declared infrastructure and actual running state.

### 5.15 Cost Efficiency / Cloud Optimization (FinOps)

**Why it matters:** Cloud and infrastructure spend that goes unexamined tends to grow faster than usage justifies, and by the time it becomes a visible problem it's often deeply entangled with the architecture.

**What good looks like:** Spend is tracked, attributed to teams or services, and reviewed on a regular cadence with clear ownership for acting on waste — not just reported, but actually optimized.

**Questions to ask:**
- Who owns cloud spend, and when was it last reviewed with an eye toward cutting waste rather than just reported?
- Can spend be attributed to specific services or teams, or is it one undifferentiated bill?
- What's the last piece of obviously wasted spend (idle resources, oversized instances) that was found and eliminated?
- Are cost implications considered when architecture or infrastructure decisions are made, or only discovered after the bill arrives?

**Red flags:** nobody can explain what's driving a significant fraction of the cloud bill; cost review happens rarely or never, only reported after the fact with no one acting on it; known idle or oversized resources left running because addressing them isn't anyone's job.

### 5.16 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
