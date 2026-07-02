# Product Design Systems

Load this reference when a task names a known product family, asks to follow a design规范/design system, or lacks screenshots/Figma but expects product-native styling.

## Selection Rules

1. Prefer explicit Figma or screenshot evidence for the exact target screen.
2. Use the product design system for missing tokens, component behavior, layout density, and fallback styling.
3. Keep PRD and requirement text as the business-logic source of truth.
4. Record which design system was used in `design-tokens.json` or the final notes.
5. If a fallback design system is used, say so clearly in assumptions or delivery notes.

## Known Products

| Product hint | Design system reference | Rule |
| --- | --- | --- |
| 蝉圈圈 / Chanquanquan | `references/chanquanquan-design-system.md` | Load directly. |
| 蝉妈妈 / Chanmama | `references/chanquanquan-design-system.md` until a dedicated Chanmama reference exists | Use as temporary fallback and label it as fallback. |
| 蝉镜 / Chanjing | Future product-specific reference | If no dedicated reference exists, ask for screenshots/Figma or use neutral Haodazi defaults. Do not silently use 蝉圈圈 unless the user asks. |

## Output Requirements

When using a product design system, include:

- `designSystem.product`: product family inferred or provided by the user.
- `designSystem.reference`: reference file or source used.
- `designSystem.isFallback`: boolean.
- `designSystem.fallbackReason`: short reason when fallback is true.
- Design tokens derived from the loaded reference.

## Conflict Rules

- Figma target frame overrides product design-system defaults for that frame.
- Screenshot visual evidence overrides generic defaults but not Figma node evidence.
- Product design system overrides generic Element Plus styling.
- Requirement logic overrides visual references when business rules conflict with visuals.
