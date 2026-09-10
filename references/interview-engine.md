# Interview Engine

Use this reference whenever a request needs refinement.

## Desired outcome

Produce a minimum sufficient specification: the smallest set of confirmed decisions and explicit assumptions that lets the host agent deliver the requested outcome reliably.

Completeness is subordinate to question quality. A shorter interview with decision-changing questions is better than a comprehensive checklist filled with low-value details.

## Maintain an internal decision ledger

Track these categories in the conversation context without exposing a verbose ledger:

- **Confirmed:** explicitly provided or accepted by the user.
- **Inferred:** supported by supplied material but not yet confirmed.
- **Assumed:** a proposed default the user has accepted, or a low-risk default that will be disclosed.
- **Unknown-critical:** unresolved information that can materially change the outcome or make delivery unreliable.
- **Superseded:** earlier conclusions replaced by later user input. Never include these in the final output.

Also maintain:

- the current one-sentence task definition;
- the number of answered interview rounds;
- the number of continuation checkpoints reached;
- the current readiness state;
- the unresolved decision branches.

## General decision dimensions

Consider these dimensions, but never ask them mechanically:

1. intended outcome;
2. target user or audience;
3. relevant context and existing material;
4. requested deliverable;
5. included and excluded scope;
6. time, cost, technology, resource, or policy constraints;
7. preferences and priorities;
8. success criteria and unacceptable outcomes.

Classify relevant gaps as:

- **Critical:** delivery cannot be reliable without an answer or explicit assumption.
- **Important:** omission creates meaningful risk, rework, or a substantially different result.
- **Optional:** useful only if it clearly improves the result.

Classification is operational, not permanent. Promote an important gap to unknown-critical when it cannot be assumed safely and leaving it unresolved could materially change the solution category, scope, execution path, or acceptance criteria. Do not promote it merely because more detail would be useful.

## Candidate-question value gate

Generate candidate questions internally, then keep a question only when it passes all applicable checks:

1. **Decision impact:** its answer can change scope, content, approach, quality, reliability, or acceptance.
2. **Actual gap:** the answer is not already known and cannot be reliably inferred.
3. **Non-duplication:** it is not semantically equivalent to an answered, pending, or same-round question.
4. **Current relevance:** its prerequisites are already satisfied; otherwise defer it.
5. **Risk reduction:** asking is more valuable than using a disclosed, low-risk default.
6. **Answerability:** the user can understand the decision, or the question can provide clear options.

Delete a candidate if its downstream consequence cannot be stated in one sentence.

Only promote a candidate into the next round when all of these are true:

- it represents an unknown-critical decision rather than an optional improvement;
- a disclosed, low-risk assumption would not resolve it reliably;
- leaving it unresolved could materially change the solution category, included or excluded scope, execution path, or acceptance criteria.

Do not use a numeric formula. Rank candidates qualitatively by:

- how many downstream decisions they unlock;
- how severely a wrong assumption would affect delivery;
- how much they narrow the task;
- whether they determine the appropriate depth of later questions.

## Prevent repetition

Before asking a question:

1. Reduce it to its semantic intent, such as "target audience," "deployment environment," or "desired emotional tone."
2. Compare that intent with confirmed, inferred, assumed, skipped, and already asked items.
3. Map the answer to individual decisions, not question numbers. A partial answer does not resolve every subitem. Ask only for the missing portion that still materially affects delivery; do not repeat answered parts. "I don't know" does not authorize invented facts: omit nonessential unknowns, use an authorized placeholder, or report a missing required dependency.
4. Merge overlapping candidates only when they form one natural decision cluster. Do not combine independent choices merely to reduce the visible question count.
5. Do not restate an unanswered question unchanged. Explain why it blocks progress, offer options, or mark it unresolved.

Repeated wording is not the only duplication. Questions are duplicates when their answers drive the same decision.

## Match questions to delivery depth

First determine what the user wants delivered. Do not ask implementation questions for a concept-only request.

Treat deliverable type as an upstream decision. If two plausible interpretations would produce different artifacts, execution depths, or acceptance requirements and the available context does not resolve the difference, keep it unknown-critical. For example, an outline and a publishable article, a design and a working implementation, or an analysis and an external action are not interchangeable deliverables. When this distinction shapes the remaining questions, prioritize it in the first round instead of first collecting broad background. Independent critical questions may share that round; defer questions that depend on an unresolved interpretation.

Use explicit instructions and clear context without reconfirming them. Ambiguous verbs such as "plan," "make," or "organize" are cues to inspect context, not automatic triggers for a question. Do not turn a material choice into a low-risk assumption merely because one interpretation is easier to deliver. When the user explicitly asks for no clarification or accepts your choice, use the corresponding user-control path, disclose the choice, and preserve scope and permission limits.

Examples:

- For an article concept, determine purpose, audience, form, subject or conflict, setting or evidence, tone, length, and constraints only as relevant.
- For executable software, move from users and core flows to functional scope, data lifecycle, permissions, interfaces, failure handling, environment, testing, deployment, and acceptance. Ask these only when the user expects a working product rather than a visual shell or concept.
- For a recommendation, ask only preferences and constraints that would materially change the candidates.

Use dependencies. For example, do not ask database details until persistent data is actually in scope.

Ask only questions whose prerequisites are settled. Independent critical decisions may share a round within the existing cluster limit; a question that depends on another unanswered question belongs to a later round. Recompute the relevant branches after each answer without expanding into optional branches merely to exhaust the tree.

## Construct each round

A **decision cluster** is one coherent choice the user can answer as a unit and that selects or rules out a meaningful downstream branch. Closely coupled attributes may share a cluster when separating them would be artificial. Technology stack, data model, deployment, visual style, and unrelated feature choices are separate clusters unless the current task makes them genuinely interdependent.

At the start of a round, briefly show:

- **Current narrowed task:** a concise statement of the task as currently understood.
- **Approximate completeness:** a band or approximate percentage.
- **Round purpose:** the boundary or risk this round will resolve.

Then ask zero to three numbered decision clusters. There is no minimum. Rank eligible clusters by boundary gain and ask only the highest-value set. If no cluster passes the gate, ask nothing and move to the appropriate completion path.

For each question:

- state the specific decision it will settle and make clear what information would answer it; avoid open-ended requests for every aspect of the user's background;
- use 2-4 options when there are clear alternatives;
- say whether options are single-choice or multi-select;
- allow a free-form answer;
- mark a recommendation only when the user lacks a sound basis for choosing;
- explain the recommendation's effect and scope cost briefly; do not default to a larger bundle such as both a plan and a finished deliverable without a reason grounded in the user's goal.

Keep the round easy to answer. Do not bury questions in long explanations.

## Completeness and readiness

Use these approximate bands:

- **0-30%:** the outcome is still vague.
- **31-60%:** the direction is known, but major branches remain.
- **61-80%:** the main decisions are formed.
- **81-94%:** only a few high-value gaps remain.
- **95-100%:** the task is sufficiently bounded for reliable delivery.

These values are qualitative. Never imply a mathematical measurement.

Completeness is informational only. Never ask another question solely to raise the displayed band or percentage.

Stop when:

- all critical items are confirmed or explicitly assumed;
- important items are answered or safely disclosed as assumptions;
- no unknown is likely to materially change the plan;
- execution risk is proportionate to the requested deliverable.

Stop early even after one question if these conditions are met.

## Mandatory post-answer stop check

After every user response, perform this check before drafting another round:

1. Update confirmed, inferred, assumed, unknown-critical, and superseded items from what the user actually answered. Retain unresolved necessary subitems; do not mark an entire question complete merely because it received a reply. The user's no-clarification controls still apply.
2. Before counting remaining unknown-critical decisions, check that the intended artifact, execution depth, and what counts as finished follow from the user's instructions, accessible sources, or an allowed, disclosed assumption. Include required components and quality constraints only where they materially affect acceptance. If materially different deliverables remain plausible, keep the difference unknown-critical rather than clearing it by selecting one yourself.
3. Reassess downstream decisions affected by any changed upstream answer. Preserve unaffected facts and do not ask for them again.
4. For each remaining critical item, compare another question with a clearly disclosed, low-risk assumption. Prefer the assumption only when it will not materially change the solution category, scope, execution path, or acceptance criteria. Explicit answer-directly or no-clarification instructions end the interview through the corresponding control path, not by pretending that unresolved facts were confirmed.
5. If no critical item remains, stop immediately. Otherwise ask only the highest-value unresolved critical clusters whose prerequisites are settled and that cannot be assumed safely.

When stopping with non-critical gaps, disclose only the assumptions that matter to execution. Do not turn skipped optional details into hidden requirements.

This is an internal consistency check, not a fixed questionnaire or a request for universal final approval. A detailed audience description or a rich source brief does not compensate for an unresolved deliverable type.

## Round limits and continuation

- Ordinary requests should usually complete within one or two answered rounds.
- After five answered rounds, if critical gaps remain, offer: continue, adopt recommended assumptions and deliver, or stop.
- If the user continues, ask at most two further rounds before another checkpoint.
- Use checkpoints after rounds 5, 7, and 9 at most.
- At the round-9 checkpoint, do not begin another interview block. Force an incomplete handoff.

At a forced stop:

- state that substantial information is still missing;
- list the unresolved critical questions;
- distinguish confirmed information, assumptions, and unknowns;
- do not label the result execution-ready;
- recommend that the user resolve the open questions before proceeding.

## Changes, contradictions, and scope drift

- Use the user's latest explicit answer as current truth.
- For a material contradiction, identify the conflicting decisions and ask for confirmation rather than silently choosing.
- When new scope changes the task substantially, update the one-sentence task definition and reassess earlier decisions.
- When an upstream choice changes, reopen only the dependent assumptions or requirements that may no longer apply. For example, changing a design request into implementation may make the runnable environment and verification relevant; it does not erase an unchanged audience or supplied source facts.
- Do not include a history of discarded answers in the final output.

## Source material

Use accessible files, images, links, and specifications before questioning.

- Treat direct statements in the material as evidence.
- Mark interpretations as inferred until confirmed when they materially affect the result.
- If a source cannot be accessed, say so and ask for the relevant content.
- Never ask the user to repeat information that is already clear in the material.

## High-stakes requests

Run the same refinement process, but do not present completeness as professional validation. Preserve unresolved factual verification, professional review, authoritative sourcing, safety, and permission requirements in the final handoff.
