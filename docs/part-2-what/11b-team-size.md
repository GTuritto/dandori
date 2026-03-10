# Team Size: Where Dandori Works and Where It Breaks

Every framework has a range. Scrum says 5-9 people per team. Kanban is more flexible but assumes a single team managing a shared board. Dandori has its own range, and being honest about where it works, where it stretches, and where it breaks is more useful than claiming it works for everyone.

## The Minimum: 3 People

Dandori has three roles: Spec Owner, Reviewer, and Prioritizer. The critical constraint is that the Spec Owner and the Reviewer must be different people. If the person who writes the spec also reviews the AI output, the entire quality model collapses. They will unconsciously validate what they intended rather than what was produced. This is the same reason code review exists: the author's brain fills gaps that the artifact does not.

The Prioritizer can be one of the two engineers wearing a second hat, or it can be the PM or product person. So the absolute minimum is two engineers plus someone handling prioritization. That is three people.

At three people, some ceremonies compress or merge. The Pipeline Sync becomes a quick conversation. The Spec Handoff is between the two engineers. The Spec Retrospective and Integration Review can merge into a single weekly session. The Intent Review may not be needed if the team shares enough context through daily work. But the core discipline holds: one person specs, another reviews, and the separation is what maintains quality.

Below three, an individual can use spec-driven development practices. They can write specifications, use AI to execute, and validate the output. But they cannot run full Dandori, because the framework's quality model depends on the separation between specification and review. A solo practitioner using specs is doing spec-driven development. A team of three using specs with defined roles, ceremonies, and metrics is doing Dandori. For the solo engineer, see [Dandori Solo](11c-dandori-solo.md), a variant that preserves the principles and lifecycle while honestly acknowledging what is lost without a second pair of eyes.

## The Sweet Spot: 4-8 People

This is where Dandori works best. The team is large enough that roles are distinct (multiple Spec Owners, at least one or two dedicated Reviewers, a clear Prioritizer), and small enough that the ceremonies scale naturally.

At this size, the Pipeline Sync genuinely takes 15 minutes because the number of specs in flight is manageable (typically 5-15 across all lifecycle stages). Everyone can see the full pipeline. Bottlenecks are visible. The Spec Retrospective works well with Troika Consulting because there are enough people for meaningful rotation. The Integration Review covers the week's output without rushing. The Intent Review builds genuine shared context because everyone can absorb the upcoming work.

Cross-discipline teams fit well at this size. A team of 4-8 might include three or four engineers (some acting as Spec Owners, some as Reviewers), a UX designer who contributes to specifications, a QA engineer who shapes acceptance criteria, and a PM who shares the Prioritizer role with the engineering lead. Everyone participates in the ceremonies that are relevant to their discipline.

The Prioritizer role works naturally at this size because one person can hold the full context of the pipeline in their head. They know what every spec is, where it stands, and what the dependencies are. This breaks down as team size grows.

## Stretched but Functional: 9-12 People

At this size, Dandori still works but requires adjustments.

The Pipeline Sync needs tighter facilitation. With 10+ specs in flight and 10 people in the room, 15 minutes is tight. The EM must be disciplined about keeping the sync focused on systemic issues (bottlenecks, blocked decisions, patterns) rather than walking through every spec. Using the 1-2-4-All Liberating Structure becomes essential rather than optional: silent pipeline scan, pair discussion, then full group for the top issues only.

The Spec Retrospective may need to split into rotating subgroups. Instead of everyone attending every week, two or three people rotate through Troika Consulting sessions while the rest continue working. The full team comes together monthly for pattern review.

The Prioritizer role strains. One person cannot hold the full context of 15-20 specs in flight across 10 people. At this size, the Prioritizer needs a lightweight tracking system (a shared board with spec status is sufficient) and may need to delegate tactical prioritization for well-understood work areas while retaining strategic prioritization.

The Intent Review becomes more important, not less, because shared context does not happen organically in a group of 10+. Without it, people encounter specs they have no context for, and review quality drops.

## Where Dandori Breaks: Beyond 12

Beyond 12 people, the framework's single-team model breaks down for specific, identifiable reasons.

The pipeline becomes too large for any single person to hold in their head. With 20-30 specs in various lifecycle stages, the Pipeline Sync either becomes a 30-minute meeting (defeating its purpose) or skips specs (defeating its purpose differently). The Prioritizer cannot maintain meaningful context across all of them.

Ceremonies become broadcasts rather than working sessions. The Integration Review with 15 people is a presentation, not an inspection. The Spec Retrospective with 15 people is a lecture, not a consulting session. The Liberating Structures that make ceremonies effective are designed for groups of 4-12 and lose their power at larger sizes.

Architectural coherence, which the Integration Review is supposed to maintain, becomes impossible to check in a single weekly session when the volume of changes is too high. Individual reviews may be thorough, but the systemic view degrades.

### What to Do Beyond 12

Dandori does not currently define a multi-team scaling model, and doing so prematurely would be a mistake. The framework needs more real-world experience before prescribing how multiple Dandori teams coordinate. However, the likely shape of a scaling approach involves the following principles.

Split into smaller teams, each running their own Dandori pipeline with their own roles and ceremonies. Each team should be in the 4-8 range. The split should follow domain or system boundaries, not arbitrary headcount divisions.

Add a cross-team synchronization ceremony, likely weekly, where the Prioritizers from each team align on dependencies, shared specs, and architectural decisions that span team boundaries. This is similar in function to Scrum-of-Scrums but focused on the spec pipeline rather than sprint status.

The Integration Review may need a cross-team component for changes that affect shared systems. This could be a monthly session where senior Reviewers from each team examine cross-team architectural coherence.

Shared spec patterns become essential. When multiple teams write specs for the same system, pattern consistency prevents divergence. A shared spec pattern library, maintained collaboratively, serves this purpose.

The framework explicitly does not prescribe a scaling model like SAFe or LeSS because these models carry significant overhead and assumptions that may not apply to spec-driven, AI-augmented teams. The scaling approach should emerge from the experience of teams that outgrow the single-team model, and their experience reports are among the most valuable contributions the community can make.

## Team Size and AI Adoption

One pattern worth noting: AI amplification changes the relationship between team size and output. A team of 5 using AI effectively may produce the output that previously required a team of 12. This means many teams that currently feel too large for a single-team framework may not need to scale Dandori at all. They may instead find that their effective team size drops as AI handles more implementation, bringing them into the 4-8 sweet spot where Dandori works best.

This is not a recommendation to reduce headcount. It is an observation that teams may choose to take the AI amplification as increased capability rather than reduced staffing, and that the coordination model for a team of 8 doing the work of 15 is still a single Dandori pipeline.
