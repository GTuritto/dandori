# Understanding Spec-Driven Development

Dandori is built on the foundation of spec-driven development. Before diving into the framework's ceremonies and roles, it is essential to understand what spec-driven development is, what a specification looks like, and how work flows through the Dandori lifecycle in practice.

## What Is Spec-Driven Development?

Spec-driven development is the discipline of writing structured, precise specifications before implementation begins, and treating those specifications as the primary artifact around which all coordination happens.

This is not a new idea. It draws from formal methods, design-by-contract, behavior-driven development, and the structured engineering practices that predated agile. What makes it newly relevant is that AI execution engines can now implement against well-written specifications with high fidelity, making the specification the most leveraged artifact in the entire development process.

The core difference from traditional agile approaches is precision. A user story says "As a customer, I want to filter search results by price so I can find affordable options." That is enough for a human developer who can interpret intent, ask clarifying questions, and make reasonable assumptions. It is not enough for an AI agent, and frankly, it was never enough for consistent outcomes even with human developers. Teams that relied on vague stories compensated with verbal conversations, tribal knowledge, and implicit assumptions that new team members had to rediscover.

A specification makes all of that explicit. It captures not just what the user wants, but the constraints, the business rules, the edge cases, the acceptance criteria, and the architectural decisions that shape how the feature gets built.

## What a Specification Looks Like

There is no single "correct" format for a specification. Different teams will adapt the structure to their domain, their tools, and their level of AI maturity. What matters is that the spec is precise enough that someone (human or AI) can implement against it without guessing, and that a reviewer can validate the output against explicit criteria.

Here is an example specification for a realistic feature: adding a price filter to a travel search results page.

---

### Example Specification: Price Range Filter for Search Results

**Spec ID:** SEARCH-042

**Intent:** Customers searching for flights frequently abandon results pages when prices are higher than expected. Adding a price range filter allows customers to narrow results to their budget, reducing abandonment and increasing booking conversion on price-sensitive routes.

**Requirements:**

The search results page must display a price range filter that allows the customer to set a minimum and maximum price. The filter must apply to the total trip price including taxes and fees, not the base fare. The filter must update results in real time without requiring a page reload. When the filter is active, results outside the price range must be hidden, not removed from the underlying dataset, so the customer can adjust the range and see results reappear.

The filter must display the price distribution of available results as a histogram above the slider, showing the customer where most options cluster. The histogram must update when other filters (stops, airlines, departure time) are applied.

**Constraints:**

- The filter range must be bounded by the minimum and maximum prices in the current result set, not hardcoded values.
- Currency must match the customer's selected currency. No currency conversion happens at the filter level.
- The filter state must be preserved when the customer navigates to a booking page and returns to results using the browser back button.
- Performance: filtering must complete in under 100ms for result sets up to 500 items. For larger result sets, a loading indicator is acceptable but filtering must complete in under 500ms.
- The filter must be accessible: keyboard navigable, screen-reader compatible, and must announce filter changes to assistive technology.

**Interface Contract:**

The filter component receives the full result set and emits filtered results to the parent component. It does not make API calls. Filtering happens client-side against the already-loaded result set.

```
Props:
  results: Array<SearchResult>  // Full unfiltered result set
  currency: string              // ISO 4217 currency code
  onFilterChange: (filtered: Array<SearchResult>) => void

State:
  minPrice: number    // Customer-selected minimum
  maxPrice: number    // Customer-selected maximum
  rangeMin: number    // Lowest price in results
  rangeMax: number    // Highest price in results
```

**Acceptance Criteria:**

1. Given a result set with prices ranging from 50 to 800 EUR, when the page loads, the filter slider must show the full range (50-800) with both handles at the extremes.
2. Given the customer sets the maximum to 200 EUR, results with total price above 200 EUR must be hidden within 100ms.
3. Given the customer has set a filter and clicks on a result to view booking details, then presses the browser back button, the filter state must be restored with the same min/max values.
4. Given a result set of 500 items, filtering must complete in under 100ms as measured by time-to-render of the updated list.
5. Given a screen reader is active, when the customer adjusts the price slider, the new price range must be announced (e.g., "Price filter: 50 to 200 euros, showing 45 of 120 results").
6. Given other filters are active (e.g., "direct flights only"), the histogram must reflect only the currently visible results, not the full unfiltered set.

**Architectural Decision:**

Client-side filtering is chosen over server-side because the full result set is already loaded, and round-trip latency to the search API would degrade the real-time filtering experience. If future requirements include filtering across paginated result sets that are not fully loaded, this decision must be revisited.

---

This specification is longer than a user story. That is the point. The time invested in writing it is time saved in implementation (the AI or developer does not have to guess), in review (the reviewer has explicit criteria to check against), and in debugging (when something is wrong, you can trace it to a specific requirement or constraint that was missed).

## How This Flows Through Dandori

Now let us walk through how this specification moves through the five lifecycle stages, with the Dandori roles and ceremonies involved at each step.

### Stage 1: Intent

The product manager identifies that price-sensitive routes have a 23% higher abandonment rate than average. They write an intent document:

> **Problem:** Customers on price-sensitive routes abandon search results at a 23% higher rate. Customer research suggests they cannot quickly identify options within their budget.
>
> **Success Criteria:** Reduce abandonment rate on price-sensitive routes by at least 10 percentage points within 60 days of launch.
>
> **Constraints:** Must not increase page load time by more than 200ms. Must work within the existing search results architecture.

This intent enters the queue at the **Prioritization Reset / Flow Planning** ceremony. The Prioritizer (engineering lead + PM) reviews it, classifies it as **Clear** (well-understood problem, straightforward implementation, high confidence in AI execution), and assigns a Spec Owner.

### Stage 2: Specification

The Spec Owner, a senior frontend engineer, writes the specification shown above. They draw on the intent document, their knowledge of the existing search results architecture, and past spec patterns the team has developed (for example, the team has a standard pattern for client-side filtering components).

During this stage, the Spec Owner encounters one ambiguity: should the histogram show the full result set or the currently filtered set (after other filters are applied)? This triggers a **Decision Request** to the PM. The request format is:

> **Decision needed:** Should the price histogram reflect the full result set or the set after other active filters?
> **Options:** (A) Full set, simpler to implement, but histogram may not match visible results. (B) Filtered set, more complex, but histogram always matches what the customer sees.
> **Recommendation:** Option B. The histogram is misleading if it shows a distribution that does not match visible results.
> **Blocked:** Acceptance criterion #6 cannot be finalized without this decision.

The PM responds within 4 hours (the tactical decision SLA): Option B confirmed.

### Stage 3: Execution

The completed spec is handed off to the Reviewer in a **Spec Handoff** (10-15 minutes). The Spec Owner walks through the spec, highlights the architectural decision (client-side filtering), the accessibility requirements, and the performance constraint. The Reviewer confirms they understand the intent well enough to evaluate the output.

The spec then goes to execution. In a team using AI agents, this means the spec is provided to the coding agent (Claude Code, Cursor, Kiro, or whatever the team uses) as the implementation instruction. In a team without AI, a developer implements against the spec. In either case, the specification is the single source of truth for what gets built.

### Stage 4: Validation

The AI (or developer) produces a price filter component with tests. The Reviewer evaluates the output against the six acceptance criteria:

1. Does the slider initialize with the correct range? **Pass.**
2. Does filtering happen within 100ms? **Pass** (measured at 47ms for 500 items).
3. Does browser back button restore filter state? **Fail.** The component does not persist state to the URL. The Reviewer catches this because acceptance criterion #3 is explicit.
4. Performance under 100ms for 500 items? **Pass.**
5. Screen reader announces filter changes? **Fail.** The implementation updates the aria-live region but uses "polite" instead of "assertive," causing announcements to be delayed or skipped during rapid slider adjustment.
6. Histogram reflects filtered set? **Pass.**

Two criteria failed. The Reviewer does not fix the code. The Reviewer sends the spec back to the Specification stage with a note: "Criteria #3 and #5 not met. #3 needs URL state persistence. #5 needs aria-live assertive mode or debounced announcements."

The Spec Owner reviews whether the spec was ambiguous (it was not, the criteria were clear), adds a note to the team's spec patterns about explicitly specifying URL state persistence for any filter component, and sends the spec back to Execution with the specific failures noted.

The second pass produces output that passes all six criteria. The spec moves to Integration.

### Stage 5: Integration

The validated component merges into the main branch. The specification is archived in the team's spec repository as a permanent record of the design decisions (why client-side filtering was chosen, what the accessibility requirements are, what the performance thresholds are). Future specs that touch the search results page can reference SEARCH-042 for context.

This entire cycle, from intent to integration, took three days. Under Scrum, the same feature would have been a story estimated at 5-8 points, discussed in sprint planning, potentially deprioritized and carried over to a second sprint, and delivered with implicit assumptions about accessibility and performance that might or might not match what the PM intended.

## How This Looks in the Weekly Ceremonies

At the **Integration Review**, the team examines SEARCH-042 alongside other specs that shipped that week. They note that the first execution pass failed two criteria, which is normal and healthy. The spec quality was good (the criteria caught real issues). The AI execution was correct on four of six criteria on the first pass. The team's first-pass success rate for the week was 71%, within the target range.

At the **Spec Retrospective**, the team discusses the URL state persistence issue. This is not the first time a client-side component spec has missed browser navigation state management. They add a new item to their spec pattern library: "Any component that modifies the visible result set must specify behavior on browser back/forward navigation." This pattern prevents the same failure from recurring in future specs.

## The Spec Is Not the Code

One critical distinction: the specification is not pseudocode. It does not describe implementation steps. It describes what the output must do and the constraints it must satisfy. The "how" is left to the implementer (human or AI), except where architectural decisions are made explicitly (like the choice of client-side versus server-side filtering).

This is what makes specs reusable. If the team later decides to rewrite the component in a different framework, the specification still applies. If AI models improve and can produce better implementations, the specification still applies. The spec captures intent, constraints, and criteria. The code is one possible expression of those, and a disposable one.

## Spec-Driven Development Without AI

Everything in this example works identically if the Execution stage is handled by a human developer instead of an AI agent. The developer receives the same specification, implements against the same criteria, and the Reviewer validates against the same acceptance tests.

The difference is speed: a human developer might take two days for the implementation where an AI agent takes two hours. But the coordination model, the roles, the ceremonies, and the quality outcomes are the same. This is why Dandori works for teams at any point on the AI adoption spectrum. The framework coordinates around specifications, not around who or what writes the code.
