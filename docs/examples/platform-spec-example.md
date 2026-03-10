# Specification Template — Example (Platform)

## Title

Distributed tracing across services A/B/C using OpenTelemetry

## Summary

Lack of end‑to‑end request visibility slows incident resolution and obscures latency regressions. Introduce distributed tracing across services A/B/C with consistent trace/segment IDs and correlation into logs and metrics.

## Background

Currently, services log request IDs inconsistently and emit partial metrics. Cross‑service latency is inferred. P1 incidents require manual log stitching.

## Problem statement

We cannot reliably follow a request across services or attribute latency to a specific hop. MTTR remains high; regressions ship unnoticed.

## Desired outcome

≥ 95% of inbound requests produce a complete trace spanning services A/B/C with service/hop timings and error annotations. On‑call can pivot from an incident to the slow hop within 2 minutes.

## Scope

### In scope

- HTTP/gRPC ingress for A/B/C
- Asynchronous messaging between B→C
- Trace context propagation and sampling policy

### Out of scope

- Legacy admin service D
- Mobile client instrumentation (tracked separately)

## Users / stakeholders affected

- Platform/Infra: owns tracing stack and sampling policy
- Service owners A/B/C: adopt instrumentation
- Support/On‑call: use traces during incidents

## Constraints

- Overhead ≤ 3% CPU and ≤ 5% latency on P95
- No PII in traces; follow existing data retention policy
- Self‑hosted collector; no new vendor contracts this quarter

## Requirements

### Functional requirements

- Inject/extract W3C trace context across HTTP/gRPC and messaging
- Emit spans with standard attributes (service, http.method, status, db.statement redacted)
- Correlate trace_id with structured logs

### Non-functional requirements

- Trace coverage ≥ 95% for A/B/C ingress within 30 days
- Sampling: 10% baseline with dynamic upsampling on 5xx bursts
- Storage retention: 14 days

## Acceptance criteria

- Synthetic request across A→B→C yields a single trace with three service spans and correct timing within ±10ms tolerant error.
- Incident drill: pager on 5xx burst; on‑call locates slow hop and error cause via trace within 2 minutes.
- Overhead measured in staging ≤ 3% CPU/≤ 5% P95.

## Proposed approach

- Adopt OpenTelemetry SDKs/auto‑instrumentation for A/B/C (language‑appropriate).
- Deploy OTel Collector with pipelines → export to existing metrics/logs backends.
- Implement middleware for context propagation in messaging.
- Add logging interceptor to append trace_id/span_id to structured logs.

## Alternatives considered

### Alternative 1

Custom request IDs only. Rejected: lacks timings, spans, and ecosystem support.

### Alternative 2

Buy managed tracing now. Rejected this quarter due to procurement timing; revisit next Q.

## Dependencies

- Existing metrics/logs backends capacity
- Sidecar/base image updates for services

## Risks

- Sampling too low to capture rare failures
- Excess cardinality from labels

## Mitigations

- Dynamic sampling rules for error conditions; targeted always‑on sampling for critical routes
- Attribute allow‑list; drop high‑cardinality fields

## Validation plan

- Staging load: confirm coverage, overhead, and span correctness
- Fault injection: induce B 5xx and verify drill success
- Dashboards: trace coverage, collector queue depth, span export failures

## Rollout / release notes

- Week 1: A service; Week 2: B; Week 3: C; Week 4: sampling tuning
- Canary 10% traffic per service; expand when overhead within thresholds
- Rollback: disable exporter; keep context propagation

## Operational considerations

- Ownership: Platform team (collector), service owners (SDK updates)
- Monitoring: coverage %, export latency, collector CPU/mem
- Alerting: coverage drop > 10pp, collector queue backpressure
- Runbooks: collector restart, sampling change, SDK version rollback

## Decisions already made

- Use W3C Trace Context and OTel semantic conventions
- Export to existing backends (no new vendor)

## Decisions still needed

- Whether to enable DB/sql instrumentation in C (privacy review)

## Completion criteria

- Coverage ≥ 95% for A/B/C ingress for 7 consecutive days; incident drill passed
- Runbooks and ownership acknowledged by teams

## References

- RFC: Tracing adoption plan (link)
- OTel semantic conventions (link)
- Logging guide with trace correlation (link)
