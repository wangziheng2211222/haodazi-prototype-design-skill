---
name: haodazi-prototype-design
description: Use when Codex needs to follow the Haodazi prototype-design workflow to turn PRDs, requirement notes, screenshots, Figma context, or product ideas into a multi-page high-fidelity review prototype with page navigation, consistent product structure, Vue 3 + Element Plus generated pages, review issues, and delivery notes. Trigger for requests such as 原型设计模式, 好搭子原型, 需求生成原型, 高保真评审稿, screenshot style replication, Figma-to-review-prototype, pageId decomposition, or left-preview/right-navigation prototype output.
---

# Haodazi Prototype Design

## Purpose

Execute the Haodazi prototype-design workflow: turn product requirements and optional visual references into a complete, reviewable, multi-page high-fidelity prototype. Compete on workflow quality, not generic page generation.

Use this skill to produce a shared review object for product, design, and engineering: page map, clickable page navigation, high-fidelity pages, states, review issues, and delivery notes.

## Operating Principles

- Treat requirements as the source of business truth.
- Treat screenshots as visual language and component-pattern evidence.
- Treat Figma as an optional restoration or design-system evidence lane, not the default input.
- Generate a complete result first; do not stop at abstract module selection unless the user explicitly asks.
- Keep internal decomposition hidden by default, but preserve it in structured outputs.
- Build one coherent product, not isolated screens.
- Prefer precise reviewability over decorative UI.
- Ask at most one clarification question only when missing information would make the product category, platform, or core flow impossible to infer.

## Runtime Boundary

When generating runnable prototype code, use Vue 3 + Element Plus + Tailwind CDN. Do not use React, JSX, shadcn, `className`, or `useState` inside generated prototype pages.

For generated Vue pages:

- Separate code with `// ---TEMPLATE---` and `// ---SCRIPT---`.
- Access Vue through the global `Vue` object, such as `Vue.ref()` and `Vue.computed()`.
- Use Element Plus components such as `el-button`, `el-table`, `el-dialog`, `el-drawer`, `el-form`, `el-tabs`, and `el-empty`.
- Use `ElMessage` and `ElMessageBox.confirm` for feedback.
- Include realistic Chinese or domain-appropriate mock data. Avoid `Lorem ipsum`, `test`, `abc`, and emoji.

## Workflow

### 1. Intake

Collect and normalize available inputs:

- PRD, feature brief, meeting notes, pasted requirements, or product idea.
- Screenshots, existing pages, brand/style references, or product screenshots.
- Figma links, selected frames, node IDs, or exported design context.
- User constraints: target user, platform, must-have pages, output location, fidelity level, and review focus.

If the user provides only a vague idea, infer a compact but complete product scope and state assumptions before outputting artifacts.

### 2. Requirement Understanding

Extract:

- Product type and main users.
- Roles, permissions, business objects, fields, states, and rules.
- Core user flows and edge flows.
- Pages, dialogs, drawers, tables, forms, details, settings, and empty/error/loading states.
- Ambiguities, risks, and missing requirements.

Keep this step as internal reasoning unless the user asks to inspect it.

### 3. Page Map And `pageId` Decomposition

Create stable `pageId`s before writing pages. Bind a page's list, details, create/edit dialogs, drawers, filters, and local states to the same `pageId` when they are part of one review surface.

Default structure:

- Dashboard or overview when the product needs an entry point.
- Primary list/workbench page for the main business object.
- Detail page or detail drawer.
- Create/edit flow.
- Review/approval/status flow when relevant.
- Settings or rule-management page only when requirements imply it.

Do not create redundant pages just to inflate scope.

### 4. Visual Direction

If screenshots are provided, extract a visual DNA:

- Layout density, navigation structure, information hierarchy, and component families.
- Color palette, typography, radius, shadow, border, spacing, and data density.
- Primary interaction patterns and visible states.
- Style avoidances.

If Figma context is provided, prefer Figma node/layout/token evidence over screenshot guesses. If both exist and conflict, keep requirement logic from the PRD, detailed visual constraints from Figma, and broader style atmosphere from screenshots.

Read `references/output-contract.md` when you need exact artifact schemas. Read `references/review-checklist.md` before final QA or when the user asks for review issues.

### 5. High-Fidelity Generation

Generate all agreed or inferred `pageId`s in one coherent pass:

- Maintain shared navigation, naming, data fields, status labels, and primary actions.
- Include realistic mock data and visible state examples.
- Cover empty, loading, error, disabled, permission, validation, and destructive-action confirmation states where they matter.
- Make the left side a live/page preview target and the right side a page-navigation or scheme-navigation surface when creating an HTML review shell.
- Keep side navigation concise: pages, key states, issues, and delivery notes.

For repository work, follow the existing project stack and scripts. For standalone artifact work, prefer a self-contained HTML file that can open locally unless the user asks for a framework app.

### 6. Review And Repair

Before final delivery, check:

- Each requirement maps to at least one page, state, or review note.
- Main flows can be followed across pages.
- Status names, fields, and actions stay consistent.
- Dialogs, drawers, forms, tables, and details belong to the right `pageId`.
- Visual language is coherent across pages.
- Generated Vue code respects the runtime boundary.

If flaws are found, repair affected pages or record explicit review issues. Do not hide gaps by claiming they are complete.

### 7. Delivery

Return the prototype with:

- Where the user can open it.
- What pages were generated.
- What review issues or assumptions remain.
- What validation was run.

If the user asks for an artifact, create files instead of only describing the plan.

## Output Modes

Choose the smallest useful output:

- **Chat blueprint**: use for early brainstorming or product alignment.
- **Standalone review prototype**: use for quick artifact delivery outside a repo.
- **Repo-integrated prototype**: use when the user asks to modify an existing project.
- **Skill/plugin evolution notes**: use when improving this workflow itself.

Do not write product docs unless the user asks. In brainstorming, keep the answer in chat.
