# Idea Refining

[中文说明](README.zh-CN.md)

Idea Refining is an instruction-only agent skill for Codex. It turns broad, ambiguous, preference-dependent requests into minimum sufficient specifications before the host agent answers or acts.

Its purpose is boundary definition, not exhaustive questioning. Every question must change a downstream decision about scope, content, implementation, reliability, quality, or acceptance. Redundant, inferable, premature, and low-impact questions are removed.

Version 1.3 prioritizes consequential deliverable choices in the first round, tracks partially answered decisions, and checks actual outputs for source fidelity and explicit delivery constraints. It retains direct execution and no-clarification controls. Behavioral evaluation of v1.3 is pending.

## Quick start

1. Copy the complete `idea-refining` folder into a repository-scoped or user-scoped Codex skill location.
2. Start or restart Codex from the relevant repository.
3. Invoke the skill with a broad request:

~~~text
$idea-refining Help me define a website for reviewing food around my campus.
~~~

The skill may also activate automatically because implicit invocation is enabled in `agents/openai.yaml`.

## Main capabilities

- Detects when missing information can materially change the result.
- Narrows the task into a one-point definition.
- Asks zero to three highest-value decision clusters per round, with no minimum.
- Explains what decision each question will settle.
- Offers understandable options when the user does not know how to answer.
- Uses supplied files, images, links, and specifications before asking for repeated information.
- Runs a mandatory stop check after every answer and stops when no critical unknown remains.
- Preserves numbers, ranges, names, metrics, source values, and other protected constraints exactly.
- Produces a visible execution context only when a handoff or planning deliverable is needed.
- Produces an additional human-readable specification for interviews lasting three or more rounds.

## When to use it

Use Idea Refining when missing information could materially change the solution category, scope, execution path, quality bar, or acceptance criteria. Typical requests include:

- planning an article, story, report, product, or service;
- selecting a product when preferences or hard constraints are incomplete;
- defining a website, application, or software feature;
- turning an early idea into a requirements document or reusable execution prompt;
- narrowing any request with several plausible interpretations.

The skill is most useful when the request could otherwise produce a polished but misdirected result.

## What it does not do

- It does not interrogate simple factual questions.
- It does not force every request through a checklist.
- It does not impose a universal approval gate. It respects the authorization already present in the request and leaves protected actions to the host platform's permission system.
- It does not provide professional validation for high-stakes conclusions.
- Version 1 does not include domain-specific modules or scripts.

## How it works

The skill follows this cycle:

1. Inspect the conversation and supplied materials.
2. Compress the request into a one-sentence task definition.
3. Identify only the missing decisions that affect delivery.
4. Remove questions that are duplicate, inferable, premature, or safely defaultable.
5. Ask at most three highest-value decision clusters and update the task boundary.
6. After every answer, stop immediately when critical decisions are confirmed or safely and explicitly assumed.
7. Continue the original task, produce a requested handoff, or return an incomplete definition according to execution intent.
8. Before a handoff, verify source facts and prevent unconfirmed extensions from becoming requirements.

Completeness is shown as an approximate range. It describes how well the request is specified, not whether the eventual answer is safe or correct.

### Decision clusters

A decision cluster is one coherent choice that selects or rules out a meaningful downstream branch. Closely coupled details may be answered together, but independent topics must not be bundled merely to reduce the visible question count. Technology stack, data model, deployment environment, and visual style are normally separate clusters.

### Mandatory stop check

After every answer, the skill updates confirmed information, assumptions, superseded answers, and remaining critical unknowns. It stops immediately when no `unknown-critical` item remains. A disclosed low-risk assumption is preferred over another question when it will not materially change the result.

A material ambiguity such as outline versus finished article remains critical until resolved. Clear instructions are used without reconfirmation; no-clarification requests still end the interview with disclosed assumptions. When an upstream choice changes, only affected downstream decisions are reopened.

### Execution routing

Once the request is sufficiently bounded, the skill chooses among direct continuation, a visible handoff, and an incomplete definition. Ordinary text generation, read-only analysis, deterministic transformation, and implementation already authorized by the original request can continue without a second skill-level approval. Host safety and permission controls still apply.

## Install in Codex

Codex supports repository-scoped and user-scoped skills.

For one repository, copy this entire folder to:

~~~text
<repository>/.agents/skills/idea-refining/
~~~

For your user account, copy it to:

~~~text
$HOME/.agents/skills/idea-refining/
~~~

Copy the complete folder, including `SKILL.md`, `references/`, and `agents/`. Keep `SKILL.md` at the root of the copied `idea-refining` folder.

Codex scans repository `.agents/skills` locations from the current working directory toward the repository root. The user-scoped location makes the skill available across local projects. Codex discovers skills from their name and description and loads the full instructions when the task matches.

Codex detects new and updated skills automatically. Restart Codex if the skill does not appear.

See the official [Codex skill documentation](https://learn.chatgpt.com/docs/build-skills) for current discovery and installation details.

## Use

Explicit invocation:

~~~text
$idea-refining Help me define a website for reviewing food around my campus.
~~~

~~~text
$idea-refining I want to write an article, but I have not decided its form or focus.
~~~

Implicit invocation is enabled. Codex may select the skill automatically when a broad request is missing decisions that would materially affect the result.

The skill should not activate for a simple request such as:

~~~text
What is the weather today?
~~~

## User controls

You can say:

- **Answer directly** to stop refinement and let the host agent continue without a skill-level approval prompt.
- **Skip** to leave the current item unresolved.
- **Use the recommendation** to accept a proposed default.
- **Go back and change** to replace an earlier decision.
- **Restart** to begin the refinement again.
- **Create the plan but do not execute** to receive the handoff without starting work.

Equivalent phrases in other languages are supported.

## Source fidelity

Before sending an actual deliverable or visible handoff, the skill checks protected facts against the conversation and supplied materials. It preserves numbers, ranges, units, dates, names, identifiers, field names, ordered values, required wording, and statistical meaning.

It must not broaden `2–3` candidates into `3–5`, turn a budget ceiling into a target, rename source fields, reinterpret an unsupported percentage, or present an inferred extension as a confirmed requirement. Execution-required source data must be included directly or referenced through a location the receiving agent can access; otherwise the dependency remains unresolved rather than being guessed.

## Output

If the same host agent can continue an already authorized task, the skill keeps the narrowed context internal and proceeds without a ceremonial approval step.

If a visible handoff or planning deliverable is requested and the request becomes ready within one or two rounds, the skill returns a concise agent execution context.

If the interview takes three or more rounds, it returns:

1. a human-readable refined specification;
2. a concise agent execution context.

If substantial critical information is still missing at the final continuation limit, it returns a document marked not ready for reliable execution and lists the unresolved questions.

## Representative evaluation example

This example comes from evaluation case SW-01 and shows why boundary refinement matters.

Initial request:

~~~text
Design an appointment system for me.
~~~

Without refinement, the baseline interpreted this as a customer-facing service-booking platform for clinics, training, consulting, or beauty businesses. It introduced customers, service staff, schedules, reminders, APIs, databases, and reporting. The output was detailed, but it solved the wrong problem.

The refinement process identified the decisions that materially changed the task:

- **Scenario and users:** an internal meeting-room system for a company of about 70 people, used by employees and administrators.
- **Required deliverable:** product requirements and low-fidelity page and flow descriptions, not code or a clickable prototype.
- **Core outcome:** prevent overlapping room bookings while showing room capacity, equipment, and availability.
- **Permissions:** employees can book and cancel their own reservations; administrators can block maintenance periods and resolve conflicting reservations.
- **Boundaries:** company-email login; no attendee management, external calendar integration, off-site notifications, payment, visitor booking, or room-record administration.
- **Unresolved configuration:** time granularity, maximum duration, booking horizon, and late-cancellation limits remain explicit configuration items instead of invented defaults.

Refined task:

~~~text
Produce product requirements and low-fidelity page and flow descriptions for a responsive internal meeting-room booking system used by a company of about 70 people. Employees sign in with company email, view room capacity, equipment and availability, create bookings, and cancel their own bookings. Administrators can block maintenance periods and cancel reservations that conflict with maintenance. The system must prevent overlapping bookings for the same room and clearly define role permissions, conflict feedback, and major page states. Do not produce code or a clickable prototype, and do not add attendee management, external calendars, notifications, payments, visitor booking, or room-record administration. Leave unspecified booking limits as clearly marked configuration items.
~~~

The refined result matched the actual internal meeting-room use case, while the baseline had committed to an unrelated external service-booking product. The improvement came from resolving a small number of outcome-changing boundaries rather than collecting every possible product detail.

## Package structure

~~~text
idea-refining/
├── SKILL.md
├── README.md
├── README.zh-CN.md
├── agents/
│   └── openai.yaml
└── references/
    ├── interview-engine.md
    ├── output-contract.md
    └── module-contract.md
~~~
