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
