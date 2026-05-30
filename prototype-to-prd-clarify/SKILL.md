---
name: prototype-to-prd-clarify
description: Read AGENTS.md, project briefs, prototype notes, wireframes, screenshots, and page flows, then interrogate ambiguous interactions through dialogue before any PRD drafting starts. Use when Codex should simulate user flows, button logic, state transitions, dependencies, business process, front-end and back-end boundaries, and unresolved edge cases, ask focused question batches, and finally write a stable handoff file named prototype-prd-handoff.md for a later drafting step.
---

# Prototype To PRD Clarify

Use this skill before writing the PRD.

This skill does not draft the final document.
It does three things:
- read the project contract and source materials
- question the user until the blocking ambiguities are reduced
- write a handoff file for the drafting skill

## Required Inputs

Read inputs in this order:
- `AGENTS.md` or the project writing contract
- project brief, prototype explanation, or business notes
- prototype artifacts such as wireframes, screenshots, page flows, or interaction maps

## Output Contract

Always write the handoff file to the project root unless the user specifies another path:

`prototype-prd-handoff.md`

Use the fixed structure in [references/handoff-template.md](references/handoff-template.md).

The handoff file is the source of truth for the later drafting step.
Do not leave key conclusions only in chat when they should be in the handoff file.

## Source Priority

Use this priority order when source materials differ:
1. User answers during clarification.
2. `AGENTS.md` or project writing contract.
3. Existing handoff conclusions, if any.
4. Project brief or business notes.
5. Prototype artifacts.

If the prototype conflicts with a user answer, treat the user answer as confirmed and record the prototype point as a correction or implementation note.
Do not mark a question as `待确认` after the user has already answered it.
Use prototype artifacts to discover pages, fields, visual structure, and missing interaction entries, not to override clarified business rules.

## Workflow

1. Read the project contract first.
- Follow `AGENTS.md` if it exists.
- Extract numbering, tone, prohibited expressions, and document structure constraints.

2. Read the business facts next.
- Build a fact list from the project brief and prototype notes.
- Separate confirmed facts from assumptions.

3. Read the prototype artifacts last.
- Build a complete page map.
- Record page entry, exit, save return path, and refresh target.
- Split visually similar pages when logic differs.

4. Enter clarification mode.
- Simulate the main flow.
- Simulate alternate flows.
- Simulate failure paths.
- Write down blocked steps, contradictions, missing rules, and uncertain scope.
- Ask focused question batches by using [references/question-framework.md](references/question-framework.md).

5. Re-run the logic after each user answer.
- Check whether the main flow is now closed.
- Check whether button logic is now closed.
- Check whether dependencies and state transitions are now closed.
- Check whether historical impact and front-end/back-end boundaries are now closed.
- If new contradictions appear, ask another focused batch.

6. Stop only when the clarification gate passes.
- Stop when blocking issues are resolved.
- Anything still unknown but non-blocking should be written as `待确认`, `本期不做`, `暂不支持`, or `不展示`.

7. Write the handoff file.
- Use the fixed template.
- Write the conclusions, not the whole chat transcript.
- Make the handoff file readable without the original conversation.

## Working Rules

1. Do not draft the final PRD in this step.
2. Do not invent business rules that are not supported by the materials or the user's answers.
3. Prefer grouped question batches over one giant dump of questions.
4. Ask blocking questions first and optimization questions later.
5. After each answer, run the flow mentally again instead of mechanically asking the next preset question.
6. Mark unresolved but necessary items explicitly in the handoff file.

## References

Read these files as needed:
- [references/workflow.md](references/workflow.md)
- [references/question-framework.md](references/question-framework.md)
- [references/handoff-template.md](references/handoff-template.md)

## Default Invocation

```text
Use $prototype-to-prd-clarify. Read AGENTS.md first, then the project brief and prototype artifacts. Do not draft the PRD yet. First interrogate ambiguous interactions, button logic, state transitions, dependencies, business flow, and front-end/back-end boundaries through dialogue. When the blocking questions are resolved, write prototype-prd-handoff.md in the project root.
```
