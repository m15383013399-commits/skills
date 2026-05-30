---
name: prototype-to-prd
description: Convert wireframes, page flows, screenshots, and prototype notes into implementation-ready PRDs, interaction specs, or prototype explanations. Use when Codex needs to write or rewrite internal development documents from prototype artifacts, especially when the project already defines writing constraints in AGENTS.md or a project brief, and Codex should first interrogate ambiguous interactions, button logic, state transitions, dependencies, and business flow through dialogue before drafting any document.
---

# Prototype To PRD

Use this skill to turn prototype artifacts into development-ready requirement documents.

Treat project-specific materials as the source of truth:
- Read `AGENTS.md` or user-provided writing constraints first.
- Read the project brief or prototype explanation next.
- Read prototype artifacts after the contract and facts are clear.

Use this skill as the generic method layer:
- `AGENTS.md` defines format, tone, numbering, and project writing constraints.
- Project notes define business facts, scope, and known rules.
- This skill defines how to extract implementation details from prototype artifacts.

## Workflow

1. Lock the output contract first.
- If `AGENTS.md` or a project style guide exists, follow it.
- If the project does not define a structure, use the default page structure in [references/default-structure.md](references/default-structure.md).
- Do not start drafting before the structure and tone are fixed.

2. Build a complete page map before drafting the document body.
- List all pages, popups, drawers, selectors, tabs, detail pages, and empty states.
- Split pages with different logic into separate sections even if the visual shell is similar.
- Record page entry, exit, save return path, and refresh target.

3. Enter clarification mode before drafting.
- Do not draft the PRD immediately after reading the materials.
- First simulate the core flows, alternate flows, and likely failure paths from the prototype.
- Collect contradictions, missing rules, uncertain assumptions, and blocked transitions.
- Ask the user focused question batches by using the framework in [references/question-framework.md](references/question-framework.md).
- Keep looping until the blocking questions are resolved or explicitly marked as `待确认`.

4. Draft page by page after the clarification gate passes.
- Write page structure first.
- Then write interactions by following `user action -> system feedback -> state change`.
- Then fill fields, rules, states, exceptions, and boundaries.
- Then write `本期不做 / 待确认` for anything unavailable or undecided.

5. Deepen implementation rules instead of repeating the prototype.
- For every button, switch, filter, tab, and popup, write what happens after the action.
- Make default values, editability, validation, dependencies, override behavior, and mutation scope explicit.
- Clarify whether a change affects only the current operation, current task, current entity, or historical data.
- Separate front-end behavior from back-end judgment when the boundary matters.

6. Run a gap scan before final output.
- Use [references/checklist.md](references/checklist.md) to check missing rules.
- Delete abstract capability language and replace it with concrete product behavior.
- Mark unknown rules as `待确认`, `本期不做`, `暂不支持`, or `不展示`.

## Working Rules

1. Do not invent business rules that are not present in the prototype or project materials.
2. Do not start drafting until the clarification loop has removed the blocking ambiguities.
3. Do not stop at page summaries; keep going until implementation rules are explicit enough for development and testing.
4. Prefer grouped question batches over one giant dump of questions.
5. After each user answer, re-run the flow mentally and check whether new contradictions appear.
6. Prefer one rule per line.
7. Keep sentences short.
8. When the prototype is visually clear but behavior is implicit, extract the likely implementation questions and either answer them from available materials or mark them as `待确认`.

## High-Risk Areas

Read [references/workflow.md](references/workflow.md) for the full end-to-end procedure.
Read [references/question-framework.md](references/question-framework.md) when preparing clarification questions.

Prioritize deeper extraction for:
- Batch actions
- Create/edit/delete flows
- Assignment or dispatch flows
- Import/export/upload/download
- Status transitions
- Filters and tree selectors
- Period or date range handling
- Historical data impact
- Front-end and back-end validation boundaries

## Default Invocation

Use a prompt like:

```text
Use $prototype-to-prd. Read AGENTS.md as the output contract, then read the project brief and prototype artifacts. Do not draft immediately. First question me about ambiguous interactions, button logic, dependencies, state transitions, and business flow. After the blocking questions are resolved, write an implementation-ready PRD. Do not invent missing business rules; mark them as 待确认 or 本期不做.
```
