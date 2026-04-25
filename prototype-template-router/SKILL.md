---
name: prototype-template-router
description: Route product prototype and Figma UI design requests to the best user-maintained Figma reference template, then design new screens in that template's style. Use when the user asks Codex to create, update, or plan a prototype from a product description; when the user says to reference Ant Design, Atlassian, Shopify Polaris, middle/back office systems, enterprise collaboration tools, ecommerce admin systems, or future template categories such as mobile apps and ecommerce storefronts; or when Codex needs to choose a design-system reference before writing screens to Figma.
---

# Prototype Template Router

## Core Idea

Use this skill to avoid designing from taste alone. First classify the requested product, then use the matching Figma template file as the style, structure, and component reference for the new prototype.

Keep the routing table extensible. Read `references/templates.md` before making a routing decision, because that file is the source of truth for available template libraries and their Figma URLs.

## Workflow

1. Read the user request and identify the product type, audience, primary workflows, and whether the user explicitly named a reference system.
2. Read `references/templates.md` and select exactly one primary template. Select a secondary template only when the product genuinely spans two domains.
3. If the user names a template keyword, honor it unless it obviously conflicts with the product goal. Explain the conflict briefly if choosing differently.
4. For Figma write work, use the Figma skills/tools already available in the environment. Load `figma-use` before every `use_figma` call, and use `figma-generate-design` when composing full screens.
5. Inspect the chosen template file lightly: list top-level pages/frames and locate the index or common components palette. Do not scan every component unless the task specifically requires deep component discovery.
6. Design the target screens using the selected template's layout rhythm, typography scale, density, navigation pattern, cards, tables, filters, forms, badges, and empty/error states.
7. Validate with Figma screenshots for representative screens. Fix text overflow, wrong font hierarchy, overlapping components, and charts/cards that spill out of their containers.
8. Return a short summary naming the selected template, the pages created or changed, and any verification performed.

## Routing Rules

Prefer explicit user intent over inference:

- If the user says "Ant Design", "中后台", "SaaS", "CRM", "管理系统", or "后台管理", choose the Ant Design middle/back office template.
- If the user says "Atlassian", "协作工具", "项目管理", "工单", "知识库", "团队协作", or "企业工具", choose the Atlassian collaboration template.
- If the user says "Shopify Polaris", "电商后台", "订单管理", "商品管理", "库存", "客户分群", or "营销后台", choose the Shopify Polaris ecommerce admin template.

When there is no explicit keyword, classify by the primary workflow:

- Operations, approvals, permissions, records, dashboards, CRUD tables -> Ant Design.
- Team collaboration, issues, docs, project boards, comments, activity timelines -> Atlassian.
- Merchant operations, orders, products, inventory, customers, discounts, channels -> Shopify Polaris.

If the request is for an ecommerce storefront, marketplace, mobile app, or another category not yet in the routing table, say that the current skill has no dedicated template for it and choose the closest temporary fallback only if the user still wants to proceed.

## Design Guidance

Use templates as reference systems, not as a pile of elements to copy blindly.

- Start from high-frequency page patterns already present in the chosen template.
- Reuse the template's common components palette for small controls and states.
- Keep B2B/admin screens dense, scannable, and restrained.
- Keep font hierarchy consistent with nearby template text. Do not enlarge row titles, table cells, labels, or badge text as if they were page headings.
- Keep cards at modest radii and avoid card-inside-card layouts unless the template already establishes that pattern.
- Include realistic domain data. Empty generic labels make the prototype harder to evaluate.
- For each new screen, include normal, empty, loading, error, permission, or disabled states when those states are important to the workflow.

## Extending the Skill

To add a new template category, edit only `references/templates.md`:

1. Add a new template entry with category, keywords, best use cases, Figma URL, and recommended pages/components.
2. Add a short routing note explaining when to prefer it over existing templates.
3. Keep the entry concise so future Codex sessions can route without consuming many tokens.

Do not embed large component inventories in `SKILL.md`. Put detailed notes in references and load them only when needed.
