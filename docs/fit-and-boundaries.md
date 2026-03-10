# Fit and Boundaries

Dandori is a team coordination framework. It works best when preparation determines quality. This page clarifies where it fits, where to adapt, and where not to force it.

## Best Fit

Use Dandori as the default when:
- Work is specifiable: intent can become testable acceptance criteria.
- Execution is fast relative to specification (e.g., AI-assisted or well-known domains).
- Interfaces are explicit (APIs, contracts, data shapes, user flows).
- Decisions affect downstream teams and need visibility (Decision Requests help).
- You can validate outcomes against measurable success criteria.

Examples:
- Product features with clear inputs/outputs or user flows.
- Backend/platform changes with defined contracts and SLOs.
- Migrations with known constraints and rollback plans.

## Good Fit with Adaptation

Use Dandori with lighter touch when work is uncertain or exploratory:
- Classification is Uncertain: discovery precedes specification.
- Use brief Intents to frame the problem and constraints.
- Run a focused exploration spike or RFC to retire key unknowns.
- Switch to specification once acceptance criteria can be written.
- Keep ceremonies minimal (short, async where possible).

Examples:
- New problem/solution discovery, unfamiliar integrations, emerging domains.

## Poor Fit (Do Not Force)

Avoid forcing Dandori on work that is not spec-driven:
- Pure research or open-ended experiments without near-term delivery.
- Hackathons, spikes intended only to learn, not to ship.
- Emergency incident response (use Post-Mortems afterwards to learn).
- Extremely small/trivial changes where the overhead outweighs the benefit.

## Signs You’re Applying It Too Early

- Most items remain Uncertain; specs attempt to document unknowns rather than reduce them.
- Acceptance criteria cannot be stated without hand-waving.
- Decision Requests pile up with no clear decider or deadline.
- Integration Reviews have little to inspect beyond opinions.
- Spec writing time dwarfs discovery time; assumptions get invalidated quickly.

If these appear, return to discovery (Intent, RFC, exploration) before specifying.

## When to Switch from Discovery to Specification

Switch once the work is specifiable:
- Problem and constraints are agreed and stable enough.
- Success criteria are measurable and observable.
- Testable acceptance criteria can be written for the core behavior.
- Interfaces/contracts are named (inputs, outputs, failure modes).
- Key decisions are few and tractable (or clearly flagged as Decision Requests).
- Classification can move from Uncertain to Clear or Complex.

## When to Reduce Formality

Reduce ceremony and document weight when data shows stability:
- First-pass success rate is consistently high; rework is low.
- Domain is well understood; patterns repeat.
- Items are Clear and low risk.

Practical reductions:
- Combine or shorten ceremonies; use async handoffs where safe.
- Keep specs lean (only what’s needed for unambiguous execution/validation).
- Update the patterns library and checklists instead of adding sections.

---
Principle: Earn the right to lighten. Reduce formality based on evidence (metrics), not preference.
