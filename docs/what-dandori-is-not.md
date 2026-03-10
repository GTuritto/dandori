# What Dandori Is and Is Not

## Dandori Is Not a Spec-Driven Development Tool

The emergence of AI in software development has produced a wave of spec-driven development (SDD) tools and frameworks: GitHub Spec Kit, AWS Kiro, the BMAD Method, OpenSpec, Tessl, and others. These tools focus on the developer workflow. They answer the question "how does a developer go from a specification to working code with AI assistance?" They provide CLIs, agent workflows, specification templates, and implementation pipelines.

Dandori is none of these things.

Dandori does not generate specifications. It does not execute code. It does not provide a CLI. It does not define a spec format or a prompt template. It does not depend on any specific AI tool, model, or vendor.

Dandori answers a different question entirely: **"How does a team coordinate when the way software gets built is changing?"**

Spec-Kit tells a developer how to structure a specification for GitHub Copilot. Dandori tells a team how to decide what gets specified, who writes the spec, who reviews the output, how priorities flow, when to meet, and how to know if the system is healthy. These are complementary, not competitive. A team could use Spec-Kit or Kiro or BMAD for their developer workflow and use Dandori for their team coordination. Or they could use no SDD tool at all and still use Dandori.

The distinction matters because confusing the two leads to wrong expectations. Someone expecting a developer tool will be disappointed. Someone looking for how to organize their team in a post-Scrum world will find exactly what they need.

## Dandori Is Tool-Agnostic

Dandori does not prescribe which AI tools a team should use. It does not assume GitHub Copilot, or Claude Code, or Cursor, or any specific model or platform. It does not even assume AI tools that follow the spec-driven development pattern.

A team using AI through embedded features in their CI/CD pipeline can use Dandori. A team using autonomous coding agents can use Dandori. A team using AI only for code review and test generation can use Dandori. A team using AI in ways that have not been invented yet can use Dandori.

This is deliberate. AI tools change every quarter. Any framework that ties itself to a specific tool or workflow pattern will be obsolete within a year. Dandori ties itself to the coordination problem, which is durable, not to the tools, which are not. The five-stage lifecycle (Intent, Specification, Execution, Validation, Integration) describes how work flows through a team regardless of whether the Execution stage is handled by an AI agent, a human developer with AI assistance, or a human developer with no AI at all.

## Dandori Works Without AI

This is the claim that most clearly separates Dandori from the SDD ecosystem: **a team that uses no AI whatsoever can still benefit from Dandori.**

The framework was born from two converging observations. The first is that AI is joining software teams. The second, and arguably the more fundamental one, is that Scrum is broken. These are independent problems. AI makes Scrum's dysfunction more visible and more costly, but the dysfunction existed before AI arrived.

Consider a team that writes no AI-generated code but suffers from the classic Scrum problems: ceremonies that have lost their meaning, estimation rituals that produce no useful signal, sprint boundaries that create artificial urgency or artificial slack, and a coordination model that optimizes for human labor allocation when the real bottleneck is decision quality and specification precision.

That team can adopt Dandori's principles (the specification as the unit of work, human judgment as the scarce resource, preparation determines quality), its roles (Spec Owner, Reviewer, Prioritizer), its ceremonies (Pipeline Sync, Integration Review, Spec Retrospective), and its metrics (cycle time, first-pass success rate, decision latency) without touching a single AI tool. The framework will make them more effective because it coordinates around the activities that actually determine software quality: thinking clearly about what to build, specifying it precisely, and validating that the output matches intent.

When that team later adopts AI tools, Dandori is already in place. The coordination model does not need to change. The team simply discovers that the Execution stage gets faster, which means the surrounding stages (Specification, Validation) become proportionally more important, which is exactly what the framework was designed to optimize.

This is what makes Dandori a team coordination framework rather than an AI development tool. It is a response to the modern reality of software delivery, of which AI is one part but not the only part. It works for teams with AI. It works for teams without AI. It works for teams that are somewhere in between. The coordination problem it solves, how to organize humans to produce high-quality software through precise specification, fast decisions, and rigorous validation, is universal.
