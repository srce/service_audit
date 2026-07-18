# 6. Security & Compliance

Part of the [Software Project Maturity Assessment](../ASSESSMENT.md) — spec version 0.1.1.

### 6.1 Security Requirements

**Why it matters:** Security bolted on after design is always more expensive and less complete than security considered from the start; without an explicit threat model, teams defend against whatever they happened to think of rather than what actually threatens the system.

**What good looks like:** A lightweight threat model exists for the system, is revisited when the architecture changes meaningfully, and translates into concrete controls that are tracked rather than left as good intentions.

**Questions to ask:**
- Has anyone written down what or who this system needs to be protected from, and when was that last revisited?
- Can you point to a specific control that exists because of an identified threat, not just as a generic best practice?
- When a new feature touches sensitive functionality, does threat modeling happen before or after it ships?
- Who owns security requirements — is it a named responsibility or does it fall through the cracks between product and engineering?

**Red flags:** no threat model exists in any form, written or verbal; security is "whatever the framework does by default"; security requirements are discovered retroactively, after an incident or audit.

### 6.2 Sensitive Data Protection

**Why it matters:** Data that's exposed, over-collected, or under-protected turns a routine breach into a reportable, reputation-damaging incident, and the cost of getting this wrong is borne long after the original engineering decision is forgotten.

**What good looks like:** Sensitive data is classified, encrypted at rest and in transit, masked or tokenized where full values aren't needed, and collected only when there's a real, current use for it.

**Questions to ask:**
- Can you list the categories of sensitive data this system stores, and who classified them as sensitive?
- Where does encryption stop — is anything sensitive stored or logged in plaintext, including in backups or logs?
- Who has access to raw sensitive data, and is that access narrower than "anyone with database credentials"?
- What's collected today that nobody actually uses — has data minimization ever been revisited?

**Red flags:** sensitive fields show up unmasked in application logs or error trackers; "we encrypt the database" is the entire answer with no detail on what, how, or key ownership; data is retained indefinitely because deleting it was never someone's job.

### 6.3 Input Validation

**Why it matters:** Every external entry point — API, form, file upload, webhook, message queue — is a place an attacker or a malformed client can inject something the system wasn't built to handle; validation at the boundary is what keeps bad input from becoming a bad outcome deeper in the system.

**What good looks like:** All external inputs are validated and sanitized at the boundary using a consistent approach, validation failures are rejected with a clear response rather than silently coerced, and the same rules are enforced regardless of which entry point is used.

**Questions to ask:**
- Can you walk through what happens when malformed or unexpected input hits an API endpoint — where exactly is it caught?
- Is validation applied consistently across all entry points, or does it depend on which developer built that endpoint?
- Has an injection-class vulnerability (SQL, command, template, XSS) ever been found here, and how was it caught?
- What happens to input that fails validation — is it logged, alerted on, or does it just disappear?

**Red flags:** validation exists on some endpoints but not others, with no consistent standard; client-side validation is trusted as sufficient on its own; user-controlled input is concatenated directly into queries, commands, or templates.

### 6.4 Authentication / Authorization

**Why it matters:** Authentication answers "who is this," authorization answers "what can they do" — get either wrong and every other control is moot, because the wrong party is standing in front of the system with the wrong level of access.

**What good looks like:** Identity is verified through a modern, well-vetted mechanism (not homegrown), authorization follows least privilege with roles or policies that are reviewed periodically, and privilege escalation requires a deliberate, auditable action.

**Questions to ask:**
- Is authentication built on a standard, vetted mechanism, or does the system roll its own session or token handling?
- Can you trace how a permission check actually happens for a sensitive action — is it enforced centrally or scattered across the codebase?
- When was access and role assignment last reviewed for staleness — do former employees or unused service accounts still have access?
- What's the most privileged role in the system, who holds it, and how is that access justified?

**Red flags:** authorization checks are duplicated ad hoc in each handler instead of centralized; roles were assigned once and never revisited; a homegrown password or session scheme exists instead of a standard library or provider.

### 6.5 Credentials

**Why it matters:** Passwords, API keys, and service tokens that are hardcoded, shared, or never rotated turn a single leaked value into standing, often invisible access — and the leak is frequently discovered only after it's been exploited.

**What good looks like:** Credentials for people and services live in a secrets manager, are never committed to source control, are scoped to the minimum needed, and are rotated on a schedule or automatically rather than only after a suspected compromise.

**Questions to ask:**
- Where do secrets actually live today — a vault, environment variables, or somewhere they could end up in version control?
- When did any given credential — a database password, an API key — last rotate, and was that on a schedule or reactive?
- If a specific credential leaked right now, how would the team find out, and how long would it take to revoke it?
- Are credentials scoped narrowly per service, or does one shared key unlock more than it needs to?

**Red flags:** secrets found in git history, config files, or Slack messages; a shared credential used across multiple services or environments with no way to revoke one without breaking the others; rotation has never happened for a long-lived credential.

### 6.6 Key Management

**Why it matters:** Cryptographic keys are what make encryption meaningful — a well-encrypted system with poorly managed keys is only as secure as wherever those keys sit unprotected, and losing or leaking a key can be as damaging as never encrypting at all.

**What good looks like:** Encryption and signing keys are generated, stored, and rotated through a dedicated key management system (not alongside application secrets), access to keys is scoped and audited, and there's a defined process for rotation and for responding to a suspected key compromise.

**Questions to ask:**
- Where do cryptographic keys live, and is that separate from where application credentials and secrets are stored?
- Who can access or use a signing or encryption key directly, and is every use of it logged?
- What's the key rotation policy, and has it actually been exercised — not just written down?
- If a key were suspected of being compromised today, is there a rehearsed process for revoking and replacing it without an outage?

**Red flags:** encryption keys stored alongside the data they protect, or in the same secrets store with no distinction from application credentials; no audit trail of key usage or access; a key has been in use since the system launched with no rotation ever performed.

### 6.7 Vulnerability Management & Dependency Scanning

**Why it matters:** Exploitable weaknesses show up across containers, base images, running infrastructure, and cloud configuration — not just application dependencies — and without an org-wide program for finding and triaging them, coverage gaps go unnoticed until an attacker finds them first.

**What good looks like:** Automated scanning covers every surface — container images, infrastructure, cloud configuration, running services — on a regular cadence, findings roll up to a single triage process with clear ownership and severity-based SLAs, and escalation for critical findings is documented and governed at the organization level rather than left to whichever team owns the affected system. Day-to-day dependency patching hygiene is assessed in [4.14](04-code-quality.md#414-dependency-security--updates); this item covers the organization-wide scanning and triage program.

**Questions to ask:**
- What surfaces are covered by the scanning program — containers, infrastructure, cloud config, running services — and which ones, if any, aren't?
- Who owns the org-wide triage process, and does every team's findings feed into it, or do some teams run their own silently?
- What's the governed SLA by severity, and can you show a critical infrastructure finding that met — or missed — it?
- If a new scanning gap opened up (a new service, a new cloud account), how would the program notice?

**Red flags:** scanning exists for code dependencies but nothing covers containers, infrastructure, or cloud configuration; each team runs its own ad hoc scanning with no org-wide rollup or shared SLA; a critical infrastructure or container finding sat unactioned because no one owned triage outside the application layer.

### 6.8 Penetration Testing / Audits

**Why it matters:** Automated scanning catches known vulnerability patterns, but only an adversarial human test — internal or external — reliably surfaces the logic flaws, chained exploits, and business-context weaknesses that tools miss.

**What good looks like:** Penetration tests or security audits happen on a defined cadence or before major changes, findings are tracked to remediation with real deadlines, and the team treats results as input to prioritization rather than a compliance artifact to file away.

**Questions to ask:**
- When was the last penetration test or security audit, who performed it, and what was the highest-severity finding?
- Of the findings from the last test, how many were actually remediated, and how many are still open?
- Is testing triggered by a schedule, a compliance requirement, or only after something already went wrong?
- Does anyone outside the security or compliance function ever see the results, or does the report go straight to a drawer?

**Red flags:** the most recent test is more than a year old, or one has never been performed; findings from the last test are still open with no remediation plan; testing exists solely to produce a document for a customer or auditor, with no intent to act on it.

### 6.9 Incident Response Process

**Why it matters:** Every system eventually has a security incident; whether that incident is contained in hours or festers for weeks depends entirely on whether detection, response, and communication were planned before the pressure was on, not improvised during it.

**What good looks like:** Detection mechanisms are in place, a written incident response plan defines roles and escalation paths, the plan has actually been exercised (not just written), and every real incident produces a blameless post-mortem with tracked follow-through.

**Questions to ask:**
- Is there a written incident response plan, and when did the team last run a drill or tabletop exercise against it?
- Walk through the last real security incident — how was it detected, and how long from detection to containment?
- Who has authority to declare an incident and make containment decisions at 2am, and do they know that role is theirs?
- What did the last post-mortem produce, and were those action items actually completed?

**Red flags:** no written incident response plan exists, or one exists but has never been rehearsed; the last incident was discovered by a customer or the public before the team noticed internally; post-mortems happen but their action items are rarely followed up on.

### 6.10 Compliance & Data Retention Policies

**Why it matters:** Regulatory and contractual obligations carry real legal and financial consequences, and retention policies that are undefined or unenforced mean the organization is either holding data it has no right to keep or unable to produce data it's obligated to retain.

**What good looks like:** Applicable compliance obligations are operationalized into concrete, enforced controls, data retention and deletion schedules are defined per data category and actually executed (not just documented), and evidence of compliance can be produced on demand rather than assembled under pressure. Which obligations apply to the product is assessed in [1.8](01-product-vision.md#18-compliance--legal-requirements); this item covers how retention and compliance are operated.

**Questions to ask:**
- For a given data category, what's the defined retention period, and can you show it's actually enforced rather than just written down?
- If an auditor asked for evidence of a specific control right now, how long would it take to produce it?
- Who owns day-to-day compliance operations, and is that distinct from whoever decided which obligations apply?
- Has a data deletion or retention request (e.g., a user's right-to-erasure request) ever been tested end to end?

**Red flags:** retention policy exists as a document but no automated or manual process enforces it; data past its retention date is still sitting in production or backups; compliance evidence has to be reconstructed from scratch every time it's requested rather than being readily available.

### 6.11 Other

Anything important to this category that the items above did not cover. Record it here with an importance and state rating like any other item.
