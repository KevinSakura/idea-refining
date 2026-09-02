# Idea Refining

[中文说明](README.zh-CN.md)

Idea Refining is an instruction-only agent skill for Codex. It turns broad, ambiguous, preference-dependent requests into minimum sufficient specifications before the host agent answers or acts.

Its purpose is boundary definition, not exhaustive questioning. Every question must change a downstream decision about scope, content, implementation, reliability, quality, or acceptance. Redundant, inferable, premature, and low-impact questions are removed.

## What it does

- Detects when missing information can materially change the result.
- Narrows the task into a one-point definition.
- Asks normally 3-5 related, high-value questions per round, or fewer when fewer are justified.
- Explains what decision each question will settle.
- Offers understandable options when the user does not know how to answer.
- Uses supplied files, images, links, and specifications before asking for repeated information.
- Stops as soon as the request is sufficiently bounded.
- Produces an execution context for the host agent.
- Produces an additional human-readable specification for interviews lasting three or more rounds.

## What it does not do

- It does not interrogate simple factual questions.
- It does not force every request through a checklist.
- It does not execute the refined task without user approval, except when the user explicitly says to answer directly.
- It does not provide professional validation for high-stakes conclusions.
- Version 1 does not include domain-specific modules or scripts.

## How it works

The skill follows this cycle:

1. Inspect the conversation and supplied materials.
2. Compress the request into a one-sentence task definition.
3. Identify only the missing decisions that affect delivery.
4. Remove questions that are duplicate, inferable, premature, or safely defaultable.
5. Ask the highest-value questions and update the task boundary.
6. Stop when critical decisions are confirmed or explicitly assumed.
7. Produce a clean handoff without discarded answers or interview history.

Completeness is shown as an approximate range. It describes how well the request is specified, not whether the eventual answer is safe or correct.

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

Keep SKILL.md at the root of the copied idea-refining folder. Codex discovers skills from their name and description and can load the full instructions when the task matches.

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

- **Answer directly** to stop refinement and let the host agent continue.
- **Skip** to leave the current item unresolved.
- **Use the recommendation** to accept a proposed default.
- **Go back and change** to replace an earlier decision.
- **Restart** to begin the refinement again.
- **Create the plan but do not execute** to receive the handoff without starting work.

Equivalent phrases in other languages are supported.

## Output

If the request becomes ready within one or two rounds, the skill returns a concise agent execution context.

If the interview takes three or more rounds, it returns:

1. a human-readable refined specification;
2. a concise agent execution context.

If substantial critical information is still missing at the final continuation limit, it returns a document marked not ready for reliable execution and lists the unresolved questions.

## Examples of narrowing

Broad writing request:

~~~text
Write me an article.
~~~

Possible narrowed task:

~~~text
Write a 3,000-word realistic short story for high-school readers, set in a contemporary coastal town, about a student choosing between family expectations and a personal ambition. Keep the tone restrained but warm and end openly.
~~~

Broad software request:

~~~text
Build me a review website.
~~~

Possible narrowed task:

~~~text
Build a working website for students to review campus cafeterias and nearby restaurants. It must support location and cuisine browsing, multidimensional ratings, text reviews, image uploads, moderation, reliable persistence, error handling, tests, and local deployment instructions. The deliverable must complete the full review flow rather than only display static pages.
~~~

The exact questions depend on the requested delivery depth. A concept request should not be burdened with database or deployment questions; a production-ready software request must address reliability beyond visual appearance.

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
