# A Week With Dandori

Theory describes what a framework is. Practice shows what it feels like. This chapter follows a team through one full week of working with Dandori, showing what each day looks like, which ceremonies happen, and how work flows through the pipeline. The team, the tools, and the domain are fictional, but the rhythm is real.

## The Team

A product team at a mid-size SaaS company building a project management platform. Six people:

- **Marta** (Senior Engineer, primary Spec Owner): Writes most specifications, deep domain knowledge of the platform's core data model.
- **Tomek** (Senior Engineer, primary Reviewer): Strong architectural instincts, catches systemic issues others miss. Also writes specs for his area of expertise.
- **Lucia** (Mid-level Engineer, Spec Owner in training): Growing into the Spec Owner role, currently handles Clear specs independently and pairs with Marta on Complex ones.
- **James** (UX Designer): Contributes interaction patterns and accessibility requirements to specifications.
- **Priya** (QA Engineer): Shapes acceptance criteria, contributes edge cases, runs exploratory testing during validation.
- **David** (Product Manager, shares Prioritizer role with Marta): Owns the intent queue, writes intent documents, responds to Decision Requests.

Their Engineering Manager, **Sofia**, oversees this team and one other. She attends the Integration Review and facilitates the monthly Team Retrospective. Day to day, she monitors the pipeline dashboard and steps in when systemic issues surface.

The team uses Claude Code for AI-assisted execution. Some specs are fully AI-executed. Some are human-implemented with AI assistance. Some, particularly UI-heavy work where James's designs are intricate, are primarily human-built. The framework does not care which. The coordination model is the same.

---

## Monday

### 9:00 AM — Pipeline Sync (15 minutes)

The team opens the pipeline board. Currently in flight:

- **In Intent:** Two new items David added Friday afternoon. One is a customer-reported issue with notification timing. The other is a strategic initiative to add a Gantt chart view.
- **In Specification:** One spec Marta started Friday (PROJ-087: batch task reassignment). She hit an ambiguity and sent a Decision Request to David.
- **In Execution:** One spec (PROJ-085: keyboard shortcuts for task navigation) went to Claude Code on Friday. Output is ready for review.
- **In Validation:** One spec (PROJ-084: email digest customization) that Tomek has been reviewing. He found one acceptance criterion failing.
- **In Integration:** Nothing pending. Last week's work all shipped.

Using 1-2-4-All: everyone silently scans the board for one minute. Pairs discuss for two minutes. Marta and Tomek note that PROJ-085's output arrived fast but PROJ-087 is blocked on David's decision. Lucia and Priya note that PROJ-084's failing criterion is a minor formatting issue and should resolve quickly.

Full group for five minutes. Two items surface: David needs to resolve the Decision Request for PROJ-087 this morning (it has been pending 18 hours, approaching the tactical SLA). And someone needs to start reviewing PROJ-085. Tomek takes it since he will finish PROJ-084's re-validation first.

Total time: 14 minutes. Everyone knows what is flowing, what is stuck, and what they are doing next.

### 9:30 AM — Marta starts specifying the notification timing issue

David's intent document for the notification issue is brief but clear: customers report that notifications for task updates arrive 15-45 minutes late. Success criteria: notifications delivered within 60 seconds of the triggering event, 99th percentile. Constraint: must not increase infrastructure costs by more than 5%.

Marta reads the intent, checks the existing notification service code, and begins writing the specification. She identifies the root cause during spec research: notifications are batched in 15-minute windows for cost efficiency. The fix requires changing the batching strategy.

She includes an Architectural Decision section: real-time push via WebSocket for active users, batched delivery only for offline users. She documents why: the current batching strategy was chosen when the platform had 1,000 users. At 50,000 users, the latency is unacceptable for active users but batching still makes sense for offline delivery to keep costs within David's 5% constraint.

### 10:00 AM — David resolves the Decision Request

David reads Marta's Decision Request for PROJ-087 (batch task reassignment). The question: when reassigning tasks in batch, should the system send individual notifications to each new assignee, or a single summary notification? Options: (A) individual notifications, more noisy but each person sees exactly their task; (B) summary notification, less noise but requires the recipient to click through to see details.

David responds within the 4-hour tactical SLA: Option A, with a follow-up intent to add notification preferences in a future spec. Marta unblocks and finishes PROJ-087's specification.

### 11:00 AM — Spec Handoff: PROJ-087

Marta walks Tomek through PROJ-087 in 12 minutes. She highlights the batch size constraint (maximum 50 tasks per operation for performance), the notification decision (individual per assignee), and the acceptance criteria (7 criteria covering permission checks, partial failure handling, and undo behavior). Tomek asks about what happens if one of the 50 reassignments fails partway through. Marta realizes the spec does not address partial failure atomicity. She adds a criterion: if any reassignment in the batch fails, all reassignments in the batch must roll back, and the user must see which specific tasks failed and why.

The handoff caught a real gap. This is exactly what the ceremony is for.

### 11:15 AM — PROJ-087 goes to Execution

Marta sends the spec to Claude Code. The AI begins implementing.

### 11:30 AM — Tomek finishes re-validation of PROJ-084

The email digest customization spec passes all criteria on the second pass. The formatting issue is fixed. PROJ-084 moves to Integration. Tomek merges the PR and archives the spec.

### 1:00 PM — Tomek starts reviewing PROJ-085

PROJ-085 (keyboard shortcuts) was AI-generated over the weekend. Tomek reviews against 8 acceptance criteria. Six pass immediately. Two issues: the keyboard shortcut for "move task up" conflicts with a browser default shortcut (Ctrl+Up), and the focus management after a shortcut action does not follow the WAI-ARIA pattern specified in criterion #7.

Tomek sends the spec back to Execution with specific notes. He also messages Priya to flag the accessibility issue for her exploratory testing queue.

### 3:00 PM — PROJ-087 output arrives from Claude Code

Fast turnaround. Marta glances at it but Tomek is the assigned Reviewer. It will wait for tomorrow's review.

### End of Monday

Pipeline state:
- **Intent:** Gantt chart view (waiting for prioritization), notification timing (Marta still specifying)
- **Specification:** Notification timing (in progress)
- **Execution:** PROJ-085 (back for second pass after review feedback)
- **Validation:** PROJ-087 (output arrived, awaiting Tomek's review)
- **Integration:** PROJ-084 shipped today

---

## Tuesday

### 9:00 AM — Pipeline Sync (12 minutes)

Short sync. PROJ-084 shipped. PROJ-085 is back in execution for the keyboard shortcut fixes. PROJ-087 is waiting for Tomek to review. Marta is finishing the notification timing spec (PROJ-088). No blockers. No systemic issues. The 1-2-4-All takes 8 minutes and the group discussion takes 4.

### 10:00 AM — Marta finishes PROJ-088 and triggers a Pre-Mortem

The notification timing spec is Complex: it touches the real-time messaging infrastructure, changes the batching strategy, and introduces WebSocket connections for active users. Marta classifies it as Complex and schedules a Pre-Mortem.

### 10:30 AM — Pre-Mortem for PROJ-088 (25 minutes)

Marta, Tomek, Priya, and James attend. Using TRIZ: "How could we guarantee this spec produces a catastrophic failure?"

The team generates disaster scenarios: WebSocket connections exhaust server memory at scale. The "active user" detection is wrong and everyone gets real-time push, blowing through the cost constraint. The batching-to-real-time migration corrupts the notification queue during deployment. The 60-second SLA is measured incorrectly because the clock starts at the wrong event.

Then they invert: which of these are real risks?

The WebSocket memory concern is real. Marta adds a constraint: maximum 10,000 concurrent WebSocket connections, with graceful fallback to polling. The "active user" detection needs a precise definition. Marta adds it: a user is "active" if they have had a page interaction in the last 5 minutes. The migration risk is real. Marta adds a requirement: the old batching system must run in parallel during rollout, with a feature flag to switch back within 30 seconds.

The Pre-Mortem added three constraints and one acceptance criterion that the spec did not originally have. Time well spent.

### 11:00 AM — Spec Handoff: PROJ-088

Marta walks Tomek through the notification spec. 15 minutes. Tomek focuses on the WebSocket fallback mechanism and the parallel-run deployment strategy. He is satisfied he understands the intent.

PROJ-088 goes to Execution.

### 2:00 PM — Tomek reviews PROJ-087

Tomek reviews the batch reassignment output against 8 acceptance criteria (7 original plus the partial failure criterion added during handoff). All pass. He runs a few exploratory scenarios and finds that the UI feedback for "reassignment in progress" disappears too quickly for large batches. This is not a spec failure (the spec did not specify feedback duration), but it is a UX issue.

Tomek approves PROJ-087 for integration but opens a new intent: "Batch operation progress feedback needs minimum display duration." This becomes a future Clear spec. PROJ-087 moves to Integration.

### 3:30 PM — Lucia finishes her first independent Complex spec

Lucia has been writing PROJ-089 (workspace template duplication) with Marta available for questions but not co-writing. She has grown enough to handle Complex specs with light guidance. She schedules a Spec Handoff with Priya (who will be the Reviewer for this one) for tomorrow morning.

### End of Tuesday

Pipeline state:
- **Intent:** Gantt chart view, batch progress feedback (new from Tomek's review finding)
- **Specification:** Nothing in progress (all shipped to execution or handoff)
- **Execution:** PROJ-085 (second pass), PROJ-088 (notification timing), PROJ-089 (pending handoff tomorrow)
- **Validation:** Nothing pending
- **Integration:** PROJ-084 and PROJ-087 shipped

---

## Wednesday

### 9:00 AM — Pipeline Sync (10 minutes)

Shortest sync of the week. Two specs in execution, one pending handoff, nothing blocked. Lucia will do the PROJ-089 handoff right after the sync. PROJ-085's second pass output arrived overnight. Tomek will re-validate.

### 9:15 AM — Spec Handoff: PROJ-089

Lucia walks Priya through the workspace template spec. This is a learning moment: Priya asks about how the spec handles templates with integrations that the target workspace does not have. Lucia realizes she did not specify that edge case. She adds a criterion: if the template includes integrations not available in the target workspace, the duplication must succeed with those integrations marked as "unavailable," and the user must see a clear message listing which integrations need to be set up.

The handoff pattern is working as a teaching tool. Lucia is learning to anticipate the questions Reviewers will ask.

### 10:00 AM — Integration Review (35 minutes)

Weekly ceremony. The whole team plus David attends. Sofia joins from the dashboard to listen but lets Marta facilitate.

**What shipped this week:** PROJ-084 (email digest customization) and PROJ-087 (batch task reassignment). Both integrated cleanly. PROJ-084 was a first-pass success. PROJ-087 required no code revision but surfaced a UX finding that became a new intent.

**Patterns:** The team's first-pass success rate this week is 50% (one of two specs passed validation on first attempt). Lower than the 70% target. Tomek notes this is not a trend; last week was 80%. The specs this week were both Complex, which have a naturally lower first-pass rate. Using W3: the "So What" is that Complex specs involving UI feedback (PROJ-085's accessibility issue, PROJ-087's progress display) are the most common source of revision. The "Now What" is that the team should consider adding a standard section to UI-related specs: "Feedback and State Communication," which explicitly addresses loading states, progress indicators, success/error messages, and accessibility announcements.

**Architectural check:** PROJ-087's batch reassignment uses optimistic locking. PROJ-088 (notification timing, still in execution) will introduce WebSockets. David asks whether the two will interact. Tomek confirms they do not share data paths, but flags that both add server-side state management and suggests monitoring memory usage after both ship. Sofia makes a note to watch infrastructure metrics.

### 10:45 AM — Spec Retrospective (30 minutes)

Marta, Tomek, Lucia, and Priya attend. David does not (this is an engineering ceremony).

Using Troika Consulting: Lucia presents the workspace template edge case she missed (integrations not available in target workspace). Two minutes of description, then Tomek and Marta consult while Lucia listens. Tomek suggests a pattern: "Any spec involving duplication or copying must include a section on what happens when the source and target environments differ." Marta agrees and notes that this also applies to import/export features.

The team adds this to the spec patterns library. This is the third pattern added this month. The library is growing into a genuine institutional asset.

Second round: Marta presents the PROJ-088 Pre-Mortem and what it caught (WebSocket limits, active user definition, parallel-run deployment). The team discusses whether Pre-Mortems should be standard for any spec touching real-time infrastructure, not just Complex specs in general. They agree: any spec that introduces a new communication protocol or changes an existing one gets a Pre-Mortem regardless of classification.

### 2:00 PM — Tomek re-validates PROJ-085

Second pass. The keyboard shortcut conflict is resolved (changed to Alt+Up, which does not conflict). The accessibility focus management now follows WAI-ARIA correctly. All 8 criteria pass. Priya does 20 minutes of exploratory testing on keyboard navigation flows and finds no additional issues. PROJ-085 moves to Integration.

### 3:00 PM — Prioritization Reset / Flow Planning (30 minutes)

Marta and David attend. Lucia joins for the Intent Triage portion.

**Queue review:** Two intents waiting. The Gantt chart view is a large initiative that David classifies as **Uncertain** (needs significant research into rendering performance and data modeling). The batch progress feedback is **Clear** (well-understood UX improvement, small scope).

**Flow Planning:** The team has bandwidth for one more spec this week. The batch progress feedback (Clear) can be specified and executed by Friday. The Gantt chart view needs an exploration spike first, which David schedules for next week. Lucia takes the batch progress feedback spec.

**Capacity check:** PROJ-088 (notification timing) is still in execution. When it arrives, Tomek will need significant review time given its complexity. The team decides not to start any new Complex specs until PROJ-088 clears validation, to avoid overwhelming Tomek's review bandwidth.

This is Flow Planning in action: not "how many story points can we fit?" but "given what is in the pipeline, what can we responsibly add without creating a review bottleneck?"

---

## Thursday

### 9:00 AM — Pipeline Sync (11 minutes)

PROJ-085 shipped yesterday. PROJ-088 output arrived overnight from Claude Code. Tomek will start his review. Lucia is writing the batch progress feedback spec (PROJ-090). No blockers.

### 9:30 AM — Lucia writes PROJ-090 (batch progress feedback)

This is a Clear spec. She writes it in 90 minutes. Six acceptance criteria covering minimum display duration (3 seconds), animation, error state display, and screen reader announcements. She schedules a Spec Handoff with Tomek for after lunch.

### 10:00 AM — Tomek begins reviewing PROJ-088 (notification timing)

This is the big one. Complex spec with WebSocket infrastructure, batching strategy changes, and a parallel-run deployment requirement. Tomek reviews systematically against 11 acceptance criteria plus the 3 constraints added during the Pre-Mortem.

9 of 11 criteria pass. Two fail: the WebSocket fallback to polling triggers at 10,001 concurrent connections as specified, but the fallback is not graceful (users experience a 3-second gap with no notifications during the switch). And the "active user" detection uses last page load time rather than last interaction time, which means a user who has been reading the same page for 6 minutes gets switched to batched delivery even though they are actively looking at the screen.

Tomek writes detailed validation notes and sends the spec back to Execution with the specific issues. He tags Marta to review whether the "active user" definition in the spec was ambiguous (it said "page interaction," which Claude Code interpreted as "page load" rather than "any interaction including scroll or mouse movement").

### 1:00 PM — Spec Handoff: PROJ-090

Lucia walks Tomek through the batch progress feedback spec. 10 minutes. Straightforward. Tomek has one suggestion: add a criterion for what happens if the user navigates away while a batch operation is in progress. Lucia adds it: a subtle notification badge appears when the operation completes, visible when the user returns.

PROJ-090 goes to Claude Code.

### 3:00 PM — Marta reviews the PROJ-088 validation failure

She looks at Tomek's notes. The "active user" definition was indeed ambiguous in her spec. "Page interaction" could mean page load or any user interaction. She revises the spec to be precise: "A user is considered active if any of the following events have occurred in the current browser tab within the last 5 minutes: mouse movement, scroll, keyboard input, or click. Page load alone does not constitute activity."

She also adds a constraint for the WebSocket fallback: "When transitioning from WebSocket to polling, the system must maintain a 500ms overlap where both channels are active, ensuring no notifications are lost during the transition."

The revised spec goes back to Execution with the two specific fixes annotated.

### End of Thursday

Pipeline state:
- **Intent:** Gantt chart view (scheduled for exploration spike next week)
- **Specification:** Nothing in progress
- **Execution:** PROJ-088 (second pass with revised spec), PROJ-090 (batch progress feedback)
- **Validation:** Nothing pending
- **Integration:** PROJ-084, PROJ-085, PROJ-087 shipped this week

---

## Friday

### 9:00 AM — Pipeline Sync (8 minutes)

Shortest sync of the week. PROJ-088 second pass output arrived. PROJ-090 output arrived. Both need review. Tomek will validate PROJ-090 first (Clear spec, should be quick) then tackle PROJ-088's second pass. No blockers.

### 9:30 AM — Tomek validates PROJ-090 (batch progress feedback)

All 7 criteria pass on first attempt. First-pass success. Priya runs 15 minutes of exploratory testing. Clean. PROJ-090 moves to Integration. Lucia's confidence grows. She has now delivered a Clear spec independently, from specification through first-pass validation, in under two days.

### 10:30 AM — Tomek re-validates PROJ-088 (notification timing)

Second pass. Both issues are resolved. The active user detection now uses the precise interaction-based definition. The WebSocket-to-polling transition maintains the 500ms overlap. All 11 criteria pass. Priya runs 30 minutes of exploratory testing on the notification flow, including simulating high connection counts. She finds one minor issue: the notification sound plays twice during the overlap window. This is not a spec failure (the spec did not address notification sounds during transition), but Priya logs it as a new intent: "Deduplicate notification sounds during WebSocket-to-polling transition."

PROJ-088 moves to Integration. The team's largest spec this week ships on Friday with one cycle of revision. The Pre-Mortem constraints held up: no memory issues, the parallel-run flag works, and the cost impact is within the 5% constraint.

### 12:00 PM — Integration and week close

Marta merges PROJ-088 and PROJ-090. The specification repository now has four new specs archived this week, each with full decision records, acceptance criteria, and validation history.

Sofia reviews the weekly dashboard:
- **Specs integrated this week:** 4 (PROJ-084, 085, 087, 090) plus PROJ-088 integrated Friday afternoon
- **First-pass success rate:** 40% (2 of 5 passed on first attempt). Below the 70% target but explainable: three Complex specs this week, and the two failures were both specification ambiguity issues (not AI execution failures)
- **Average cycle time:** 3.2 days (skewed by PROJ-088 which took 4 days due to its complexity)
- **Decision latency:** All Decision Requests resolved within SLA
- **Spec pattern additions:** 2 new patterns (environment-mismatch handling, real-time protocol Pre-Mortem trigger)

---

## What the Team Never Did This Week

They never estimated story points. They never debated sprint capacity. They never sat through a two-hour planning session negotiating what to commit to. They never held a demo where they performed delivery for stakeholders. They never wrote a status report.

They did think carefully about what to build. They did specify it precisely. They did catch problems before and during validation. They did improve their spec patterns. They did maintain architectural awareness across the pipeline. And they shipped five features in five days, including one complex infrastructure change, with full traceability from intent to integration.

That is a week with Dandori.
