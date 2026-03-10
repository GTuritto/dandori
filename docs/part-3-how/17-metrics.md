# 17. Metrics and Measurement

Dandori supplements (or, in mature teams, replaces) velocity with flow and quality metrics.

| Metric | What It Measures | Healthy Signal |
|--------|-----------------|----------------|
| **Cycle Time** | Average time from Intent to Integration | Decreasing or stable |
| **First-Pass Success Rate** | Specs where AI output passes validation without revision | Increasing (target: 70%+) |
| **Decision Latency** | Time between Decision Request and resolution | Within SLA (4hr tactical, 24hr strategic) |
| **Stage Dwell Time** | Time a spec spends in each lifecycle stage | Balanced flow, no single stage dominates |
| **Validation Rework Rate** | Specs cycling back from Validation to Specification | Decreasing (target: under 20%) |
| **Spec Failure Classification** | Distribution by type: ambiguity, AI limitation, review miss, operational | Spec ambiguity decreasing |
| **Pipeline WIP** | Specs in each stage at any point | No stage exceeding WIP limits |
| **Specifiability Accuracy** | How often Clear/Complex/Uncertain matched actual experience | Increasing accuracy |
| **Execution Mode Ratio** | AI-executed vs. human+AI vs. fully human | Tracked for trend, no fixed target |

These metrics serve the EM's System Operator function. They should be visible to the entire team on a shared dashboard, not hidden in management reports.

## Translating Metrics into Business Language

Engineering metrics are necessary but not sufficient. Cycle time, first-pass success rate, and pipeline WIP tell the EM whether the system is healthy. They tell the business nothing it cares about.

Business stakeholders, product leadership, and executives ask different questions: When will I get this feature? What happens if I change priorities? How much is this initiative going to cost? What is the risk that we miss a deadline? These are legitimate questions. If the framework cannot translate its metrics into answers, the business will fill the gap with their own narratives, and those narratives will often be wrong, as Gerard Boyle observed: "engineering ends up taking the hit as product tends to have more control over the narrative."

Dandori's pipeline visibility and flow metrics provide the raw data. The translation layer turns that data into business-consumable answers.

### "When Will I Get This?"

The honest answer comes from cycle time data broken down by specifiability classification. Instead of a sprint commitment that may or may not hold, the business gets a data-driven range:

| Classification | Typical Cycle Time | What the Business Hears |
|---------------|-------------------|------------------------|
| **Clear** | 2-3 days | "This is well-understood. Expect it within the week." |
| **Complex** | 5-7 days | "This requires design decisions. Expect it in one to two weeks." |
| **Uncertain** | 10-15+ days | "This needs research before we can specify it. Expect two to three weeks minimum, and we will update you after the exploration spike." |

This is less satisfying than "it will be done by Friday" but far more honest. And unlike sprint commitments, it does not require waiting until a review meeting to discover the truth. The business can check the pipeline at any time and see where their priority stands.

### "What Happens If I Change Priorities?"

The pipeline makes reprioritization costs visible. When a stakeholder wants to insert a new priority, the Prioritizer can show them the current pipeline state: here are the specs in execution (interrupting them has a cost), here are the specs in specification (they can be paused with minimal waste), here are the intents in the queue (they can be reordered freely). The conversation shifts from "can you squeeze this in?" to "here is what moves and here is what it costs."

The Decision Latency metric also surfaces a common but invisible cost. If the business is slow to respond to Decision Requests, the pipeline stalls. Showing stakeholders that three specs have been waiting for decisions for 48 hours, blocking everything downstream, translates engineering frustration into business language: "Your features are waiting for your decisions."

### "What Is the Risk?"

Risk in Dandori is measurable through the Spec Failure Classification and the Validation Rework Rate. If the rework rate is climbing, the business should know that output quality is at risk and the team is investing more time in corrections than in new features. If spec failures are dominated by ambiguity rather than AI limitations, the risk is upstream: the intents are not clear enough, which means the business and product are not providing sufficient clarity.

This feedback loop is important because it distributes accountability. In Scrum, engineering "took the hit" when things were late because the sprint commitment was an engineering promise. In Dandori, the metrics show where the system is constrained. If the bottleneck is decision latency, that is a product or business problem. If the bottleneck is spec quality, that is an engineering problem. If the bottleneck is validation throughput, that is a review capacity problem. The data makes it visible, which makes it actionable, and prevents any one party from controlling the narrative at the expense of the others.

### "How Much Does This Cost?"

Dandori does not prescribe how to translate engineering effort into financial terms, because that calculation is organization-specific. But the framework provides the inputs that make the calculation possible. Cycle time per spec, broken down by classification and team, gives a reliable basis for effort estimation. Pipeline throughput (specs integrated per week) gives a capacity baseline. The Execution Mode Ratio shows how much of the work is AI-assisted versus human-intensive, which has direct cost implications.

The EM's responsibility is to maintain this translation layer. Not as a one-time report, but as a standing capability: the business can ask these questions at any time and get answers grounded in real pipeline data rather than estimates, promises, or narratives.

### Who Controls the Narrative?

In many organizations, strategy and product control the narrative about software delivery. Engineering's perspective gets filtered, simplified, or lost. This is not malice. It is a structural consequence of who writes the status reports and who presents to leadership.

Dandori's pipeline visibility addresses this by making the system's state observable to everyone. The pipeline is not an engineering tool that gets summarized for the business. It is a shared artifact that all parties can read directly. When the pipeline shows that five specs are blocked on Decision Requests from product, that is not engineering's narrative. It is the system's state. When the pipeline shows that three Complex specs integrated this week with a 75% first-pass success rate, that is not engineering's spin. It is measured reality.

The Integration Review, which includes the PM and can include stakeholders, is the ceremony where this shared visibility is discussed. It replaces the sprint review's demo format (which was engineering presenting to the business) with a joint inspection of the pipeline (which is everyone looking at the same data and discussing what it means).

This does not eliminate organizational politics. No framework can. But it reduces the information asymmetry that enables narrative control, and it gives engineering a factual basis for its perspective that is harder to dismiss than a verbal status update in a sprint review.
