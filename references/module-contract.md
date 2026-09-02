# Future Domain Module Contract

Read this reference only when adding, reviewing, routing, or combining domain-specific modules. Version 1 of idea-refining has no domain module.

## Purpose

A domain module contributes specialized candidate questions and output requirements. It does not replace the core interview engine and must not force the user through a fixed questionnaire.

## Location and naming

Store future modules under:

~~~text
references/domains/
  software-development.md
  academic-writing.md
  recommendation.md
~~~

Use lowercase hyphenated filenames.

## Required sections

Each module must define:

1. **Scope:** tasks the module improves.
2. **Exclusions:** similar tasks that should not load it.
3. **Routing signals:** cues for primary or auxiliary use.
4. **Decision dimensions:** domain-specific critical, important, and optional information.
5. **Dependencies:** when a question becomes relevant and what prerequisite must be known first.
6. **Risk indicators:** missing information that can make delivery unreliable.
7. **Stage gates:** differences between concept, plan, prototype, production, publication, or other domain stages.
8. **Output additions:** sections or fields to add to the human specification or agent context.
9. **Examples:** a small number of examples that clarify non-obvious decisions.

## Module invariants

- Propose candidate questions; never mandate that every candidate be asked.
- Apply the core question-value gate and semantic deduplication.
- Do not repeat general dimensions unless the domain changes their meaning.
- Do not prescribe tools, technologies, methods, or styles without user need or a defensible default.
- Match questions to the requested delivery depth.
- Keep professional validation, safety, and permissions separate from information completeness.
- Do not alter the core stopping and continuation rules.

## Combining modules

For a cross-domain request:

1. choose one primary module based on the final deliverable;
2. load auxiliary modules only for material secondary concerns;
3. merge candidate questions by downstream decision;
4. remove semantic duplicates;
5. use one shared interview state and one final handoff.

Do not produce disconnected specifications unless the user explicitly asks for separate deliverables.

## Review checklist

Before accepting a new module, verify that:

- it adds domain knowledge that the general engine cannot reliably infer;
- its activation and exclusion boundaries are clear;
- its questions are conditional and consequence-driven;
- it does not inflate ordinary interviews;
- its output additions help an execution agent deliver a materially better result.
