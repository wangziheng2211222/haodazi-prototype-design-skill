# Review Checklist

Use this before final delivery or when asked to review a generated prototype.

## Requirement Coverage

- Every explicit requirement is mapped to a page, flow, state, or open issue.
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

## Visual Coherence

- Screenshots or Figma evidence influence layout density, typography, color, radius, spacing, and component patterns.
- The result avoids falling back to a generic blue-white admin template when a stronger visual reference exists.
- Components share one design language across pages.
- Page titles, table density, form rhythm, and button hierarchy stay consistent.
- Text does not overflow buttons, tables, cards, sidebars, or navigation.

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
- Validation commands or visual checks are reported honestly.
