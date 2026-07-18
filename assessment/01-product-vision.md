# 1. Product & Vision

Part of the [Software Project Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.1.

### 1.1 Product Overview

**Why it matters:** If the team can't articulate the product, its users, and the problem it solves in plain language, every downstream decision — architecture, prioritization, hiring — is guesswork dressed up as strategy.

**What good looks like:** Any engineer on the team can explain in a couple of minutes who the product serves, what pain it removes, and why that matters, without reaching for a slide deck.

**Questions to ask:**
- If you stopped a random engineer in the hallway, could they describe the product and its core users in two sentences?
- Who is explicitly *not* the target user, and why was that boundary drawn?
- What problem does this solve that the user couldn't solve another way before?
- When did the product overview last change, and did the team notice?

**Red flags:** the description only exists in a founder's head or a pitch deck; engineers describe the product in purely technical terms with no mention of the user; "it does everything for everyone."

### 1.2 Product Vision / Mission

**Why it matters:** Without a shared long-term direction, teams optimize locally — every sprint looks reasonable in isolation but the product drifts without accumulating toward anything.

**What good looks like:** A concise, durable statement of where the product is headed exists, is written down, and is referenced (not just recited) when weighing competing priorities.

**Questions to ask:**
- Where is the vision written down, and when was it last revisited?
- Can you give an example of a decision the vision helped settle in the last quarter?
- If two people on the team described the vision independently, would they agree?
- Has the vision changed recently — and if so, does everyone know?

**Red flags:** vision statement is generic boilerplate that could apply to any company; it hasn't been mentioned in a planning meeting in over a year; leadership and engineering describe the direction differently.

### 1.3 Project Goals

**Why it matters:** Goals translate vision into something a team can actually plan against and measure; without them, "we're moving fast" substitutes for "we're moving somewhere."

**What good looks like:** Short- and mid-term goals are explicit, tied to measurable outcomes, and revisited on a predictable cadence rather than only when something goes wrong.

**Questions to ask:**
- What are this quarter's goals, and how do they connect to a business or user outcome?
- How do you know when a goal has been achieved — what's the measurable signal?
- What was the last goal that was missed, and what happened as a result?
- How often do stated goals change mid-cycle, and why?

**Red flags:** goals are activity-based ("ship feature X") rather than outcome-based; goals exist only as a Jira epic nobody reopens; no one can name this quarter's top goal without checking a document.

### 1.4 Functional and Non-Functional Requirements

**Why it matters:** Functional requirements describe what the product does; non-functional ones (security, scalability, reliability) determine whether it survives contact with real usage. Skipping either invites rework or outages later.

**What good looks like:** Requirements are captured somewhere durable, distinguish must-have from nice-to-have, and explicitly address non-functional concerns rather than leaving them implicit.

**Questions to ask:**
- Where do non-functional requirements (performance, security, availability) get written down, if anywhere?
- For the last major feature, how were "must have" and "nice to have" distinguished?
- What happens when a requirement conflicts with a deadline — who decides what gets cut?
- Can you point to a recent incident caused by an unstated non-functional requirement?

**Red flags:** requirements live only in a ticket title; non-functional requirements are never discussed until an incident forces the conversation; "we'll figure out scale when we get there" as a standing policy.

### 1.5 Product Roadmap

**Why it matters:** A roadmap turns goals into a sequence the team and stakeholders can plan around; without one, priorities feel arbitrary and dependencies get discovered too late.

**What good looks like:** A roadmap exists, is visible to the team, names dependencies and rough timing, and is updated often enough to stay credible rather than becoming decorative.

**Questions to ask:**
- Where does the roadmap live, and who can see it?
- When was it last updated, and does it reflect what's actually being worked on right now?
- What's an example of a dependency the roadmap surfaced before it became a blocker?
- How far out does the roadmap realistically hold — weeks, quarters, longer?

**Red flags:** the roadmap is a static slide from a quarterly business review; engineers learn about upcoming priorities from stand-up rather than the roadmap; dates are treated as commitments despite being guesses.

### 1.6 User Research & Feedback Loops

**Why it matters:** Product decisions made without user input are bets; regular, structured feedback loops turn those bets into informed choices and catch misdirection early.

**What good looks like:** There's a consistent mechanism for gathering user input (interviews, support signals, usage data, beta programs) and evidence that it actually changes what gets built.

**Questions to ask:**
- What's the most recent product decision that changed because of user feedback?
- How do insights from support tickets or sales calls make it back to the product team?
- Who talks to users directly, and how often?
- If a feature flopped, how would the team find out — and how would they know why?

**Red flags:** "we know what users want" asserted without a mechanism behind it; feedback is collected but has no visible path into planning; user research happened once, long ago, and hasn't been repeated.

### 1.7 Product Metrics & Analytics

**Why it matters:** Metrics are how a team tells the difference between shipping and succeeding; without them, launches are declared wins by default rather than by evidence.

**What good looks like:** A small set of meaningful metrics (adoption, engagement, quality) is tracked, visible to the team, and actually consulted when deciding what to build next.

**Questions to ask:**
- What are the two or three metrics that most define product success here?
- Who looks at the dashboard, and how often?
- Can you describe a time a metric moved unexpectedly and what the team did about it?
- How do you distinguish a vanity metric from one that drives a decision?

**Red flags:** metrics are tracked but nobody can recall the current numbers; dashboards exist but are never opened outside of a quarterly review; success is measured only by "did we ship it," not by impact.

### 1.8 Compliance & Legal Requirements

**Why it matters:** Compliance obligations (GDPR, accessibility, industry-specific regulation) carry legal and financial risk if ignored, and retrofitting them after the fact is far more expensive than designing for them upfront.

**What good looks like:** Applicable obligations are identified explicitly, someone is accountable for tracking them, and they inform product decisions rather than being discovered during an audit or a customer's security questionnaire. How compliance is operated day-to-day is assessed in [6.10](06-security-compliance.md#610-compliance--data-retention-policies).

**Questions to ask:**
- Which specific regulations or standards apply to this product, and who determined that list?
- Who owns compliance accountability — is there a named person or is it "everyone's job, so no one's"?
- What was the last compliance gap discovered, and how was it found — audit, incident, or customer question?
- How do new features get checked against compliance obligations before they ship?

**Red flags:** compliance is treated as a one-time checkbox rather than an ongoing obligation; no one can name which regulations apply; obligations are only discovered when a customer or regulator asks.

### 1.9 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
