# Android App — DESIGN.md Reference

## Platform Constraints

| Constraint | Rule |
|-----------|------|
| Units | `dp` for layout/spacing, `sp` for text sizes. Never use `px` directly |
| Touch Targets | Minimum 48×48dp for all interactive elements (Material guideline) |
| Fonts | Roboto (default) or custom via `res/font`. Use `sp` for text to respect user font scale |
| Components | Prefer Material Design 3 (Material You) components |
| Safe Areas | Handle system bars: status bar top, gesture nav bar bottom. Use `WindowInsetsCompat` |
| Dark Mode | Support via `values-night/` resource directory or dynamic color |
| Dynamic Color | Material You supports wallpaper-based dynamic theming — define seed color |

---

## DESIGN.md Structure for Android App

```markdown
# DESIGN.md — [Project Name] (Android App)

## 1. Project Overview
[One sentence: product purpose and target user]

## 2. Visual Theme
- Style: [Material You / Custom branded / Flat]
- Theme: [Light only / Dark only / Follow system]
- Density: [Spacious / Standard / Compact]
- Design reference: [Similar to: Gmail, Notion, Linear, etc.]

## 3. Color System (Material You tokens)

| Token | Light Hex | Dark Hex | Usage |
|-------|-----------|----------|-------|
| primary | #XXXXXX | #XXXXXX | FAB, filled buttons, active nav |
| onPrimary | #FFFFFF | #XXXXXX | Text/icon on primary |
| primaryContainer | #XXXXXX | #XXXXXX | Chips, selected states |
| secondary | #XXXXXX | #XXXXXX | Secondary actions |
| background | #FAFAFA | #1C1B1F | Page background |
| surface | #FFFFFF | #2B2930 | Cards, bottom sheets |
| surfaceVariant | #F4EFF4 | #49454F | Input fields, chips |
| outline | #79747E | #938F99 | Borders, dividers |
| error | #B3261E | #F2B8B5 | Error states |

## 4. Typography (Material Type Scale)

Font: Roboto (system default) / [Custom font name]

| Style | sp Size | Weight | Usage |
|-------|---------|--------|-------|
| displayLarge | 57sp | 400 | Hero text |
| headlineMedium | 28sp | 400 | Screen titles |
| titleLarge | 22sp | 400 | App bar title |
| titleMedium | 16sp | 500 | Card titles, list headers |
| bodyLarge | 16sp | 400 | Primary body text |
| bodyMedium | 14sp | 400 | Secondary body, list items |
| labelLarge | 14sp | 500 | Buttons |
| labelSmall | 11sp | 500 | Captions, badges |

## 5. Spacing & Layout

Base unit: 4dp

| Token | dp | Usage |
|-------|----|-------|
| spacing-xs | 4dp | Icon padding |
| spacing-sm | 8dp | Inline gaps |
| spacing-md | 16dp | Card padding, screen margin |
| spacing-lg | 24dp | Section spacing |
| spacing-xl | 32dp | Major layout breaks |

Screen horizontal margin: 16dp
List item height: 56dp (single line) / 72dp (two lines) / 88dp (three lines)

## 6. Component Specs

### Buttons
- Filled: background `primary`, `onPrimary` text, 20dp corner radius
- Outlined: `outline` border, `primary` text
- Text: no border/background, `primary` text
- FAB: 56×56dp, 16dp corner radius, `primaryContainer` background
- Min touch target: 48dp height

### Cards
- Background: `surface`
- Elevation: 1dp (rest), 3dp (hovered), 8dp (dragged)
- Corner radius: 12dp
- Padding: 16dp

### Top App Bar
- Height: 64dp
- Background: `surface`
- Title: titleLarge

### Navigation
- Bottom nav: 3-5 items, icon 24dp, label 12sp
- Navigation drawer: 360dp wide, list items 56dp tall

### Text Fields
- Outlined style preferred
- Corner radius: 4dp
- Height: 56dp
- Use `surfaceVariant` fill for filled variant

## 7. Platform-Specific Rules

- Always handle `WindowInsets` — don't draw under system bars unless intentional
- Use `Scaffold` padding for bottom nav overlap
- All tap states must have ripple effect
- Long-press should trigger contextual action / selection mode
- Support RTL layout (use `start/end` not `left/right`)
- Minimum list item touch target: full row width × 48dp height

## 8. Do's and Don'ts

**Do:**
- Use Material You dynamic color as a layer on top of fixed brand colors
- Provide meaningful motion (container transforms, shared element transitions)
- Handle empty states with icon + message + primary action

**Don't:**
- Don't use `px` units
- Don't hardcode colors — always reference theme attributes
- Don't create custom components when Material ones exist
- Don't ignore dark mode — test all screens

## 9. Agent Prompt Guide

**Quick color reference:**
- Primary: [PRIMARY_HEX]
- Background: [BG_HEX]
- Surface: [SURFACE_HEX]

**Ready-to-use prompts:**

Build a screen:
> "Using DESIGN.md, build a [ScreenName] composable in Jetpack Compose. Follow the Material You color tokens, spacing system, and component specs defined there."

Extract a component:
> "Using DESIGN.md, create a reusable [ComponentName] composable with parameters: [xxx]. Apply the correct typography scale and spacing tokens."

Fix consistency:
> "Review this Composable against DESIGN.md. Fix any hardcoded colors, incorrect spacing values, or missing ripple effects."
```
