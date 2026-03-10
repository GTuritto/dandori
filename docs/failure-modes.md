# Failure Modes and Corrections

Dandori is opinionated about preparation, roles, and flow. This guide names common ways it breaks in real organizations and how to detect and correct misuse early. Keep responses light but decisive.

## Spec Owner becomes the bottleneck

- What it looks like
  - Specs pile up waiting for a single Spec Owner to write or update them.
  - High Stage Dwell Time in Specification; idle capacity in Execution/Validation.
- Why it happens
  - Role over-ownership; others feel they “cannot write specs.”
  - Overly heavy spec expectations; perfectionism over clarity.
- Early warning signs
  - WIP in Specification keeps growing; Pipeline Sync surfaces the same blocked items.
  - First-Pass Success is decent, but throughput drops.
- Corrective action
  - Pair spec writing; enable more engineers/PMs to draft with Reviewer support.
  - Add a checklist and examples; remove non-essential sections from specs.
  - Use Specifiability Classification to split work: Clear items flow; Complex items get RFCs or Pre‑Mortems.

## Reviewer becomes a gatekeeper or shadow manager

- What it looks like
  - Reviews stall; decisions rerouted through the Reviewer; style policing replaces acceptance criteria.
- Why it happens
  - Ambiguous acceptance criteria; unclear decision boundaries; status power dynamics.
- Early warning signs
  - Validation Rework Rate rises from preference changes; Decision Requests bypass the Prioritizer.
- Corrective action
  - Re-anchor on acceptance criteria and intent; enforce “spec over taste.”
  - Rotate Reviewers; timebox validation; escalate cross-cutting decisions to Integration Review.
  - EM reinforces role boundaries: Reviewer validates against the spec, not manages the spec owner.

## Product decision latency blocks flow

- What it looks like
  - Specs sit waiting on product/strategy decisions; Execution starves.
- Why it happens
  - No explicit Decision Requests; no SLA; unclear decider.
- Early warning signs
  - Decision Latency exceeds 4h/24h norms; Pipeline Sync repeatedly flags “waiting on decision.”
- Corrective action
  - Use Decision Requests with owner and needed‑by; track in the pipeline.
  - Prioritizer enforces tradeoffs visibly; unblock Clear work while Complex items wait.
  - Review latency weekly in Integration Review; assign owners for chronic delays.

## Teams write long specs instead of clear specs

- What it looks like
  - Verbose documents; unclear acceptance criteria; execution teams guess.
- Why it happens
  - Confusing rigor with length; fear of missing something; template bloat.
- Early warning signs
  - First-Pass Success falls; Validation finds “missing” criteria; authors avoid handoffs.
- Corrective action
  - Cut to essentials: requirements, decisions, interfaces/contracts, acceptance criteria.
  - Use examples and edge cases over prose; move background to References.
  - Spec Retrospective updates the patterns library; remove non-value sections from templates.

## Ceremonies multiply without adding clarity

- What it looks like
  - Extra meetings appear; same topics repeat; little changes between sessions.
- Why it happens
  - Avoiding hard decisions; unclear purpose per ceremony; cargo-culting.
- Early warning signs
  - Meetings grow in length/attendance; few actions; duplicate agendas.
- Corrective action
  - Re-apply ceremony classification: start with all, reduce by evidence.
  - Merge or shorten; prefer async for updates; reserve live time for decisions.
  - Track actions and outcomes in Integration Review; cancel if value not evident.

## Metrics become performative

- What it looks like
  - Teams optimize numbers (e.g., shorter specs) instead of outcomes; gaming appears.
- Why it happens
  - Metrics lose connection to decisions; missing translation to business impact.
- Early warning signs
  - Metrics improve while Integration Review flags architectural drift or customer pain.
- Corrective action
  - Tie each metric to a decision: what will change if it moves?
  - Highlight contradictions at Integration Review; favor qualitative patterns over vanity improvements.
  - Keep a small, stable set: Cycle Time, First‑Pass Success, Decision Latency, Rework.

## Discovery work is forced into specification too early

- What it looks like
  - Specs encode unknowns; frequent reversals; thrash between stages.
- Why it happens
  - Pressure for dates; discomfort with uncertainty; lack of Uncertain path.
- Early warning signs
  - Many “spec updates” after execution starts; rework due to wrong assumptions.
- Corrective action
  - Mark work Uncertain; run a short exploration or RFC; define acceptance criteria for the learning, not the solution.
  - Switch to specification once interfaces and success criteria are nameable.

## Teams comply with artifacts but avoid judgment

- What it looks like
  - Boxes checked (intent, spec, review) but weak decisions; low ownership.
- Why it happens
  - Fear of accountability; templates seen as ends rather than means.
- Early warning signs
  - Repeated “no decision” outcomes; unresolved risks; Integration Review with few real changes.
- Corrective action
  - Emphasize intent, decisions, and acceptance criteria over document completeness.
  - Use Troika Consulting in Spec Retrospective to surface judgment gaps.
  - EM and leads model explicit tradeoffs; document decisions and consequences succinctly.

---
Use this guide during Pipeline Sync, Integration Review, and Spec Retrospective. Detect early, correct lightly, and keep preparation the work.
