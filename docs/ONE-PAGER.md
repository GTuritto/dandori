# Dandori at a Glance

> [Download the One-Pager as PDF](assets/dandori-onepager.pdf){ .md-button }

**段取り Dandori** — A Team Coordination Framework for AI-Augmented Engineering

> *Preparation is the work.*

---

## Core Principles

| Principle | In Practice |
|-----------|------------|
| **The Specification Is the Unit of Work** | Not user stories. A precise document that is simultaneously the design, the execution instruction, the review criteria, and the communication medium. |
| **Human Judgment Is the Scarce Resource** | Optimize for thinking, deciding, and validating. Not for labor allocation. |
| **Preparation Determines Quality** | The spec determines the output. Invest in better specs, not faster execution. |
| **Flexible Constraints** | Non-negotiable elements protect quality. Adaptive elements flex to context. If adoption can mean anything, adoption means nothing. |

---

## Specification Lifecycle

```
INTENT → SPECIFICATION → EXECUTION → VALIDATION → INTEGRATION
  ↑            ↑                          |              |
  |            └──── Spec revision ───────┘              |
  └──────── Back to intent if misunderstood ─────────────┘
```

---

## Roles

| Role | Owns | Key Rule |
|------|------|----------|
| **Spec Owner** | Translating intent into precise specifications | Must be different person from Reviewer |
| **Reviewer** | Validating output against spec and system coherence | Evaluates what was built, not how |
| **Prioritizer** | Pipeline flow, what gets specified next | Shared between EM and PM |

---

## Ceremonies

| Non-Negotiable | Required (Adaptive) | Conditional | Earned Optional |
|---------------|---------------------|-------------|-----------------|
| Pipeline Sync (daily, 15m) | Spec Retrospective (weekly) | Pre-Mortem (complex specs) | Team Retrospective (monthly) |
| Spec Handoff (per spec) | Prioritization Reset (weekly) | Decision Request (async) | Demo Day (biweekly) |
| Integration Review (weekly) | | Intent Review (biweekly) | War Games (quarterly) |

---

## Specifiability Classification

| Clear | Complex | Uncertain |
|-------|---------|-----------|
| Well-understood, high confidence | Design decisions needed, moderate risk | Research required, high revision likelihood |
| → Straight to spec | → Pre-Mortem before execution | → Exploration spike first |

---

## Key Metrics

**Cycle Time** · **First-Pass Success Rate** · **Decision Latency** · **Validation Rework Rate** · **Pipeline WIP**

---

## What Dandori Is Not

Not a spec-driven development tool (not Spec-Kit, not Kiro, not BMAD). Not tied to any AI tool. Works with or without AI. It is a team coordination framework that addresses broken Scrum and the modern reality of software delivery.

---

**Team Size:** 1 (solo variant) · 3 minimum (full framework) · 4-8 sweet spot · 9-12 with adjustments · Beyond 12 needs multi-team model

**License:** CC BY-SA 4.0 · **Repository:** github.com/GTuritto/dandori
