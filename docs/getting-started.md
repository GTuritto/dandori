# Getting Started (Incremental Adoption)

This guide helps real teams adopt Dandori without replacing their entire operating model at once. Start small, keep it light, and let data justify changes.

## Who Should Not Adopt Yet
- In active incident/crisis mode where stability work dominates (return after stabilization).
- Pure research/spikes with no near-term delivery (use Post‑Mortem/learning notes, not specs).
- No clear product ownership or willingness to decide (Decision Requests will stall).
- Extremely small, trivial work where any extra coordination is waste.

## Minimum Viable Dandori (MVD)
- Roles (can be shared): Spec Owner, Reviewer, Prioritizer.
- Lifecycle: Intent → Specification → Execution → Validation → Integration.
- Artifacts: Intent (1 page), Specification (lean), Decision Request (when blocked).
- Ceremonies: Pipeline Sync (15m daily), Spec Handoff (10–15m per spec), Integration Review (30–45m weekly).
- Metrics: Cycle time, First‑pass success rate, Decision latency.
- Classification: Clear | Complex | Uncertain (guides rigor and use of discovery).

## Start With One Workstream
- Choose one product area, service, or initiative; keep WIP small.
- Assign a Spec Owner and a Reviewer; name a Prioritizer (PM or EM/lead).
- Create an Intent queue for this workstream only; keep everything else unchanged.
- Run MVD for 30 days; measure throughput and first‑pass success.

## Minimal Artifact Set
- Intent (1 page): problem/opportunity, success criteria, constraints, next step.
- Specification (lean): requirements, decisions, interfaces/contracts, acceptance criteria, validation plan.
- Decision Request (as needed): decision needed, options, recommendation, needed‑by.
Tip: Keep background in References; prefer examples and edge cases over prose.

## Minimal Ceremony Set
- Pipeline Sync (15m): Track specs, not people. What moved, what’s blocked, what’s next.
- Spec Handoff (10–15m/spec): Owner walks Reviewer through acceptance criteria and edge cases.
- Integration Review (30–45m weekly): What shipped, patterns, architectural coherence, actions.
Optionally add Spec Retrospective if first‑pass success < ~70% or rework is rising.

## How to Run a 30‑Day Pilot
- Week 0 (Prep): Pick workstream; draft 2–3 Intents; agree on MVD; set up a visible pipeline.
- Week 1: Write 1–2 lean specs; run Pipeline Sync daily; do Spec Handoffs before execution.
- Week 2: Integrate first specs; hold Integration Review; log 2–3 actions.
- Week 3: Add discovery for Uncertain items (short RFC/spike); keep Clear items flowing.
- Week 4: Review metrics (cycle time, first‑pass, decision latency); run a Spec Retro; decide to scale, adjust, or pause.
Success criteria: at least one meaningful spec integrated; decision latency within SLA; fewer reversals.

## Adopting Inside Existing Environments
- Scrum: Keep sprints. Replace standup content with Pipeline Sync (specs/flow). Keep demos if useful; use Integration Review for system coherence. Backlog items become Intents/Specs.
- Kanban: Add lifecycle columns (Intent → Spec → Exec → Validation → Integration). Keep WIP limits. Add Decision Requests and Spec Handoffs.
- Ad hoc: Start a simple Intent queue. Run Pipeline Sync and Spec Handoff. Write only the specs you need for current work.

## If PM Support Is Weak
- Engineering drafts Intents; use Decision Requests to surface choices explicitly to PM/leadership.
- Prioritizer can be EM/tech lead temporarily; make tradeoffs visible at Pipeline Sync.
- Keep success criteria business‑observable (customer impact, SLO/SLA), not just technical.

## Backend, Platform, Cross‑Functional Teams
- Emphasize interfaces/contracts, SLOs/SLIs, and rollback. Include telemetry in specs.
- Use Pre‑Mortems for Complex changes or new protocols.
- Invite adjacent teams to Integration Review when cross‑cutting risks exist.

## Signs the Pilot Is Helping
- Cycle time becomes predictable; first‑pass success trending upward.
- Decision latency decreases; fewer “waiting on product” blocks.
- Fewer surprises at integration; less rework and fewer reversals.

## Signs It’s Creating Admin, Not Clarity
- Document volume grows but acceptance criteria stay vague.
- Meetings multiply without new decisions or actions.
- People comply with templates but avoid judgment.
Correction: Cut sections; focus on criteria and decisions. Merge/shorten ceremonies. Re‑read Fit and Boundaries and Failure Modes, then adjust.

---
Principle: Earn the right to expand. Start small, measure, and only scale what proves useful.
