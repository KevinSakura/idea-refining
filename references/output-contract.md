# Output Contract

Read this reference when the interview is complete, the user stops it, or the user asks to answer directly.

The source-fidelity and quality checks apply to the actual deliverable during direct continuation as well as to a visible handoff. They are internal checks, not additional user-facing approval steps.

## Choose the execution route first

Do not use the visible handoff template until the execution route is known.

### Direct continuation

Continue the original task without another business-approval prompt when the request is sufficiently bounded and any of these apply:

- the requested result is ordinary text generation, read-only analysis, or a deterministic transformation;
- the user already asked the host to implement the feature or modify files within the defined scope;
- the user said "answer directly" or an equivalent instruction.

When the same host agent will execute immediately, keep the narrowed context internal unless the user requested a specification or reusable prompt. Do not display a large Agent Execution Context solely as a procedural preface. Host safety, sandbox, tool, and permission rules still apply and may require their own approval.

### Handoff or wait

Produce a visible handoff and wait only when:

- the user explicitly requested planning, a specification, or a prompt without execution;
- the next action needs authority not present in the original request, materially expands scope, or would create an unrequested external state change;
- the host platform requires a permission decision that the skill cannot make.

If authorization is needed, ask only for the specific missing authority. Do not ask the user to approve the already confirmed business requirements again.

### Incomplete

Use the forced incomplete handoff when an unknown-critical decision remains and cannot be handled by a disclosed, low-risk assumption. Do not execute.

## Global rules

- Write in the user's current language.
- Lead with one sharply bounded task statement.
- Include only current conclusions. Exclude superseded answers and chat history.
- Separate confirmed decisions, disclosed assumptions, and unresolved items.
- Match detail to the requested deliverable.
- Do not claim execution readiness when critical information is missing.

## Source fidelity

Treat these as protected source facts whenever they appear in the conversation or supplied material:

- numbers, quantities, ranges, units, dates, deadlines, prices, and version values;
- names, identifiers, field names, enum labels, ordered items, and text that must remain verbatim;
- statistical claims, including the measured concept, population, numerator or denominator when stated, timeframe, and uncertainty qualifiers;
- explicit inclusions, exclusions, priorities, and acceptance thresholds.

Maintain an internal trace from every confirmed decision to the user's words or an accessible source. A decision may enter **Confirmed** only when it is directly stated or explicitly accepted. Put interpretations, defaults, and useful extensions in **Assumptions** instead.

Preserve each protected fact's exact value, range direction, unit, label, ordering, and measurement meaning. Do not broaden `2-3` to `3-5`, turn an upper limit into a target, rename a source field, or infer a population-level interpretation from a bare satisfaction percentage. Do not introduce an unconfirmed count, range, deadline, metric, or source value inside Deliverable or Confirmed decisions. If execution needs a presentational default, choose the smallest sufficient default and disclose it as an assumption.

Do not omit source data that the receiving executor needs to complete the task. Preserve it directly or provide a reliable reference that the executor can actually access; otherwise mark the dependency as unresolved rather than inviting the executor to guess.

Distinguish expression from factual additions. Within the user's scope, wording, structure, and tone may be chosen freely; a new event theme, participation instruction, promise, historical detail, or operating procedure needs evidence or explicit creative authorization. A plausible addition is not a confirmed fact, and labeling it an assumption does not override a prohibition on invention. Preserve measurement meaning: a calendar period is not interchangeable with a rolling interval, and an item count does not establish a count of operations. For explicitly fictional or brainstorming tasks, create within that authorization without presenting inventions as real-world facts.

## Deliverable consistency

Carry the resolved deliverable type, execution depth, completion criteria, and required components consistently through the task definition, Deliverable, Acceptance criteria, and executor instructions. Do not substitute an outline for a finished article, sample code for requested integration, or an action for requested analysis. Present a partial result as partial, not as fulfillment of a different, easier task.

Trace these decisions to user instructions or accessible sources; identify allowed assumptions explicitly. If materially different deliverables remain unresolved, do not label the handoff ready for execution. When the user requests an answer without clarification, follow that control, disclose the chosen interpretation and material limits, and do not present it as a confirmed user decision. This does not grant new execution authority.

## Visible handoff completed within one or two rounds

When a visible handoff is required or requested, return only an agent execution context. Use this structure, omitting sections that are genuinely irrelevant:

~~~markdown
# Agent Execution Context

**Status:** Ready for execution

## One-point task definition
[A concise statement of what to produce, for whom, to what depth, and for what outcome.]

## Background and objective
[Relevant context and intended result.]

## Audience or users
[Who will use or receive the result.]

## Deliverable
[Resolved artifact, execution depth, required components, and format; distinguish allowed assumptions from confirmed requirements.]

## Scope
- Included: [...]
- Excluded: [...]

## Constraints and preferences
- [...]

## Confirmed decisions
- [...]

## Assumptions
- [...]

## Acceptance criteria
- [What counts as finished for this deliverable, with observable checks where applicable.]

## Instructions to the execution agent
[A direct instruction that uses the specification above and preserves the stated boundaries.]
~~~

After the context, follow the execution route already selected. Do not append a generic approval request. If the user requested planning without execution, state that execution was not requested; if specific new authority is required, ask only for that authority.

## Visible handoff completed after three or more rounds

Return two layers:

1. a human-readable specification;
2. a concise agent execution context.

Use this structure for the human-readable specification:

~~~markdown
# Refined Request

## Objective
[What the user is trying to achieve and why.]

## Users and context
[Audience, operating context, and relevant source material.]

## Deliverables
[What must be produced.]

## Scope and boundaries
[Included work, excluded work, and priorities.]

## Requirements
[Functional, content, quality, or operational requirements appropriate to the task.]

## Constraints and preferences
[Time, cost, technology, style, policy, resource, or other constraints.]

## Assumptions
[Only assumptions still in force.]

## Acceptance criteria
[Observable conditions for completion.]

## Risks or verification needs
[Only current risks, including high-stakes verification when applicable.]
~~~

Then provide the agent execution context using the shorter template above.

If the original request already authorized execution, the host may continue after presenting these two layers without asking the user to approve the requirements again.

## Answer-directly path

When the user says "answer directly" or an equivalent phrase:

1. stop asking questions;
2. use confirmed information and clearly disclosed assumptions;
3. prepare the narrowed context internally or visibly as appropriate;
4. let the host agent continue the original request without a skill-level approval prompt;
5. preserve all host safety and permission boundaries.

Do not force a large requirements document merely because the conversation was long if the user explicitly wants a direct answer.

## Forced incomplete handoff

Use this path at the final continuation limit or when the user stops while critical gaps remain.

~~~markdown
# Incomplete Request Definition

**Status:** Not ready for reliable execution
**Approximate completeness:** [band or approximate percentage]

## Current task definition
[Best current statement.]

## Confirmed information
- [...]

## Assumptions
- [...]

## Unresolved critical questions
- [Question and why it materially affects delivery.]

## Consequences of proceeding now
- [...]

## Recommended next step
[Ask the user to resolve the open questions before execution.]
~~~

State plainly that substantial information is missing. Do not append a normal execution-ready context. If a compact context would help future continuation, label it as a draft and explicitly say not to execute it.

## Quality check before sending

For direct continuation, compare the actual output with the resolved task: deliverable type and required components, protected facts, unsupported factual additions, and explicit format or length constraints. Repair observable mistakes before sending; do not ask the user to repeat information already supplied. Preserve instructions such as "output only the body" rather than appending a verification report.

For length constraints, use the stated counting unit and inclusion rules. Use an available local counter when precise verification is warranted; do not claim an exact count you have not checked. If an ordinary request leaves the counting convention unspecified, prefer a natural result with reasonable margin under common conventions rather than automatically asking another question. Clarify only when the convention materially changes strict acceptance and cannot be handled safely, subject to the no-clarification control. Do not invent facts to fill space or turn an approximate target into an unrequested hard range.

For a separate executor, carry the source facts and necessary acceptance checks into the handoff. If its final output is unavailable, do not claim that the downstream result was verified. These checks do not require additional review agents, fixed self-review loops, or a universal final approval.

For a visible handoff, apply the following relevant checks rather than imposing the full template on direct outputs.

Confirm that:

- the one-point task definition is narrower than the original request;
- every included requirement affects delivery;
- no requirement contradicts a later user decision;
- no open critical question is hidden as an assumption;
- acceptance criteria are observable where possible;
- deliverable type, execution depth, required components, and completion criteria agree across the handoff and have a source or an explicitly allowed assumption;
- changed upstream decisions have been reflected in affected downstream requirements without discarding still-valid facts;
- executable software requests include reliability concerns appropriate to their scope rather than only visual output;
- the handoff gives no authority beyond the user's request.
- every protected source fact has been compared against the conversation or supplied material for exact value, range, unit, spelling, ordering, qualifiers, and statistical meaning;
- every confirmed decision is traceable to a direct statement or explicit acceptance;
- no inferred extension has entered Deliverable, Constraints, Confirmed decisions, or Acceptance criteria as though the user supplied it;
- all execution-required source data is present or referenced through a location the receiving executor can access.
