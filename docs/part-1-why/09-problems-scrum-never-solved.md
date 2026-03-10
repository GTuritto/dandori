# The Problems Scrum Never Solved

Dandori was born from two converging observations: Scrum has lost its meaning, and AI is changing how software gets built. But there is a third observation that deserves its own chapter, because it affects every team regardless of AI adoption: Scrum never solved several fundamental problems that plague software delivery, and most teams have simply learned to live with them.

## The Visibility Problem

One of the most common complaints from business stakeholders about Scrum is the lack of visibility. A sprint starts. Two weeks pass. At the sprint review, the team demonstrates what they built. Sometimes it is what the stakeholder expected. Sometimes it is not. Sometimes a story was "almost done" and carried over. Sometimes the team delivered everything but the stakeholder realizes they asked for the wrong thing.

The sprint is a black box. Even stakeholders who attend every ceremony, sit in every standup, and read every update cannot confidently answer the question: "What will I have on this date?" Sprint commitments are aspirational. Velocity is a trailing average, not a guarantee. Story points do not translate to calendar time. The business learns what it got when the sprint ends, not before.

This is not a failure of discipline. It is a structural property of how Scrum works. The sprint is designed to protect the team from mid-sprint changes, which means the business cannot see or influence what is happening inside the sprint without violating the framework's own rules. The trade-off was intentional: Scrum chose team stability over business visibility. But for many organizations, especially those with external commitments, regulatory deadlines, or coordinated launches, that trade-off is unacceptable.

### How Dandori Addresses This

In Dandori, work is visible at every stage because the pipeline is the primary coordination mechanism, not the sprint boundary.

The business can see, at any moment, how many intents are in the queue and what their priority order is. They can see which specifications are being written and what decisions are pending. They can see which specs are in execution and which are in validation. They can see what integrated this week and what the metrics say about pipeline health.

This is not a dashboard bolted onto an opaque process. It is the process. The Pipeline Sync (daily) and the Integration Review (weekly) are both structured around pipeline visibility. The Prioritizer role exists specifically to keep the business and engineering aligned on what is flowing through the system.

The predictability question changes too. Instead of "what will I get at the end of this sprint?" the question becomes "what is the cycle time for a spec of this complexity, and how many specs are ahead of this one in the queue?" That is a more honest answer. It does not pretend to predict the future with false precision. It gives the business a real-time view of where their priorities stand and how fast things are moving.

For teams that need date commitments, Dandori's flow metrics provide a more reliable basis than sprint velocity. Cycle time data (how long specs typically take from intent to integration, broken down by specifiability classification) gives the business a data-driven range: "Clear specs typically integrate in 2-3 days. Complex specs take 5-7 days. This feature has three Complex specs, so expect 2-3 weeks." That is less satisfying than "it will be done by Friday" but far more honest, and it does not require waiting until a sprint review to discover the truth.

## The Non-Developer Problem

The Scrum Guide defines one team role for everyone who does the work: "Developers." Whether you write code, design interfaces, test software, manage infrastructure, or architect systems, you are a "Developer" in Scrum's vocabulary. The framework has no model for specialized roles that contribute to software delivery in fundamentally different ways and on fundamentally different timelines.

In reality, software teams include people with distinct disciplines: UX designers who need to research and prototype before engineers build, architects who need to define patterns and constraints that span multiple features, QA engineers who need to validate quality across dimensions that go beyond acceptance criteria, UAT specialists who need to verify that the software meets business requirements in realistic scenarios, technical writers who need to document what was built, and many others depending on the organization.

Scrum's answer to this is: put everyone on the same team, work in the same sprint, attend the same ceremonies. In practice, this creates one of two dysfunctions.

Either the specialized roles are forced into the sprint cadence and their work gets compressed or skipped (designers rush their research to fit the sprint timeline, QA gets squeezed into the last two days, UAT happens after the sprint when nobody is paying attention), or the specialized roles work on a parallel timeline that is loosely coupled to the sprint, creating the synchronization problems described in the next section.

### How Dandori Addresses This

Dandori's lifecycle has natural integration points for every discipline, because the specification is where all perspectives converge before execution begins.

The **Intent** stage is where business analysts, product managers, and domain experts contribute. They define the problem, the success criteria, and the business constraints. This is not a user story written by the PM alone. It is a collaborative articulation of what needs to change and why.

The **Specification** stage is where every relevant discipline contributes to a single, shared artifact:

- **UX designers** contribute interaction patterns, visual specifications, accessibility requirements, and responsive behavior rules to the spec before execution begins. Their designs are not separate deliverables that engineers need to interpret. They are part of the specification that engineers (or AI) implement against.
- **Architects** contribute architectural decisions, interface contracts, performance constraints, and integration patterns. These are not separate architecture documents that may or may not align with the feature spec. They are embedded in the specification.
- **QA engineers** contribute test scenarios, edge cases, and quality dimensions that go beyond the functional acceptance criteria. Their input shapes the spec before implementation, not after.
- **UAT specialists** contribute business validation criteria that define what "correct" means from the business perspective. These criteria are part of the spec's acceptance criteria, not a separate phase that happens weeks later.
- **Technical writers** can begin documentation from the specification itself, since the spec captures the intent, behavior, and constraints of the feature.

The key insight is that in Scrum, these disciplines contribute at different times and through different artifacts, creating synchronization gaps. In Dandori, they all contribute to the same artifact (the specification) at the same stage (before execution), which eliminates the gaps.

This does not mean every discipline attends every ceremony. The **Intent Review** (biweekly) is where the broader team, including designers, architects, and QA, builds shared context on upcoming work. The **Spec Handoff** includes whoever needs to understand the spec for their role. The **Integration Review** includes whoever needs to validate the output. But the synchronization point is always the specification, not the sprint boundary.

The **Pre-Mortem** ceremony is particularly valuable for cross-discipline teams. When a designer, an architect, a QA engineer, and a Spec Owner sit together for 20 minutes and ask "what could go wrong with this spec?" they surface cross-discipline risks that no single perspective would catch. The architect notices that the design requires a data flow the current API does not support. The QA engineer notices that the accessibility requirement conflicts with the proposed interaction pattern. The designer notices that the performance constraint makes a certain animation impossible. All of this is caught before execution, not after.

## The Parallel Workstream Problem

This is perhaps the most expensive problem Scrum never solved, and the one most likely to resonate with anyone who has managed a team with embedded designers, architects, or QA.

The pattern is painfully familiar. Designers work ahead of the sprint, creating designs for features that engineers will build in a future sprint. By the time engineers start building, the designs may have changed. Or the engineers discover that the design is technically infeasible with the current architecture. Or the designers have moved on to the next set of designs and are not available to answer questions.

The same pattern plays out with QA. Engineers build during the sprint. QA tests after. By the time QA finds issues, the engineers have moved on to the next sprint's work. Fixing the issues requires context-switching, which is expensive, or deferring the fixes, which creates technical debt.

And with UAT, the pattern is even worse. Business stakeholders validate the feature weeks after it was built. They discover that what was built does not match what they needed, not because the engineers made mistakes, but because the requirements were ambiguous and the engineers made different assumptions than the stakeholders expected.

In all three cases, the root cause is the same: **work that should be synchronized is happening on parallel timelines, and the sprint boundary does not synchronize them.** The sprint synchronizes the engineering work. Everything else floats alongside it, loosely coupled and frequently misaligned.

The cost of this misalignment is enormous. Late design changes require rework. Late QA discoveries require context-switching or carry-over. Late UAT feedback requires entire features to be revisited. These costs are rarely tracked because they are distributed across sprints and normalized as "just how things work." But they represent a significant percentage of total engineering effort in most organizations.

### How Dandori Addresses This

Dandori solves the parallel workstream problem by collapsing the parallel timelines into a single sequential flow through the specification lifecycle.

In Scrum, the timeline looks like this:

```
Design:  [Research]──[Prototype]──[Handoff]──────────────[Revision after feedback]
Sprint:  ──────────────────────────[Build]──[Review]
QA:      ─────────────────────────────────────────[Test]──[Bug reports]
UAT:     ────────────────────────────────────────────────────────[Validate]
```

Each workstream operates semi-independently. Synchronization happens at handoff points that are informal, often late, and frequently missed. Design changes after handoff cause rework. QA after build creates a feedback delay. UAT after everything creates the most expensive feedback delay of all.

In Dandori, the timeline looks like this:

```
Intent:         [PM + Business + Architect define the problem]
Specification:  [Spec Owner + Designer + Architect + QA write the spec together]
Execution:      [AI or developer implements against the complete spec]
Validation:     [Reviewer + QA + UAT validate against spec criteria]
Integration:    [Merge, document, archive]
```

The critical difference: **design, architecture, QA criteria, and business validation criteria all converge in the Specification stage, before execution begins.** There is no parallel design workstream that can drift out of sync. There is no post-execution QA phase that discovers issues too late. UAT criteria are part of the spec, so the output is validated against business expectations during Validation, not weeks later.

This does not mean designers stop doing research or QA stops doing exploratory testing. It means their outputs feed into the specification before execution, rather than running alongside or after it. The designer's research becomes part of the Intent. The designer's prototype becomes part of the Specification. The QA engineer's test scenarios become acceptance criteria in the Specification. The UAT requirements become validation criteria.

When a designer wants to change a specification after execution has started, the change is visible. It is a spec revision, not an informal update that catches engineers by surprise. The team can assess the cost of the change (does the current execution need to stop? can the change be a follow-up spec?) rather than discovering the misalignment after delivery.

### The Spec as the Synchronization Point

The fundamental insight is that Scrum used time (the sprint) as the synchronization mechanism, and it only works for people who operate on the same timeline. Designers, QA, UAT, and architects do not operate on the engineering timeline. Forcing them into it creates the parallel workstream problem.

Dandori uses the specification as the synchronization mechanism. Everyone contributes to the spec. Everyone validates against the spec. The spec is the single artifact that holds the complete picture of what needs to be built, including design, architecture, quality, and business criteria. When the spec is complete, everyone has already agreed on what "done" looks like. There are no surprises at the end.

This does not eliminate all disagreements or rework. Specifications can still be wrong. Execution can still reveal problems the spec did not anticipate. But it eliminates the most expensive category of rework: the kind that happens because different disciplines were working from different understandings of what was being built, on different timelines, with different artifacts.

## Why Scrum Could Not Solve These Problems

These are not implementation failures. Scrum could not solve these problems because they are structural consequences of its core design decisions.

Scrum chose the sprint as its atomic unit, which created the visibility problem (the sprint is a black box by design). Scrum chose "Developers" as its team role, which created the non-developer problem (no model for cross-discipline collaboration). Scrum chose the sprint boundary as its synchronization mechanism, which created the parallel workstream problem (anything that does not fit the sprint cadence is left unsynchronized).

These were reasonable decisions in the context of the late 1990s, when the primary goal was to protect development teams from chaotic requirements changes and give them space to work. But they are the wrong decisions for 2026, when software delivery involves multiple disciplines, business stakeholders demand visibility, and the cost of late synchronization is too high to absorb.

Dandori makes different decisions. It uses the specification as its atomic unit, the pipeline as its visibility mechanism, and the spec itself as the synchronization point across disciplines. These decisions address the problems Scrum could not, while preserving the Agile values that made Scrum worth adopting in the first place.
