# 蝉圈圈 Design System

Use this reference when the target product is 蝉圈圈. Use it as a temporary fallback for 蝉妈妈 only when no 蝉妈妈-specific design system is available, and label the fallback.

## Visual Theme

蝉圈圈 Web is a lightweight business-system and growth-analysis interface. Prefer a clean operational workbench: pale gray page frame, white content surfaces, low-contrast borders, clear text hierarchy, compact tables/forms, and coral-orange brand actions.

Avoid heavy marketing decoration, generic blue-white admin defaults, thick shadows, and arbitrary new colors.

## Core Tokens

| Role | Value | Use |
| --- | --- | --- |
| Primary | `#FF7752` | Main buttons, selected states, action focus, brand tags |
| Primary hover | `#FF9275` | Hover on primary actions |
| Primary pressed | `#E56B4A` | Active/click state |
| Primary disabled | `#FFD6CB` | Disabled primary button background |
| Primary subtle bg | `#FFF8F6` | Selected menu/card background, weak brand blocks |
| Primary pale bg | `#FFF1EE` | Pale brand background |
| Frame bg | `#F7F8FA` | Page frame, table header background |
| Subtle divider | `#F2F3F5` | Dividers, weak sections, tag background |
| Default border | `#E5E6EC` | Inputs, cards, table lines |
| Text primary | `#1D2129` | Titles and primary text |
| Text strong secondary | `#4E5969` | Body and subtitles |
| Text secondary | `#86909C` | Table headers, notes, helper text |
| Text disabled | `#A9AEB8` | Disabled text |
| White | `#FFFFFF` | Card surfaces and inverse text |

Functional colors:

| Role | Main | Light bg | Text |
| --- | --- | --- | --- |
| Info blue | `#5771FF` | `#F2F4FF` | `#344499` |
| Success green | `#00B489` | `#EBF9F6` | `#006C52` |
| Warning orange | `#FF9A1D` | `#FFF8E8` | `#A65508` |
| Danger red | `#F54B45` | `#FFEDE8` | `#A1171B` |
| Purple | `#722ED1` | `#F5E8FF` | `#3C108F` |
| Sky blue | `#027FFF` | `#EBF5FF` | `#014C99` |

Use fixed gradients only for metric-card highlight states. Use brand gradients only for brand-related menu icons, pale brand cards, or brand emphasis.

## Typography

- Font family: PingFang SC when available, then system sans-serif.
- Default body: 14px equivalent, Regular, about 22px line-height.
- Page title: 24px equivalent, Medium, about 36px line-height.
- Card title: 18px or 16px equivalent, Medium.
- Helper text: 12px equivalent, Regular.
- Very small tags: 10px only when space is constrained.

Text colors:

- Titles: `#1D2129`.
- Body/subtitle: `#4E5969`.
- Helper/table header: `#86909C`.
- Disabled: `#A9AEB8`.

## Layout

- Page background: `#F7F8FA`.
- Main content: white cards or white workbench surfaces.
- Use whitespace, pale borders, and `#F2F3F5` dividers for structure.
- Keep information density suitable for business operations: compact filters, tables, stats, detail drawers, and forms.
- Avoid oversized hero sections unless the target is explicitly a marketing page.
- Use light borders over heavy shadows.

## Components

### Buttons

- Primary: `#FF7752` background, white text.
- Hover: `#FF9275`.
- Pressed: `#E56B4A`.
- Disabled: `#FFD6CB`.
- Secondary: white background, `#E5E6EC` border, gray text.
- Text button: transparent background, `#FF7752` text.
- Default button height: 32px; large: 36px; extra large: 40px; small: 28px; mini: 24px.
- Default rectangular button radius: 6px.
- Do not make all buttons pill-shaped.

### Cards

- Default card: white background, `#E5E6EC` or `#F2F3F5` border.
- Selected brand card: `#FFF8F6` or pale brand gradient, with soft brand border.
- Metric cards may use functional light backgrounds or fixed functional gradients.
- Keep shadows subtle.

### Tables

- Header background: `#F7F8FA`.
- Header text: `#86909C`.
- Body text: `#1D2129` or `#4E5969`.
- Grid/dividers: `#F2F3F5` or `#E5E6EC`.
- Default tags: `#F2F3F5` bg and gray text.
- Status tags should use functional light backgrounds and semantic text colors.

### Forms

- Input border: `#E5E6EC`.
- Input text: `#1D2129`.
- Placeholder/helper: `#86909C` or `#A9AEB8`.
- Focus: primary border or subtle primary focus feedback.
- Error: `#F54B45` with `#FFEDE8` where background is needed.

### Tags And Status

| State | Background | Text |
| --- | --- | --- |
| Success | `#EBF9F6` | `#006C52` |
| Danger/error | `#FFEDE8` | `#A1171B` |
| Warning | `#FFF8E8` | `#A65508` |
| Info | `#F2F4FF` or `#EBF5FF` | `#344499` or `#014C99` |
| Brand | `#FFF8F6` | `#FF7752` |
| Neutral | `#F2F3F5` | `#4E5969` |

### Navigation

- Background: white or `#F7F8FA`.
- Default text: `#4E5969` or `#6B7785`.
- Selected item: `#FFF8F6` background and `#FF7752` text/icon, or strong text `#1D2129`.
- Dividers: `#E5E6EC` or `#F2F3F5`.

### Title Bars

- Common title-bar height: 76px; tabs title bar: 64px.
- Horizontal padding: 24px.
- Vertical padding: 16px.
- Bottom divider: `#F2F3F5`.
- Title: 17px equivalent, semibold, `#1D2129`.
- Subtitle/update text: 12px, `#86909C`.
- Right action gap: 12px.

### Dividers

- Default: 1px `#F2F3F5`.
- Use `#E5E6EC` only for stronger boundaries.
- Vertical text dividers commonly use 14px height with 12px horizontal text spacing.

## Matching Rules

- Match coral orange near `#FF7752` to the primary brand token.
- Match pale orange/red backgrounds to `#FFF8F6`, `#FFF1EE`, or `#FFE4DC`.
- Match pale page background to `#F7F8FA`.
- Match borders/table lines to `#E5E6EC` or `#F2F3F5`.
- Match text hierarchy to `#1D2129`, `#4E5969`, `#86909C`, and `#A9AEB8`.
- Use semantic functional colors for state, not color similarity alone.

## Token Priority

1. Exact Figma component/frame tokens if available.
2. This design-system reference.
3. Component semantic rules in this reference.
4. Nearby token inference, explicitly marked as inferred.

Do not invent new colors unless necessary.
