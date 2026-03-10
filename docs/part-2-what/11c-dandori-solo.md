# Dandori Solo: The Single Engineer Variant

Dandori's minimum team size is three people, because the framework's quality model depends on the separation between the person who writes the specification and the person who reviews the output. A solo engineer cannot maintain that separation. They will unconsciously validate their own intent rather than what was actually produced.

But solo engineers exist. Freelancers, indie developers, startup founders writing their own code, internal teams of one supporting a specific system. They deserve a coordination model too, not just "do whatever works," which is what most frameworks offer them. This section defines what Dandori looks like for a single engineer, what is preserved, what is lost, and what compensates for the gap.

## What a Solo Engineer Keeps

### The Specification Lifecycle

The five stages (Intent, Specification, Execution, Validation, Integration) work for one person. Writing an intent document before jumping into specification forces you to articulate why you are building something, not just what. Writing a specification before execution forces you to think before you code. Validating against explicit acceptance criteria after execution forces you to check whether the output matches the intent rather than assuming it does because you wrote both.

The lifecycle is a thinking discipline. It works regardless of team size.

### The Specifiability Classification

Classifying work as Clear, Complex, or Uncertain is valuable even solo. Clear work goes straight to spec and execution. Complex work gets a written Pre-Mortem (even if it is just you writing down what could go wrong and challenging your own assumptions for 10 minutes). Uncertain work gets an exploration spike before you invest time in a specification. This prevents the solo engineer's most common failure mode: jumping into implementation on something they do not understand well enough, discovering the problem is harder than expected halfway through, and either pushing through with a bad approach or abandoning the work entirely.

### Spec Patterns

A solo engineer benefits enormously from maintaining a personal spec patterns library. Every time a specification fails (the AI output does not match intent, or a deployed feature has issues), the engineer documents what was missing from the spec and adds a pattern. Over time, this library becomes a checklist that prevents recurring mistakes. It is a solo engineer's institutional memory.

### The Specification as Documentation

For a solo engineer, the specification repository is the primary project documentation. Every decision is recorded in the spec's Architectural Decision section. Every acceptance criterion documents expected behavior. When the solo engineer returns to a feature six months later (or when someone else eventually joins the project), the spec repository tells them what was built, why, and what the constraints were.

### Flow Metrics

Cycle time, first-pass success rate, and spec failure classification are all measurable by one person. Tracking them reveals patterns: which types of specs consistently fail on first execution? Where does the most time go, specification or validation? Is the first-pass success rate improving as the spec patterns library grows? These metrics are a conversation with yourself about whether your process is working.

## What a Solo Engineer Loses

### Independent Review

This is the biggest loss. No one catches the things you do not see. A human Reviewer brings independent judgment: architectural perspective you might miss, edge cases you did not think of, and the simple act of reading a spec with fresh eyes and finding ambiguities the author cannot see.

### The Decision Challenge

Decision Requests in a team force decisions to be explicit and debated. A solo engineer makes decisions implicitly, often without considering alternatives. There is no PM to push back on a requirement, no Reviewer to question an architectural choice, no Prioritizer to challenge the priority order. Decisions happen, but they are not stress-tested.

### Ceremony-Driven Reflection

Most Dandori ceremonies exist to force reflection at specific intervals. The Pipeline Sync forces you to look at the whole pipeline. The Spec Retrospective forces you to examine failures. The Integration Review forces you to check architectural coherence. A solo engineer can do all of these, but without the ceremony structure, they tend to skip them when busy, which is exactly when they are most needed.

## What Compensates

### AI as a Spec Mirror

When a solo engineer writes a specification and an AI agent executes against it, the AI's output is a literal interpretation of the spec. If the output does not match the engineer's intent, the spec was ambiguous. This is not the same as a human Reviewer, but it is a feedback mechanism. The AI will not fill gaps the way a human developer would. It will either execute the gap literally (producing something the engineer did not intend) or fail (producing nothing for the underspecified portion). Both outcomes reveal spec quality issues.

The discipline is: when the AI output does not match intent, resist the urge to fix the code. Instead, fix the specification. Then re-execute. This forces the engineer to improve spec precision rather than relying on code-level patches that leave the spec inaccurate.

### Self-Review with Time Delay

One compensating practice: do not review AI output immediately after writing the spec. Wait at least a few hours, ideally overnight. The gap between writing and reviewing allows the engineer to approach the output with fresher eyes, closer to (though never equal to) an independent reviewer's perspective. Review the output against the acceptance criteria as if someone else wrote both the spec and the code. This requires discipline but significantly improves review quality.

### Written Pre-Mortems

A solo engineer cannot run a Pre-Mortem ceremony with other people, but they can write one. Before executing a Complex or Uncertain spec, spend 10 minutes writing answers to: "How could this spec produce a catastrophic failure?" and "What am I assuming that might not be true?" Writing forces precision that thinking alone does not. A written Pre-Mortem, even if brief, catches assumptions that a mental review misses.

### Weekly Self-Retrospective

Replace the Pipeline Sync, Spec Retrospective, and Integration Review with a single weekly 30-minute self-retrospective. Review the week's pipeline: what moved through, what got stuck, what failed validation. Examine spec failures: what patterns emerge? Update the spec patterns library. Check architectural coherence: do this week's changes make sense together? This is one ceremony that combines what three ceremonies do for a team.

### External Review for High-Risk Work

For specifications that are Complex or Uncertain, especially those touching security, financial calculations, or user data, a solo engineer should seek external review. This could be a peer in a professional community, a paid code review service, or a colleague at another company. The review does not need to happen for every spec, only for the ones where the consequences of getting it wrong are significant. This is the escape valve for the independent review gap.

## Dandori Solo: The Minimum Practice

For a solo engineer adopting Dandori, the minimum practice is:

1. **Write specifications before execution.** Not for everything. For any work that is Complex or Uncertain, or any work where the consequences of a mistake are significant. Clear, low-risk work can use a lighter version.

2. **Classify work** as Clear, Complex, or Uncertain. Use the classification to decide how much specification rigor the work needs.

3. **Maintain a spec patterns library.** Update it whenever a spec fails. This is your personal quality improvement system.

4. **Track first-pass success rate.** If AI output consistently fails to match your intent on the first pass, your specs are not precise enough. The metric tells you whether you are improving.

5. **Run a weekly self-retrospective.** 30 minutes. Pipeline review, failure analysis, pattern updates, architectural coherence check.

6. **Seek external review for high-risk specs.** Do not rely solely on your own judgment for work that has significant consequences.

This is not full Dandori. It is Dandori's principles and lifecycle applied to a solo context with honest acknowledgment of what is lost. It is better than no framework, better than "just start coding," and it scales naturally: when a second person joins the project, the specifications, the patterns library, and the metrics are already in place. The transition from Dandori Solo to full Dandori is adding a Reviewer and splitting the ceremonies, not starting from scratch.
