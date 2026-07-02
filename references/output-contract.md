# Output Contract

Use these structures when a task needs explicit artifacts, traceability, or repeatable review output.

## Artifact Set

For a complete prototype-design task, produce as many of these as the user needs:

- `prototype.html` or repo-native page files: runnable high-fidelity review prototype.
- `page-map.json`: page IDs, page names, route labels, ownership, and review purpose.
- `requirements-map.json`: requirement cards, source pointers, parsed intent, and generated coverage.
- `review-notes.md`: assumptions, uncovered questions, coverage warnings, and suggested review agenda.
- `design-tokens.json`: colors, typography, radius, shadow, density, spacing, and component patterns inferred from screenshots or Figma.
- `design-system-used.md`: product design system, fallback status, and deviations.
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

## Requirements Map Schema

```json
{
  "sourceDocuments": [
    {
      "sourceId": "prd-main",
      "title": "需求文档",
      "type": "prd|notes|figma|screenshot|user-message",
      "sourcePointer": "file, URL, section, page, or message reference"
    }
  ],
  "requirementCards": [
    {
      "requirementId": "REQ-001",
      "title": "需求卡标题",
      "summary": "One-sentence parsed requirement.",
      "sourceId": "prd-main",
      "sourcePointer": "Section 2.1 / page 3 / paragraph 4",
      "sourceExcerpt": "Short excerpt or source cue.",
      "parsedIntent": "What the product must support.",
      "acceptanceCriteria": ["Reviewer can verify this condition."],
      "impactedPageIds": ["lead-workbench"],
      "impactedStates": ["empty", "error", "permission-denied"],
      "openQuestions": ["Question if any."],
      "coverageStatus": "covered|partial|open"
    }
  ]
}
```

## Design Tokens Schema

```json
{
  "sourcePriority": ["requirements", "figma", "screenshots", "inference"],
  "designSystem": {
    "product": "蝉圈圈",
    "reference": "references/chanquanquan-design-system.md",
    "isFallback": false,
    "fallbackReason": ""
  },
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
- A right page-navigation panel with page list, requirement cards, states, assumptions, and review issues.
- A requirement-card detail view: clicking a requirement card shows source pointer, source excerpt, parsed intent, acceptance criteria, impacted pages/states, and coverage status.
- Stable buttons/tabs for switching pages.
- No marketing landing page before the actual prototype.
- Responsive behavior that keeps navigation usable on narrow screens.

If the prototype includes generated Vue pages, embed them as distinct page modules or clearly separated code blocks. Keep the runtime boundary in `SKILL.md`.
