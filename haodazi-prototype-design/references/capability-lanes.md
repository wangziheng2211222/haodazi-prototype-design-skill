# Capability Lanes

Use this reference to keep Haodazi prototype-design work organized by user-facing business capability, not by internal agent roles.

## Capability Routing

| Input or request | Capability lane | Primary output |
| --- | --- | --- |
| PRD, notes, product idea | Requirement-to-prototype | `page-map.json`, `requirements-map.json`, `interaction-blueprint.json`, high-fidelity pages |
| One or more screenshots | Screenshot style replication | `visual-dna.json`, `design-tokens.json`, visual QA notes |
| Figma file/frame | Figma restoration | `figma-restoration-context.json`, frame screenshots, asset manifest, visual QA notes |
| User feedback after generation | Review repair | `review-issues`, `repair-plan`, patched pages, `repair-history.json` |
| Design/dev/Figma handoff | Delivery assets | `component-inventory.json`, `implementation-notes.md`, `figma-redraw-brief.md` |

## Requirement-To-Prototype

Default lane. Use it for every full prototype task.

Internal outputs:

- `inputSummary`
- `pageMap`
- `pageIds`
- `moduleCoverage`
- `interactionBlueprint`
- `requirementsMap`
- `highFidelityPages`
- `coverageWarnings`

Rules:

- Generate complete high-fidelity pages after understanding the requirements.
- Keep module decomposition and `pageId` reasoning available, but do not force users to choose modules first.
- Bind list, details, create/edit dialogs, drawers, and local state variants to the same `pageId` when they are one review surface.
- Keep requirement cards connected to source text and generated coverage.

## Screenshot Style Replication

Use when screenshots, existing pages, product references, or visual examples are provided.

Outputs:

- `styleSummary`
- `visualDna`
- `designTokens`
- `componentPatterns`
- `layoutPatterns`
- `densityRules`
- `assetHints`
- `avoidances`
- `visualDiffs` when a generated preview can be compared

Rules:

- Treat screenshots as visual evidence by default; do not ask whether to reference or reuse them.
- With multiple screenshots, choose a primary reference, auxiliary references, and conflict notes.
- Extract layout density, navigation shape, hierarchy, component style, color, typography, radius, shadow, border, spacing, and state treatment.
- Do not fall back to generic blue-white admin UI when screenshots show a stronger visual language.
- If screenshot visuals conflict with requirements, keep business logic from requirements and visual language from screenshots.

## Figma Restoration

Use when the user provides a Figma link, specific frame, node ID, file key, Figma-exported context, or asks for Figma-style restoration.

Outputs:

- `figmaFileSummary`
- `targetFrames`
- `nodeTreeSummary`
- `autoLayoutRules`
- `figmaDesignTokens`
- `componentInstances`
- `assetManifest`
- `frameScreenshots`
- `figmaRestorationContext`
- `visualDiffs`

Rules:

- Prefer specific frame/node evidence over screenshot guesses and product design-system defaults.
- Parse Figma URL intent: file key, node ID, selected frame, and access constraints.
- If the file is large and no target frame is specified, ask the user to choose a target frame before trying to restore everything.
- Read or preserve Auto Layout, constraints, dimensions, colors, typography, radius, shadow, stroke, opacity, components, instances, and assets when available.
- Export or use target frame screenshots as visual QA baselines when possible.
- Do not approximate Figma 1:1 restoration by only doing screenshot style replication.
- Do not let Element Plus default styling override the Figma visual target; use Element Plus as runtime components while preserving layout and visual intent.

## Review Repair

Use after a high-fidelity result exists or when the user asks to revise a prototype.

Classify feedback first:

- Requirement gap: missing rule, page, role, field, flow, or state.
- Visual deviation: layout, color, typography, spacing, radius, shadow, component, or asset mismatch.
- Interaction issue: navigation, modal/drawer behavior, confirmation, feedback, disabled state, or form validation.
- Field/state issue: naming mismatch, enum mismatch, status transition, permission, empty/error/loading state.
- Missing page: new page or route needed.
- Delivery-asset request: user needs handoff material rather than page code changes.

Repair rules:

- Patch the smallest affected page, area, interaction, or token.
- Preserve unrelated pages and business logic.
- If the fix changes shared navigation, shared fields, or shared status enums, update affected pages consistently.
- Record `repairPlan`, `patchedPages`, and `repairHistory`.

## Delivery Assets

Use when the user needs design continuation, Figma redraw, development estimation, review materials, or handoff beyond the runnable prototype.

Outputs:

- Design style summary.
- Design tokens: colors, typography, spacing, radius, shadow, components, states, icons, assets.
- Component inventory: buttons, tables, cards, forms, dialogs, drawers, tags, navigation, charts, empty/error/loading states.
- Page structure and flows.
- Development notes: data objects, API assumptions, state enums, permissions, interaction notes, risks, and open questions.
- Figma redraw brief or intermediate node description for later Figma plugin/import work.

Rules:

- Delivery assets should be generated after the prototype unless the user only asks for planning.
- Keep delivery assets structured enough for design and engineering to reuse.
- Explain why major design choices were made, not only what code was generated.

## Visual QA

Use visual QA when screenshots/Figma are provided or when the user questions visual fidelity.

Outputs:

- `quality-report.json`
- `visual-diffs`
- optional similarity score if the user asks for visible scoring
- targeted repair suggestions

Rules:

- Compare against the most specific visual baseline: Figma frame first, then screenshot, then product design system.
- Check layout, hierarchy, color, typography, spacing, radius, shadow, component presence, asset presence, and density.
- Use scores internally when useful; show scores to users only when they ask or when it clarifies a quality gate.
