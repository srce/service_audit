# 2. Processes & Collaboration

Part of the [Software Engineering Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.0.

### 2.1 Onboarding Process

**Why it matters:** How a new hire spends their first weeks predicts how long it takes them to become productive and whether they form an accurate mental model of the codebase — or a folklore one passed down in hallway conversations.

**What good looks like:** New team members follow a documented path that gets them to a first meaningful commit within days, with a clear point of contact and materials that are actually kept current.

**Questions to ask:**
- What did the last new hire do on their first day, and who decided that?
- How long did it take the most recent hire to ship their first real change?
- Is there a written onboarding checklist or guide, and when was it last used successfully?
- What did the last new hire get wrong or confused about that the docs should have covered?

**Red flags:** onboarding is "shadow someone for a week and figure it out"; the onboarding doc is a year old and references tools that no longer exist; new hires' first questions go unanswered for days.

### 2.2 Roles and Responsibilities

**Why it matters:** When ownership of a domain is fuzzy, decisions stall waiting for someone to claim them, or get made twice by people unaware of each other's work.

**What good looks like:** Everyone can name who owns product, engineering, QA, and other key domains, and those owners are the ones actually consulted when decisions in their area come up.

**Questions to ask:**
- Who owns this codebase, this feature, this decision — can you name them without checking a wiki?
- What happens when a decision falls between two roles — who resolves it?
- Has anyone left recently, and did their responsibilities have a clear successor?
- Can you point to a recent case where unclear ownership caused a delay or a duplicated effort?

**Red flags:** "it's kind of everyone's job"; ownership is only documented in an org chart nobody references day to day; the same decision gets re-litigated because no one remembers who made it the first time.

### 2.3 Methodologies and Frameworks

**Why it matters:** A team's stated methodology only matters if it's actually practiced; a mismatch between the label on the wall and the work on the ground creates friction and false expectations for anyone new.

**What good looks like:** The team can describe the process it actually follows — whether that's Scrum, Kanban, dual-track, or something bespoke — and that description matches what an observer would see in a normal week.

**Questions to ask:**
- What methodology does the team say it follows, and does a week of observation match that description?
- What parts of the "official" process get skipped in practice, and why?
- Who decided on this methodology, and has it been revisited since?
- What would change if the team switched frameworks tomorrow — anything, or just vocabulary?

**Red flags:** ceremonies happen because the calendar says to, not because they produce a decision; the process was copied from a book or a previous company without adaptation; the team can't explain why they do it this way.

### 2.4 Communications

**Why it matters:** Information that doesn't reach the people who need it might as well not exist; poor communication cadence and channel hygiene quietly recreates silos even on a small team.

**What good looks like:** There's a predictable rhythm and a small number of well-understood channels for different kinds of communication, and important information reliably reaches the people who need to act on it.

**Questions to ask:**
- If something important happened yesterday, how would you find out — and how long would it take?
- How many different channels (Slack, email, tickets, meetings) does someone need to check to stay informed?
- What was the last time an important update got missed because of where it was posted?
- How do updates reach people who were out or on a different team?

**Red flags:** critical decisions get made in a DM that nobody else can see; "check the thread" as a standard response; announcements duplicated across five channels with no single source of truth.

### 2.5 Task Management

**Why it matters:** Without a shared, trustworthy view of what's in flight and what's done, planning becomes guesswork and work quietly falls through the cracks.

**What good looks like:** Tickets have a consistent format and a clear definition of ready and done, the board reflects reality without heavy manual upkeep, and anyone can tell what's actually being worked on right now.

**Questions to ask:**
- What does "done" mean for a ticket here — is it written down or tribal knowledge?
- Can you trust the board right now, or does it need a cleanup pass before it's accurate?
- How does work that isn't a ticket yet (a hallway request, an urgent bug) enter the system?
- What's the oldest open ticket, and does anyone know its actual status?

**Red flags:** the board is updated only right before a status meeting; "definition of done" varies by person; work happens outside the tracking system entirely and gets reconciled after the fact, if at all.

### 2.6 Prioritization and Decision Making

**Why it matters:** Every team has more good ideas than capacity; how trade-offs get decided — and who gets a say — determines whether the team builds the right things or just the loudest requests.

**What good looks like:** There's a known process for weighing competing priorities, the people with relevant context are actually involved, and the reasoning behind a call is visible enough to be revisited later.

**Questions to ask:**
- Who decided what the team is working on this week, and what informed that choice?
- Can you point to a recent trade-off decision and explain why it went the way it did?
- What happens when an urgent request conflicts with planned work — is there a process, or does it depend on who shouts loudest?
- How does the team distinguish between someone's opinion and an informed decision?

**Red flags:** priorities shift based on who last talked to a stakeholder; decisions have no visible rationale, only an outcome; the most senior voice in the room wins regardless of the argument.

### 2.7 Project Estimation

**Why it matters:** Estimates drive commitments to stakeholders, staffing, and sequencing; when they're systematically wrong and nobody checks, planning becomes theater and trust erodes with every missed date.

**What good looks like:** Sizing is produced with a repeatable method, estimates are compared against actuals afterward, and the team's calibration visibly improves — or at least the gap is acknowledged and worked around.

**Questions to ask:**
- How was the last estimate produced — gut feel, a formal technique, historical data?
- Does anyone compare estimates to actuals afterward, and what did the last comparison show?
- What happens when a deadline was committed before the estimate existed?
- How does uncertainty get communicated — as a range, a confidence level, or a single number treated as fact?

**Red flags:** estimates are demanded before requirements are understood; a single number is quoted upward and treated as a promise; nobody ever revisits whether estimates were close.

### 2.8 Code Reviews

**Why it matters:** Code review is often the only point where a second engineer engages deeply with a change before it ships; when it's a rubber stamp, the team loses its main defense against design mistakes and knowledge silos.

**What good looks like:** Reviews happen promptly, reviewers engage with design and correctness rather than just style, and the process catches real problems often enough that people take it seriously.

**Questions to ask:**
- How long does a typical pull request wait for its first review comment?
- What's the last piece of substantive feedback a review caught before merge — not a typo, an actual design or correctness issue?
- Is there a required number of approvals, and is it ever bypassed — by whom, and how often?
- How do reviewers handle disagreement with the author — is there a resolution process, or does it default to whoever's more senior?

**Red flags:** approvals given without evidence the diff was read; reviews consistently take days, so people route around them; large PRs get a single "LGTM" with no comments.

### 2.9 Retrospectives and Feedback

**Why it matters:** Teams that don't pause to reflect repeat the same mistakes; retrospectives are the mechanism for turning lived experience into process change, and their absence shows up as recurring, never-fixed friction.

**What good looks like:** Retrospectives happen on a predictable cadence, produce specific action items with owners, and those action items are checked on later rather than forgotten the moment the meeting ends.

**Questions to ask:**
- What action item came out of the last retro, and what's its status today?
- How many retros in a row have raised the same unresolved issue?
- Does feedback flow both ways — do individual contributors get to raise process problems, not just report on tickets?
- What would have to happen for a retro action item to actually get prioritized against feature work?

**Red flags:** retros happen but produce no written action items; the same complaint resurfaces every retro with no visible attempt to fix it; the meeting is treated as a formality to get through, not a working session.

### 2.10 Ground Rules

**Why it matters:** Unstated norms around meetings, communication, and behavior default to whatever the most dominant personalities model, which can quietly exclude quieter voices or create friction nobody names directly.

**What good looks like:** Basic norms — meeting etiquette, response-time expectations, how disagreement is handled — are written down somewhere, referenced when they're violated, and revisited as the team changes.

**Questions to ask:**
- Are there written team norms, and can someone point to where they live?
- What happens when someone consistently violates a norm — is it addressed, or quietly tolerated?
- How were these norms decided — by the whole team, or handed down?
- When did the ground rules last get updated, and what prompted the change?

**Red flags:** norms exist only as unwritten expectations that new members have to guess at; violations are tolerated from senior people but not from others; the rules haven't been revisited since the team's headcount doubled.

### 2.11 Decision Records (ADR)

**Why it matters:** Without a record of why a significant decision was made, the reasoning leaves with the people who were in the room, and future engineers either repeat the debate from scratch or violate a constraint they don't know exists.

**What good looks like:** Significant architectural and process decisions are captured in a lightweight, consistent format, are easy to find, and are referenced when a related decision comes up later.

**Questions to ask:**
- Where do architectural decisions get recorded, and how many exist?
- Pick a major technical choice made in the last year — is the reasoning written down anywhere?
- When was the last time someone consulted an old ADR before making a related decision?
- What decisions should have an ADR but don't?

**Red flags:** "we don't really do ADRs, people just remember"; the ADR log exists but hasn't been touched in over a year despite significant changes happening; records exist but are never referenced, so decisions get silently re-litigated.

### 2.12 Cross-Team Collaboration

**Why it matters:** Most real work crosses team boundaries — engineering needs design, QA, DevOps, or another engineering team — and the quality of that handoff determines whether work flows or stalls at every interface.

**What good looks like:** Interfaces between teams are clear, dependencies are surfaced early, and there's a known way to resolve conflicts or blockers that doesn't require escalating to management every time.

**Questions to ask:**
- What's the last piece of work that depended on another team, and how smoothly did that handoff go?
- How far in advance do cross-team dependencies typically get identified — before or after they become blockers?
- When two teams disagree about an interface or a timeline, how does that get resolved?
- Is there a standing forum or contact point for coordinating with other teams, or does it happen ad hoc?

**Red flags:** dependencies are discovered the week they're due; cross-team requests routinely sit unanswered; every disagreement between teams escalates to a manager instead of being resolved peer to peer.

### 2.13 Stakeholder Management

**Why it matters:** Stakeholders who feel uninformed or unheard tend to escalate, micromanage, or lose trust in the team's judgment — all of which cost more time than proactively keeping them in the loop.

**What good looks like:** Key stakeholders are identified explicitly, there's a regular cadence for keeping them updated, and their input is gathered before decisions are finalized rather than after.

**Questions to ask:**
- Who are the key stakeholders for this product, and can the team name them without hesitation?
- How and when do stakeholders find out about scope changes or delays — before or after the fact?
- What's the last time a stakeholder was surprised by something the team already knew?
- How is stakeholder feedback gathered, and where does it go once collected?

**Red flags:** stakeholders learn about slipped deadlines in a status meeting instead of proactively; "stakeholder management" means damage control after a surprise, not a standing practice; no one can list the stakeholders for a given initiative.

### 2.14 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
