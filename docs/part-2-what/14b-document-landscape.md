# How Traditional Documents Fit Into Dandori

Software teams produce and consume many documents beyond code: PRDs, ADRs, RFCs, design documents, test plans, runbooks, and others. These documents exist for good reasons. They capture decisions, communicate intent, coordinate across teams, and create institutional memory. Dandori does not eliminate them. It repositions them within the specification lifecycle so they serve clear purposes at clear stages rather than floating as disconnected artifacts that may or may not reflect the current reality.

The core question for each document type is: where does it live in the lifecycle, who produces it, and how does it relate to the specification?

## PRD (Product Requirements Document)

**In Scrum:** The PRD often exists in a gray zone. Some teams write PRDs before sprint work begins. Others skip them entirely in favor of user stories. When PRDs exist, they frequently drift out of sync with the actual stories because they are maintained by product while stories evolve during the sprint. The PRD becomes a historical artifact rather than a living document.

**In Dandori:** The PRD maps directly to the **Intent** stage. It is the structured articulation of what needs to change and why. However, Dandori's Intent document is leaner than a traditional PRD. It focuses on the problem statement, measurable success criteria, explicit constraints, and priority signals. It does not attempt to specify the solution, because solution design happens in the Specification stage.

For large initiatives that span multiple specifications, the PRD serves as a parent document that frames the overall problem, and individual Intent documents reference it. The PRD answers "what is the initiative and why does it matter?" Each Intent answers "what is this specific piece of the initiative?" Each Specification answers "what exactly are we building for this piece?"

The PM owns the PRD. The Spec Owner references it when writing specifications. The Prioritizer uses it to sequence related intents. When the PRD changes, the change is visible because downstream intents and specs either align with it or they do not, and the Integration Review is where that alignment gets checked.

## ADR (Architecture Decision Record)

**In Scrum:** ADRs are typically maintained separately from sprint work. An architect or senior engineer writes them, they live in a docs folder or a wiki, and they may or may not be referenced when implementing features. The connection between an ADR and the code it influences is implicit and often lost over time.

**In Dandori:** ADRs are embedded directly in specifications. Every specification has an "Architectural Decision" section that captures the decisions made for that specific piece of work: what was decided, what alternatives were considered, and why this option was chosen. This is not a separate document. It is part of the spec.

This means ADRs are created at the point of decision (during the Specification stage), reviewed at the point of validation (the Reviewer checks whether the implementation respects the decision), and archived at the point of integration (the spec becomes the permanent record). The decision never drifts from the code it influences because it lives in the same artifact.

For architectural decisions that span multiple specifications, such as "we use event-driven architecture for all cross-service communication," a standalone ADR still makes sense. But it functions as a constraint that individual specifications reference, not as a disconnected document. When a Spec Owner writes a specification, they check relevant cross-cutting ADRs and either align with them or propose a revision through a Decision Request.

The Spec Retrospective is where the team identifies when architectural decisions in specs proved wrong or insufficient. These insights feed back into both the spec patterns library and any cross-cutting ADRs that need updating.

## RFC (Request for Comments)

**In Scrum:** RFCs exist outside the sprint framework entirely. Someone writes a proposal, it circulates for feedback, comments accumulate, and eventually a decision is made (or not). The RFC process has no formal connection to sprint planning, estimation, or delivery. This means an RFC can be approved and then sit in the backlog for months because the sprint process never prioritizes implementing it.

**In Dandori:** RFCs map to the transition between Intent and Specification, specifically for **Complex** and **Uncertain** work that needs broader input before a specification can be written.

When a Spec Owner encounters a problem that is too complex or uncertain to specify alone, they write an RFC. The RFC circulates during the **Intent Review** ceremony, where the broader team provides feedback, surfaces risks, and identifies dependencies. Once the RFC reaches consensus, it becomes the foundation for one or more specifications.

The critical difference from how most organizations use RFCs: in Dandori, an approved RFC immediately enters the specification queue. It does not float indefinitely. The Prioritizer is responsible for ensuring that approved RFCs are either scheduled for specification or explicitly deprioritized with a reason. This closes the gap between "we agreed this is a good idea" and "someone is actually working on it."

For cross-team RFCs (proposals that affect systems owned by multiple teams), the RFC process happens outside any single team's Dandori pipeline. But the output, the approved proposal, enters each affected team's intent queue as a coordinated set of intents that reference the same RFC.

## Design Documents

**In Scrum:** Design documents vary wildly in format, depth, and when they are produced. Some teams write them before the sprint. Some write them during the sprint. Some skip them entirely. When they exist, they often describe the "how" in detail but may not capture the "why" or the constraints, making them hard to evaluate without additional context.

**In Dandori:** Design documents are absorbed into the specification. The Specification is the design document. It captures requirements, constraints, interface contracts, architectural decisions, and acceptance criteria in a single artifact. There is no separate design doc that might contradict or drift from the spec.

For complex features that require extensive design exploration before specification, the design work happens as an exploration spike during the **Uncertain** classification path. The output of the exploration spike is not a design document. It is a specification (or the conclusion that the work is not yet specifiable and needs further research). The design thinking is captured in the spec's architectural decision section and its requirements, not in a separate artifact.

UX design artifacts (wireframes, prototypes, interaction specifications) feed into the Specification stage as inputs that the Spec Owner incorporates. They are not separate deliverables that float alongside the spec. The spec references or embeds the relevant design decisions so that the implementer (human or AI) and the Reviewer have a single source of truth.

## Test Plans

**In Scrum:** Test plans are sometimes written before the sprint, sometimes during, and sometimes not at all. They are often maintained by QA separately from user stories, creating a synchronization gap between what was specified, what was built, and what was tested.

**In Dandori:** Test plans are embedded in the specification as acceptance criteria. The QA engineer contributes test scenarios, edge cases, and quality dimensions to the spec during the Specification stage, before execution begins. These become the criteria that the Reviewer validates against during Validation.

For system-level testing that spans multiple specifications (integration tests, performance tests, security tests), a separate test plan is appropriate. But it references the specifications it covers and is updated as specs integrate. The Integration Review is where the team checks whether system-level test coverage is keeping pace with the rate of specification integration.

Exploratory testing, which is not predefined and cannot be captured in acceptance criteria, happens during the Validation stage alongside criteria-based validation. The Reviewer and QA engineer can explore the output beyond the spec's criteria, and any issues found either become spec revisions (if the criteria were incomplete) or new intents (if a previously unknown requirement is discovered).

## Runbooks and Operational Documentation

**In Scrum:** Operational documentation is often an afterthought. It gets written after deployment, if at all, and quickly drifts from reality as the system evolves.

**In Dandori:** Operational documentation is an output of the **Integration** stage. When a specification integrates, the spec itself becomes the primary operational record: it captures what was built, why, what the constraints are, and what the acceptance criteria were. For operational concerns that go beyond the spec (monitoring, alerting, incident response), the Spec Owner or a designated team member produces operational documentation as part of the integration checklist.

The specification repository becomes the living documentation of the system. Each spec is a permanent record of a design decision and its implementation. When an incident occurs, the Post-Mortem can trace back to the relevant specification and ask whether the spec was inadequate, whether the implementation deviated from the spec, or whether the operational documentation was missing.

## The Document Landscape in Dandori

| Document | Where It Lives | When It Is Created | Who Owns It |
|----------|---------------|-------------------|-------------|
| **PRD** | Intent stage (parent document for initiatives) | Before intents are written | PM |
| **Intent Document** | Intent stage | When a problem is identified | PM or Spec Owner |
| **RFC** | Between Intent and Specification | When work is Complex or Uncertain and needs broad input | Spec Owner, reviewed by team |
| **Specification** | Specification stage (the central artifact) | Before execution begins | Spec Owner, with input from all disciplines |
| **ADR** | Embedded in specification, or standalone for cross-cutting decisions | During specification writing | Spec Owner or Architect |
| **Design Artifacts** | Inputs to the specification | Before or during specification | UX Designer |
| **Test Plan** | Acceptance criteria in specification, or standalone for system-level testing | During specification (criteria) or after integration (system-level) | QA Engineer |
| **Runbook** | Output of integration stage | During integration | Spec Owner or designated team member |
| **Post-Mortem Report** | Output of Post-Mortem ceremony | After an incident | EM or incident lead |
| **Spec Patterns** | Output of Spec Retrospective | Ongoing, updated weekly | Team (maintained by EM) |

## The Specification as the Connective Tissue

The pattern across all of these documents is that the specification serves as the connective tissue. It references the PRD (for business context), embeds the ADR (for architectural decisions), incorporates design artifacts (for UX requirements), includes test criteria (for quality validation), and produces operational documentation (for system maintenance).

In Scrum, these documents existed as independent artifacts with implicit connections. A user story might reference a PRD, but the connection was a link that could break. An ADR might influence a design, but the relationship was in someone's head, not in the artifact. A test plan might cover a feature, but the mapping between test cases and acceptance criteria was maintained manually.

In Dandori, the specification makes these connections explicit. Every spec knows which intent it serves, which architectural decisions it makes, which design inputs it incorporates, and which acceptance criteria must be met. This does not eliminate the need for standalone documents (PRDs for initiatives, cross-cutting ADRs, system-level test plans), but it ensures that the connections between documents are maintained through the specification rather than through tribal knowledge.

The result is a documentation ecosystem where each artifact has a clear purpose, a clear owner, a clear stage in the lifecycle, and a clear relationship to the specification that drives implementation. Nothing floats. Everything connects.
