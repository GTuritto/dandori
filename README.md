# 段取り Dandori

## A Team Coordination Framework for AI-Augmented Engineering

**Dandori** (段取り) is a Japanese word meaning "preparation" or "setup." In the Toyota Production System, dandori refers to the meticulous preparation work done before production begins. The principle is simple: the quality of output is determined by the quality of preparation, not by what happens on the production line.

In AI-augmented software development, Dandori carries the same meaning. When AI handles a growing share of code production, the human contribution that determines quality is no longer the act of writing code. It is the act of preparation: specifying precisely what needs to be built, deciding what matters and what does not, and validating that the output matches intent.

**Dandori is the recognition that in AI-augmented software development, preparation is the work.**

> *"Scrum optimized for production. Kanban optimized for flow. Dandori optimizes for preparation, because when AI handles production and flow is continuous, the quality of what you prepare determines everything."*

---

Note on scope: Dandori is about better preparation, not more documentation. Artifacts are lean and exist only to make execution and validation unambiguous; if a document does not add clarity or decisions, it is waste.

## Download

| Document | Format | Description |
| ---------- | -------- | ------------- |
| [**The Dandori Framework**](dandori-framework.pdf) | [PDF](dandori-framework.pdf) | The complete framework (all chapters) |
| [**The Dandori Manifesto**](MANIFESTO.md) | [Markdown](MANIFESTO.md) ・ [PDF](docs/assets/dandori-manifesto.pdf) | The values and 12 principles |
| [**Dandori at a Glance**](ONE-PAGER.md) | [Markdown](ONE-PAGER.md) ・ [PDF](docs/assets/dandori-onepager.pdf) | The entire framework on a single page |

---

## Why Dandori

Scrum, as practiced in most organizations, has lost its meaning. Every company interprets it differently. Every team within the same company has different agreements. AI is simultaneously joining software teams as a participant, amplifying what the same team can deliver. These two truths demand a coordination model designed for the present reality.

## What Dandori Provides

- A **five-stage specification lifecycle**: Intent, Specification, Execution, Validation, Integration
- **Three defined roles**: Spec Owner, Reviewer, Prioritizer
- A **product management alignment model** for the spec-driven interface
- A **redefined engineering management function** split into System Operator and Talent Architect
- **Ceremonies that transform** rather than eliminate Scrum's core practices
- **Liberating Structures** facilitation guidance for every ceremony
- **Metrics** designed for spec-driven flow rather than sprint velocity

## Read Dandori

Dandori is published from this single repository to multiple platforms:

- **GitHub Pages (MkDocs Material)**: [GTuritto.github.io/dandori](https://GTuritto.github.io/dandori/) -- auto-deployed on every push
- **GitHub**: Read the Markdown files directly in this repository

## Templates

Optional, lightweight scaffolds to help teams pilot Dandori. Use as-is or adapt to your context:

- [Intent template](templates/intent-template.md)
- [Specification template](templates/spec-template.md)
- [Decision Request template](templates/decision-request-template.md)
- [Integration Review template](templates/integration-review-template.md)
- [Spec Retrospective template](templates/spec-retro-template.md)

## Table of Contents

- [Executive Summary](docs/executive-summary.md)
- [What Dandori Is and Is Not](docs/what-dandori-is-not.md)
- [Fit and Boundaries](docs/fit-and-boundaries.md)
- [Failure Modes and Corrections](docs/failure-modes.md)
- [Getting Started (Incremental Adoption)](docs/getting-started.md)
- [Pilot Guide (4–6 Weeks)](docs/pilot-guide.md)

### Part I: Why Dandori

- [1. Scrum Is Already Broken](docs/part-1-why/01-scrum-is-broken.md)
- [2. AI Is Joining the Team](docs/part-1-why/02-ai-joining-team.md)
- [3. The Economic Argument](docs/part-1-why/03-economic-argument.md)
- [4. The Failure Mode Argument](docs/part-1-why/04-failure-modes.md)
- [5. The Empirical Argument](docs/part-1-why/05-empirical-argument.md)
- [6. The Talent Argument](docs/part-1-why/06-talent-argument.md)
- [7. The Strategic Argument](docs/part-1-why/07-strategic-argument.md)
- [8. The Philosophical Argument](docs/part-1-why/08-philosophical-argument.md)
- [9. The Problems Scrum Never Solved](docs/part-1-why/09-problems-scrum-never-solved.md)

### Part II: What Is Dandori

- [9. Core Principles](docs/part-2-what/09-core-principles.md)
- [10. The Specification Lifecycle](docs/part-2-what/10-specification-lifecycle.md)
- [Spec-Driven Development in Practice](docs/part-2-what/10b-understanding-sdd.md)
- [11. Roles](docs/part-2-what/11-roles.md)
- [Team Size](docs/part-2-what/11b-team-size.md)
- [Dandori Solo: The Single Engineer](docs/part-2-what/11c-dandori-solo.md)
- [12. Product Management Alignment](docs/part-2-what/12-product-alignment.md)
- [13. The Engineering Manager's Role](docs/part-2-what/13-em-role.md)
- [14. Relationship to Existing Methodologies](docs/part-2-what/14-methodology-comparison.md)
- [How Traditional Documents Fit Into Dandori](docs/part-2-what/14b-document-landscape.md)

### Part III: How Dandori Works

- [15. Ceremonies](docs/part-3-how/15-ceremonies.md)
- [A Week With Dandori](docs/part-3-how/15b-a-week-with-dandori.md)
- [16. What Dandori Transforms](docs/part-3-how/16-transformations.md)
- [17. Metrics and Measurement](docs/part-3-how/17-metrics.md)
- [18. Facilitation: Liberating Structures](docs/part-3-how/18-liberating-structures.md)
- [19. Prerequisites](docs/part-3-how/19-prerequisites.md)
- [20. Conclusion](docs/part-3-how/20-conclusion.md)

## License

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

You are free to share and adapt this framework, even commercially, as long as you give appropriate credit and distribute any adaptations under the same license.

## Contributing

Dandori is an open framework. Contributions, feedback, and real-world experience reports are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

*Version 1.0 | March 2026*
