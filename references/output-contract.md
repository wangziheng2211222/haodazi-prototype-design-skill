# Output Contract

Use these structures when a task needs explicit artifacts, traceability, or repeatable review output.

## Artifact Set

For a complete prototype-design task, produce as many of these as the user needs:

- `prototype.html` or repo-native page files: runnable high-fidelity review prototype.
- `page-map.json`: page IDs, page names, route labels, ownership, and review purpose.
- `review-notes.md`: assumptions, uncovered questions, coverage warnings, and suggested review agenda.
- `design-tokens.json`: colors, typography, radius, shadow, density, spacing, and component patterns inferred from screenshots or Figma.
- `delivery-notes.md`: implementation remarks for design and engineering follow-up.

For lightweight chat-only tasks, summarize these sections directly instead of writing files.

## Page Map Schema

```json
{
  "productName": "string",
  "reviewGoal": "string",
  "pages": [
    {
      "pageId": "overview",
      "name": "总览",
      "purpose": "Explain what the reviewer can validate here.",
      "routeLabel": "总览",
      "primaryObjects": ["object"],
      "states": ["default", "empty", "loading", "error"],
      "contains": ["table", "filters", "detail-drawer", "create-dialog"],
      "requirementsCovered": ["R1", "R2"]
    }
  ],
  "flows": [
    {
      "name": "主流程",
      "steps": ["overview", "list", "detail"],
      "successState": "string",
      "failureStates": ["string"]
    }
  ]
}
```

## Design Tokens Schema

```json
{
  "sourcePriority": ["requirements", "figma", "screenshots", "inference"],
  "styleSummary": "string",
  "colors": {
    "background": "#ffffff",
    "surface": "#ffffff",
    "text": "#111827",
    "mutedText": "#6b7280",
    "primary": "#2563eb",
    "border": "#e5e7eb",
    "danger": "#dc2626"
  },
  "typography": {
    "fontFamily": "system-ui",
    "pageTitle": "20px",
    "body": "14px",
    "caption": "12px"
  },
  "shape": {
    "radius": "8px",
    "shadow": "subtle",
    "borderWidth": "1px"
  },
  "density": {
    "table": "compact",
    "form": "comfortable",
    "navigation": "dense"
  },
  "componentPatterns": [
    "left-sidebar navigation",
    "filter toolbar above table",
    "detail drawer for row inspection"
  ],
  "avoidances": [
    "generic marketing hero",
    "decorative gradients without product evidence"
  ]
}
```

## Review Notes Structure

```markdown
# Review Notes

## Assumptions

- ...

## Requirement Coverage

| Requirement | Covered By | Notes |
| --- | --- | --- |
| ... | ... | ... |

## Issues For Review

| Priority | Page | Area | Issue | Suggested Fix |
| --- | --- | --- | --- | --- |
| P1 | ... | ... | ... | ... |

## Delivery Notes

- ...
```

## Standalone HTML Shell

When creating a standalone review prototype, use:

- A fixed or sticky left preview/content region.
- A right page-navigation panel with page list, states, assumptions, and review issues.
- Stable buttons/tabs for switching pages.
- No marketing landing page before the actual prototype.
- Responsive behavior that keeps navigation usable on narrow screens.

If the prototype includes generated Vue pages, embed them as distinct page modules or clearly separated code blocks. Keep the runtime boundary in `SKILL.md`.
