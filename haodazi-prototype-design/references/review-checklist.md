# Review Checklist

Use this before final delivery or when asked to review a generated prototype.

## Requirement Coverage

- Every explicit requirement is mapped to a page, flow, state, or open issue.
- Every requirement card has a stable `requirementId`.
- Clicking or selecting a requirement card reveals a detail view tied back to original source text or a precise source pointer.
- Requirement details show parsed intent, acceptance criteria, impacted `pageId`s, impacted states, and coverage status.
- Business objects use consistent names across list, details, forms, and dialogs.
- Roles and permissions appear in UI states when the requirement mentions them.
- Required fields, optional fields, validation, and destructive actions are visible.
- Empty, loading, error, disabled, and permission-denied states are included where review value is high.

## Multi-Page Product Coherence

- Navigation reflects the product structure, not arbitrary page order.
- Primary actions appear in predictable locations.
- Detail views match list fields and status labels.
- Create/edit flows return to a clear destination.
- Approval, publishing, payment, or other state machines show next actions.
- Mock data stays realistic and internally consistent.
- The interaction blueprint covers primary flows, key branches, dialogs, drawers, confirmations, and return destinations.
- A generated change or repair does not mutate unrelated pages unless shared navigation, shared fields, or shared states require it.

## Visual Coherence

- Screenshots or Figma evidence influence layout density, typography, color, radius, spacing, and component patterns.
- Product-specific design systems are loaded when product names such as 蝉圈圈, 蝉妈妈, or 蝉镜 are present.
- 蝉圈圈 output follows coral-orange primary actions, pale gray workbench background, white surfaces, compact tables/forms, PingFang/system typography, and light borders.
- 蝉妈妈 output may temporarily use 蝉圈圈 design rules only when no 蝉妈妈-specific reference exists, and the fallback is disclosed.
- The result avoids falling back to a generic blue-white admin template when a stronger visual reference exists.
- Components share one design language across pages.
- Page titles, table density, form rhythm, and button hierarchy stay consistent.
- Text does not overflow buttons, tables, cards, sidebars, or navigation.
- Multi-screenshot tasks identify the primary reference, auxiliary references, and conflicts.
- Figma tasks prefer frame/node tokens, Auto Layout, asset manifest, and frame screenshots over screenshot-only inference.
- If Figma is the baseline, Element Plus components must not override the Figma layout, spacing, color, or component position.

## Generated Runtime

- Generated prototype pages use Vue 3 + Element Plus + Tailwind CDN when runnable code is needed.
- Code uses `// ---TEMPLATE---` and `// ---SCRIPT---` separators.
- Vue APIs use the global `Vue` object.
- Feedback uses `ElMessage`; confirmations use `ElMessageBox.confirm`.
- Code avoids React, JSX, shadcn, `className`, `function App()`, and `useState`.

## Review Output

- Remaining ambiguity is called out as an assumption or issue, not silently filled in.
- Review issues are tied to page, area, component, field, state, or interaction.
- Delivery notes say what design or engineering can reuse next.
- Delivery assets include component inventory, state enums, API assumptions, risks, and Figma redraw notes when the user asks for handoff value.
- Repair history records feedback classification, affected page IDs, changed artifacts, and reason.
- Validation commands or visual checks are reported honestly.
