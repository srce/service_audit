# Coverage: The Agile Manifesto

**Source:** https://agilemanifesto.org/
**Mapped against spec version:** 0.1.1
**Last reviewed:** 2026-07-31

The assessment covers 7 of the 12 principles in full (one of those through the
practice that superseded the original wording) and 5 partially. Nothing is
left uncovered. The structural difference: the Manifesto is a statement of
values, written to argue for one way of working over another, while this
assessment is deliberately methodology-neutral. [2.3 Methodologies and
Frameworks](../assessment/02-processes-collaboration.md) asks whether the team
follows the process it says it follows, not whether that process is agile. So
this mapping is a check that the ground the Manifesto covers is assessed
somewhere, not a claim that a team ought to be agile. A team that scores well
here could be running Scrum, Kanban, or nothing with a name.

This is also the first mapping aimed at the people-and-process half of the
spec. The other four frameworks in [coverage/](README.md) are technical or
security frameworks, and categories 2 and 7 barely appear in them.

| # | Agile principle | Our item(s) | Coverage |
|---|---|---|---|
| 1 | Satisfy the customer through early and continuous delivery of valuable software | 5.13 CI/CD, 5.9 Release Management Process, 1.7 Product Metrics & Analytics | ✅ Full |
| 2 | Welcome changing requirements, even late in development | 2.6 Prioritization and Decision Making, 1.5 Product Roadmap, 3.4 Loose Coupling / High Cohesion | ⚠️ Partial |
| 3 | Deliver working software frequently | 5.9 Release Management Process, 5.13 CI/CD | ✅ Full |
| 4 | Business people and developers must work together daily | 2.13 Stakeholder Management, 2.12 Cross-Team Collaboration | ⚠️ Partial |
| 5 | Build projects around motivated individuals, give them the environment and support they need, and trust them | 7.1 Working Conditions, 7.5 Team Health & Culture, 2.2 Roles and Responsibilities | ✅ Full |
| 6 | Face-to-face conversation is the most efficient method of conveying information | 7.2 Remote Work / Hybrid Efficiency, 2.4 Communications | ✅ Full (modernized) |
| 7 | Working software is the primary measure of progress | 2.5 Task Management, 1.7 Product Metrics & Analytics | ⚠️ Partial |
| 8 | Sustainable development, a constant pace maintained indefinitely | 7.5 Team Health & Culture, 7.1 Working Conditions | ✅ Full |
| 9 | Continuous attention to technical excellence and good design | 4.6 Technical Debt, 4.4 Engineering Principles, 4.2 Patterns, 3.3 Architecture Patterns | ✅ Full |
| 10 | Simplicity, the art of maximizing the amount of work not done | 4.4 Engineering Principles, 5.7 Optimizations, 2.6 Prioritization and Decision Making | ⚠️ Partial |
| 11 | The best architectures, requirements, and designs emerge from self-organizing teams | 2.6 Prioritization and Decision Making, 2.2 Roles and Responsibilities, 2.11 Decision Records (ADR) | ⚠️ Partial |
| 12 | At regular intervals the team reflects and adjusts its behavior | 2.9 Retrospectives and Feedback | ✅ Full |

## The four values

The Manifesto's four values are framing rather than practices, so they are not
scored in the table above. Three of them are assessed indirectly through the
principles; the fourth is a place where this assessment openly leans the other
way.

- **Individuals and interactions over processes and tools.** Assessed through
  7.5 (psychological safety, whether disagreement surfaces in the open), 2.3
  (whether the process on the wall matches the work on the ground), and 2.10
  Ground Rules.
- **Working software over comprehensive documentation.** The assessment does
  not adopt this preference. It puts substantial weight on documentation in
  3.1 System Documentation, 4.11 Documentation & Domain Language, 2.11
  Decision Records, and 5.3 Project Launch. The tension is smaller than it
  looks, since every one of those items scores documentation by whether it is
  current, findable, and actually used rather than by how comprehensive it is,
  and a stale doc is a red flag in all four. But a team reading the Manifesto
  literally and this assessment literally will feel the pull in two
  directions, and that is worth naming rather than smoothing over.
- **Customer collaboration over contract negotiation.** Assessed through 1.6
  User Research & Feedback Loops and 2.13 Stakeholder Management.
- **Responding to change over following a plan.** Assessed through 2.6
  Prioritization and Decision Making and 1.5 Product Roadmap, and partially,
  since the specific gap under principle 2 applies here too.

## Notes on modernized coverage

- **#6 Face-to-face conversation.** This is the principle the industry moved
  furthest from, and 7.2 Remote Work / Hybrid Efficiency inverts it on
  purpose: it treats capturing decisions and context in writing by default as
  what good looks like, and "you had to be there" as a red flag. The
  underlying concern, that information has to actually reach the people who
  need it, is assessed directly in 7.2 and 2.4 Communications. The Manifesto's
  answer to that concern was co-location, which distributed and hybrid teams
  cannot use. Recorded as modernized rather than partial because the ground is
  fully assessed, just from the opposite premise.

## Notes on partial coverage

- **#2 Welcome changing requirements.** 2.6 asks what happens when an urgent
  request collides with planned work, and 1.5 asks how far out the roadmap
  realistically holds, but neither asks the sharp version: can a requirement
  change late without the change being treated as a failure of planning? The
  architectural half is closer, since 3.4 assesses how far a change ripples,
  but it frames that as coupling rather than as cost of change. Candidate
  question for 2.6 in a future MINOR release.
- **#4 Business people and developers work together daily.** 2.13 assesses
  whether stakeholders are kept informed on a cadence and consulted before
  decisions are final, which is adjacent but not the same thing. Working
  together daily is a collaboration model, and no question asks how close the
  working relationship actually is or whether engineers talk to the business
  side without a product manager relaying. Candidate question for 2.13.
- **#7 Working software is the primary measure of progress.** 2.5 assesses
  whether "done" is defined and whether the board reflects reality, and 1.7
  assesses whether success is measured by impact rather than by shipping. What
  is missing is the direct question: what does this team point at when asked
  how much progress it made last month, and is that working software or a
  velocity number? Candidate question for 2.5 or 2.7 Project Estimation.
- **#10 Simplicity.** 4.4 covers half of this well, and sharply: it asks for
  the most over-engineered part of the codebase and treats abstractions with a
  single implementation as a red flag. That is simplicity in code. The other
  half, maximizing the work not done, is scope discipline, and 2.6 assesses
  how priorities get decided without asking whether the team is good at
  deciding not to build something. Candidate question for 2.6.
- **#11 Self-organizing teams.** The closest the spec comes is 2.6's red flag
  that the most senior voice wins regardless of the argument, plus 2.2 on
  whether ownership is real and 2.11 on whether design reasoning is recorded.
  Team autonomy over technical direction is never asked about directly, and
  neither is whether design decisions come from the team doing the work or
  from outside it. The weakest coverage of the twelve and a reasonable
  candidate for 2.2 in a future MINOR release.
