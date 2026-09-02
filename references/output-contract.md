# Output Contract

Read this reference when the interview is complete, the user stops it, or the user asks to answer directly.

## Global rules

- Write in the user's current language.
- Lead with one sharply bounded task statement.
- Include only current conclusions. Exclude superseded answers and chat history.
- Separate confirmed decisions, disclosed assumptions, and unresolved items.
- Match detail to the requested deliverable.
- Do not claim execution readiness when critical information is missing.

## Completed within one or two rounds

Return only an agent execution context. Use this structure, omitting sections that are genuinely irrelevant:

~~~markdown
# Agent Execution Context

**Status:** Ready for user approval

## One-point task definition
[A concise statement of what to produce, for whom, to what depth, and for what outcome.]

## Background and objective
[Relevant context and intended result.]

## Audience or users
[Who will use or receive the result.]

## Deliverable
[Exact expected output and format.]

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
- [...]

## Instructions to the execution agent
[A direct instruction that uses the specification above and preserves the stated boundaries.]
~~~

Ask the user to approve execution after the context, unless the user already said "answer directly" or an equivalent instruction.

## Completed after three or more rounds

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

## Answer-directly path

When the user says "answer directly" or an equivalent phrase:

1. stop asking questions;
2. use confirmed information and clearly disclosed assumptions;
3. prepare the narrowed context internally or visibly as appropriate;
4. let the host agent continue the original request without another approval prompt;
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

Confirm that:

- the one-point task definition is narrower than the original request;
- every included requirement affects delivery;
- no requirement contradicts a later user decision;
- no open critical question is hidden as an assumption;
- acceptance criteria are observable where possible;
- executable software requests include reliability concerns appropriate to their scope rather than only visual output;
- the handoff gives no authority beyond the user's request.

