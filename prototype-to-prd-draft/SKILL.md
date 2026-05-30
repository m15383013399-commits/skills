---
name: prototype-to-prd-draft
description: Draft implementation-ready PRDs, interaction specs, or prototype explanations from project materials after a clarification pass has already been completed. Use when Codex should read AGENTS.md, the project brief, prototype artifacts, and especially a handoff file named prototype-prd-handoff.md produced by the clarification step, then convert those confirmed rules into a final development-facing document without redoing the whole discovery process.
---

# Prototype To PRD Draft

Use this skill after the clarification step has been completed.

This skill assumes the project already has a handoff file:

`prototype-prd-handoff.md`

If the file is missing, prefer asking the user to run `$prototype-to-prd-clarify` first instead of rebuilding the whole clarification process inside this step.

## Required Inputs

Read inputs in this order:
- `AGENTS.md` or the project writing contract
- `prototype-prd-handoff.md`
- project brief or prototype explanation
- prototype artifacts such as wireframes, screenshots, and page flows

Treat the handoff file as the first business interpretation layer.
Treat the prototype and project notes as the base evidence layer.
If the handoff file conflicts with the source materials, ask a focused follow-up question before drafting.

## Source Priority

Use this priority order when drafting:
1. User answers captured in the clarification conversation or `prototype-prd-handoff.md`.
2. `AGENTS.md` or project writing contract.
3. Confirmed handoff conclusions.
4. Project brief or business notes.
5. Prototype artifacts.

If the prototype conflicts with clarified user answers, follow the user answers.
Treat the prototype as visual evidence for page structure and controls, not as the final business rule source.
Do not move an answered item back to `待确认` because the prototype does not show the detail.
Only keep `待确认` for issues that remain unanswered after checking the clarification answers and handoff file.

## Workflow

1. Lock the output contract first.
- Follow `AGENTS.md` if it exists.
- If no project structure exists, use [references/default-structure.md](references/default-structure.md).

2. Read the handoff file before drafting.
- Extract confirmed rules.
- Extract open questions.
- Extract items marked `本期不做`, `待确认`, `暂不支持`, or `不展示`.
- Extract the page map and key flow decisions.

3. Cross-check the handoff against source materials.
- Verify the page map.
- Verify the critical interactions.
- Verify the major dependencies and state changes.
- If a blocking contradiction remains, ask a narrow follow-up question.

4. Draft the document page by page.
- Write page structure first.
- Then write interactions by following `用户操作 -> 系统反馈 -> 状态变化`.
- Then fill fields, rules, states, exceptions, and boundaries.
- Carry unresolved items forward exactly as `待确认` or related markers.

5. Deepen the implementation layer.
- Make default values explicit.
- Make editable scope explicit.
- Make validation and dependency rules explicit.
- Clarify what affects only the current action and what affects historical data or other pages.
- Separate front-end behavior from back-end judgment when the boundary matters.

6. Run the final gap scan.
- Use [references/checklist.md](references/checklist.md).
- Replace abstract ability language with concrete product behavior.
- Remove unsupported assumptions.

## Working Rules

1. Prefer the handoff file over memory of earlier chat.
2. Do not silently override clarified conclusions.
3. Do not drop `待确认` items just to make the document look complete.
4. Ask follow-up questions only when a remaining contradiction blocks drafting.
5. Keep the final document implementation-facing, not presentation-facing.

## References

Read these files as needed:
- [references/workflow.md](references/workflow.md)
- [references/handoff-contract.md](references/handoff-contract.md)
- [references/default-structure.md](references/default-structure.md)
- [references/checklist.md](references/checklist.md)

## Default Invocation

```text
Use $prototype-to-prd-draft. Read AGENTS.md first, then read prototype-prd-handoff.md, then re-check the project brief and prototype artifacts. If the handoff is sufficient, draft the final implementation-ready PRD. If a blocking contradiction remains, ask only the minimal follow-up questions needed to finish the draft.
```
