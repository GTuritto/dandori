# Pilot Guide (4–6 Weeks)

Run a limited, empirical pilot to evaluate whether Dandori improves clarity, flow, and outcomes in your context. Keep the scope small and let data guide next steps.

## Why Pilot Before Broader Adoption
- Reduce risk by validating with one workstream before scaling.
- Tailor practices to your constraints instead of adopting doctrine.
- Produce data that informs whether to expand, adapt, or stop.

## What to Baseline Before Starting
Capture 4–8 weeks of recent work (or sample 8–12 items) using current ways of working.
- Cycle time: Intent → Integration (or request → release).
- First‑pass success rate: specs/features passing validation without revision.
- Decision latency: time from Decision Request to resolution.
- Validation rework rate: % of items that cycle back from Validation to Specification.
- Defect escape / operational follow‑up: incidents or fixes discovered post‑release.
If data is missing, do a quick sampling review of recent work; approximate consistently.

## Recommended Pilot Scope
- One workstream only (a product area or a single service).
- 2–4 active specs at a time; WIP stays small.
- Clear mix: prioritize Clear items; include up to one Complex item.
- Named roles (can be shared): Spec Owner, Reviewer, Prioritizer.

## Recommended Pilot Duration
- 4 weeks minimum; 6 weeks if your cycle times are longer or work is seasonal.
- Week 0 is prep: create the Intent queue and visible pipeline; agree on Minimum Viable Dandori.

## Suggested Metrics to Observe
Use existing definitions from the framework.
- Cycle Time (Intent → Integration)
- First‑Pass Success Rate
- Decision Latency (tactical ~4h, strategic ≤24h)
- Validation Rework Rate
- Stage Dwell Time per lifecycle stage (optional)
- Pipeline WIP by stage (optional)
Track weekly. Prefer trends over single points.

## Questions to Ask During the Pilot
- Clarity: Are intents and acceptance criteria clearer sooner?
- Decision quality: Are decisions explicit, timely, and visible?
- Validation readiness: Do specs enable fast, objective validation?
- Ownership: Are Spec Owner/Reviewer/Prioritizer boundaries working?
- Coordination: Are handoffs lighter and Integration Reviews producing actions?

## What Success Looks Like (Directionally)
- First‑pass success trending upward or stable with fewer reversals.
- Decision latency decreasing; fewer “waiting on decision” blocks.
- Cycle time stabilizing; Stage Dwell Time more balanced across stages.
- Integration Review surfaces concrete actions; architectural drift decreases.
- Fewer post‑release surprises; clearer ownership of outcomes.
Avoid absolute targets during the pilot; focus on direction and visibility.

## What False Positives Look Like
- Metrics improve while customers feel more pain (e.g., architectural drift increases).
- Shorter specs that hide missing acceptance criteria.
- Fewer meetings because nothing ships, not because coordination improved.
- “Fast” but with growing rework or incident tail.

## What Mixed Results Usually Mean (And How to Adjust)
- Clarity up, latency unchanged: strengthen Decision Requests and decider accountability; review at Integration Review.
- Faster execution, more rework: improve acceptance criteria and edge cases; add a short Spec Retrospective.
- Cycle time up, quality up: accept initial investment; keep specs lean and reduce ceremony where data allows.
- Stage bottleneck moves: adjust WIP or staffing; add/trim ceremony focusing on the bottlenecked stage.

## How to Decide: Expand, Adapt, or Stop
- Expand when: at least one meaningful spec integrates, signals trend in the right direction, and the team sees value.
- Adapt when: one dimension lags (e.g., decision latency). Change the smallest thing: add Decision Request rigor, tune ceremony frequency, refine templates.
- Stop when: admin grows without clarity; PM support is absent; decisions remain slow despite explicit requests. Capture lessons and revisit later; don’t force it.

---
References: Getting Started, Fit and Boundaries, Failure Modes, and Metrics. Use the templates directory for lean artifacts.
