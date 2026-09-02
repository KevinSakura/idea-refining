---
name: idea-refining
description: Refine ambiguous, open-ended, preference-dependent, or high-branching requests by asking only decision-changing questions before the host agent answers or acts. Use for broad requests to plan, design, write, recommend, or build when missing goals, audience, deliverables, scope, constraints, quality bars, or success criteria could materially change the result. Do not trigger for simple facts, fully specified work, straightforward transformations, or requests that explicitly ask for no clarification.
---

# Idea Refining

Narrow a broad request into the minimum sufficient specification for reliable delivery. The objective is not to ask many questions. Ask the fewest questions that materially define the outcome, boundaries, execution path, quality bar, or acceptance criteria.

## Core invariant

Before asking any question, identify the downstream decision its answer will change. Do not ask the question if no material consequence can be named.

Never pad a round, repeat a semantic question, ask for information already available in the conversation or supplied materials, or collect details that the host agent can safely decide during execution.

## Workflow

1. Inspect the full conversation and any accessible files, images, links, or specifications before asking the user to repeat information.
2. Compress the current request internally into a one-sentence task definition.
3. Decide whether refinement is necessary:
   - Refine when missing preferences, goals, audience, deliverables, boundaries, constraints, quality requirements, or success criteria could materially change the result.
   - Do not refine simple factual questions, straightforward transformations, sufficiently specified tasks, or requests that explicitly ask for a direct answer.
   - If explicitly invoked for an already sufficient request, ask nothing and prepare the execution context.
4. For a request that needs refinement, read [references/interview-engine.md](references/interview-engine.md) before asking questions.
5. Maintain the interview state in the current conversation. Do not create a separate state file unless the user requests one.
6. Normally ask 3-5 related, high-value questions per round. Ask fewer when fewer questions pass the value gate.
7. After every user response, replace superseded conclusions, update the one-sentence task definition, reassess the unresolved risks, and stop as soon as the request is sufficiently bounded.
8. Before producing the handoff, read [references/output-contract.md](references/output-contract.md).
9. Deliver the refined result and wait for explicit approval before execution, except when the user says "answer directly" or an equivalent instruction.

## User controls

Interpret equivalent phrases in the user's language:

- **Answer directly:** stop interviewing, compress the current information and assumptions, and treat the instruction as approval for the host agent to continue the original task.
- **Skip:** leave the current item unresolved and continue only if it does not block the task.
- **Use the recommendation:** adopt the recommended option as an explicit assumption.
- **Go back and change:** replace the earlier answer and reassess affected decisions.
- **Restart:** discard the current interview state and begin a new refinement.
- **Create the plan but do not execute:** deliver the appropriate handoff and wait for approval.

## Boundaries

- This skill defines the task; it does not grant permission for unrelated actions.
- Follow the host platform's existing safety, permission, and approval rules.
- For medical, legal, financial, security, or other high-stakes work, clarify the request but state that completeness does not establish safety or correctness. Preserve needs for professional or authoritative verification in the handoff.
- Use the user's current language for questions and deliverables. Internal skill files are in English; do not produce bilingual output unless requested.
- Do not load [references/module-contract.md](references/module-contract.md) during ordinary interviews. Read it only when creating, reviewing, or combining future domain modules.
