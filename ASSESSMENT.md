# Engineering Assessment Guide

This assessment template outlines categories that help evaluate software engineering maturity and identify areas worth investigating further. Each section lists prompts that teams can use to capture current practices, identify gaps, and plan improvements.

## 1. Product & Vision
1. **Product Overview:** Summarize the product, its core users, and the problem space it addresses.
2. **Product Vision / Mission:** Clarify the long-term direction and intent underpinning the product.
3. **Project Goals:** Document short- and mid-term objectives tied to outcomes and impact.
4. **Functional and Non-Functional Requirements:** Capture what the product must do and how it must perform (security, scalability, reliability).
5. **Product Roadmap:** Outline planned initiatives, dependencies, and timing for future work.
6. **User Research & Feedback Loops:** Describe how customer insights are gathered, validated, and acted upon.
7. **Product Metrics & Analytics:** List the signals you monitor to judge success, adoption, and quality.
8. **Compliance & Legal Requirements:** Note obligations such as GDPR, accessibility, or industry-specific standards.
9. **Other**.

## 2. Processes & Collaboration

1. **Onboarding Process:** Review how new team members are introduced to the product, codebase, and workflows.
2. **Roles and Responsibilities:** Define who owns each domain (product, engineering, QA, etc.).
3. **Methodologies and Frameworks:** Document adopted approaches (Scrum, Kanban, dual-track, etc.).
4. **Communications:** Assess cadence, channels, and clarity of team updates and stakeholder outreach.
5. **Task Management:** Describe ticketing practices, definition of ready/done, and work tracking tools.
6. **Prioritization and Decision Making:** Explain how choices are made, who is involved, and what trade-offs are considered.
7. **Project Estimation:** Capture how sizing/estimates are created and validated.
8. **Code Reviews:** Outline the review process, expectations, and tooling.
9. **Retrospectives and Feedbacks:** Share the rhythm for reflection and continuous improvement.
10. **Groundrules:** Document team norms for behavior, meetings, and collaboration.
11. **Decision Records (ADR):** Note the use of architectural decision records and their storage.
12. **Cross-Team Collaboration:** Describe coordination between QA, design, DevOps, etc.
13 **Stakeholder Management:** Identify key stakeholders and how they are kept informed or consulted.
14. **Team Health & Culture:** Capture morale, psychological safety, DEI considerations, and general wellbeing.
15. **Other**.

## 3. Architecture & Systems Design

1. **System Documentation:** Note the availability and freshness of architecture diagrams, runbooks, and onboarding docs.
2. **Tech Stack:** List languages, frameworks, hosted platforms, and rationale for choices.
3. **Architecture Patterns:** Describe chosen patterns (microservices, event-driven, layered, etc.).
4. **Loose Coupling / High Cohesion:** Evaluate how well modules are decoupled and responsibilities are focused.
5. **Scalability & Performance:** Document load expectations and performance testing practices.
6. **Resilience & Fault Tolerance:** Capture strategies for failure isolation, retries, and graceful degradation.
7. **Data Architecture:** Review models, migrations, data ownership, and consistency guarantees.
8. **APIs & Integrations:** List external contracts, versioning strategy, and integration testing.
9. **Other**.

## 4. Code & Quality

1. **Relevance of Codebase:** Assess whether the current code supports evolving requirements and reflects domain knowledge.
2. **Patterns:** Identify common architectural or design patterns, and their consistency.
3. **Code Style:** Note linting rules, formatting tooling, and adherence to style guides.
4. **Engineering Principles:** Evaluate usage of SOLID, KISS, DRY, etc., and how they are enforced.
5. **Error Handling:** Document strategies for capturing, logging, and surfacing errors.
6. **Technical Debt:** Highlight known debt, remediation plans, and prioritization.
7. **Package Management:** Outline dependency management practices and version control.
8. **Unit-tests:** Explain coverage goals, how flaky tests are managed, and automation strategy.
9. **Integration & E2E Testing:** Detail higher-level tests, environments, and observability.
10. **Scaffolding / Project Layout:** Describe repository structure, tooling, and onboarding scripts.
11. **Documentation & Domain Language:** Capture how code and docs express the ubiquitous language.
12. **Static Analysis / Linting:** Note analysis tools, enforcement, and integration into pipelines.
13. **Code Ownership & Review Process Quality:** Clarify ownership boundaries and review quality.
14. **Dependency Security & Updates:** Document monitoring for vulnerabilities and update cadence.
15. **Copyright & Licenses:** Ensure licensing clarity across dependencies and the project.
16. **Other**.

## 5. Engineering Practices & Delivery

1. **Version Control System:** Describe branching strategy, tagging, and release-related conventions.
2. **Project Installation:** Document how to set up the project locally (prereqs, scripts).
3. **Project Launch:** Capture deployment/playbook steps for releasing a new environment or product.
4. **Project Build:** Review how artifacts are built, tested, and stored.
5. **Project Testing:** Outline automated/regression testing performed before releases.
6. **Automation:** Document scripts, bots, or GitHub Actions used to reduce manual work.
7. **Optimizations:** Highlight performance tuning, caching, or resource efficiency efforts.
8. **Multiple Environments:** Explain staging, production, and any intermediate environments.
9. **Release Management Process:** Describe gating, approvals, and release notes generation.
10. **Recovery Plan:** Capture procedures for rollbacks, hotfixes, and catastrophe response.
11. **Observability:** Detail logging, tracing, and dashboards used post-release.
12. **Monitoring & Alerting Quality:** Assess alert noise, SLO/SLI coverage, and response workflows.
13. **CI/CD:** Explain how pipelines automate quality gates and deployments.
14. **Infrastructure as Code (IaC):** Document how infrastructure definitions are stored and versioned.
15. **Cost Efficiency / Cloud Optimization (FinOps):** Note practices for tracking and optimizing spend.
16. **Other**.

## 6. Security & Compliance

1. **Security Requirements:** List threat models, compliance requirements, and associated controls.
2. **Sensitive Data Protection:** Describe encryption, masking, and storage practices.
3. **Input Validation:** Document validation/sanitization approaches on all entry points.
4. **Authentication / Authorization:** Outline identity management, roles, and access controls.
5. **Credentials:** Note vaulting practices and rotation policies.
6. **Key Management:** Clarify key storage, rotation, and auditing.
7. **Vulnerability Management & Dependency Scanning:** Describe scanning cadence and triage process.
8. **Penetration Testing / Audits:** Capture any scheduled or ad-hoc audits.
9. **Incident Response Process:** Document detection, response, and post-mortem practices.
10. **Compliance & Data Retention Policies:** Outline applicable standards and how retention is managed.
11. **Other**.

## 7. Culture & External Factors

1. **Working Conditions:** Comment on office/remote setups, tooling, and ergonomics.
2. **Remote Work / Hybrid Efficiency:** Assess how well the team collaborates across locations.
3. **HR & Recruiting Alignment:** Describe communication with people operations on hiring and retention.
4. **Continuous Learning & Growth:** Note coaching, training budgets, guilds, or knowledge-sharing events.
5. **Other**.
