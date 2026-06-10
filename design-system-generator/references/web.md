# Web (Admin / Dashboard) — DESIGN.md Reference

## Platform Constraints

| Constraint | Rule |
|-----------|------|
| Units | `rem` for spacing/typography (base 16px), `px` for borders/shadows |
| Breakpoints | Mobile 375px / Tablet 768px / Desktop 1280px / Wide 1440px |
| Fonts | System stack or Google Fonts (loaded via CDN). Fallback always defined |
| Framework | Tailwind CSS tokens preferred — use `text-sm`, `p-4` style naming in prompt guide |
| Dark Mode | CSS variables approach — define `:root` and `[data-theme="dark"]` overrides |
| Accessibility | Color contrast ≥ 4.5:1 for text, ≥ 3:1 for UI components |

---

## DESIGN.md Structure for Web Admin

```markdown
# DESIGN.md — [Project Name] (Web Admin)

## 1. Project Overview
[One sentence: product purpose and primary user role — e.g., "Internal dashboard for lottery terminal operators to manage content and monitor device status"]

## 2. Visual Theme
- Style: [Clean SaaS / Dark dashboard / Editorial / Data-heavy]
- Theme: [Light / Dark / System-aware]
- Density: [Spacious / Balanced / Compact]
- Reference products: [e.g., Linear, Vercel, Supabase]

## 3. Color System

CSS variables (define in :root and [data-theme="dark"]):

| Variable | Light | Dark | Usage |
|----------|-------|------|-------|
| --color-primary | #XXXXXX | #XXXXXX | CTA buttons, links, active states |
| --color-primary-hover | #XXXXXX | #XXXXXX | Button hover |
| --color-secondary | #XXXXXX | #XXXXXX | Secondary actions, tags |
| --color-bg | #F9FAFB | #0F1117 | Page background |
| --color-surface | #FFFFFF | #1A1D27 | Cards, panels, sidebars |
| --color-surface-hover | #F3F4F6 | #22263A | Row/item hover |
| --color-border | #E5E7EB | #2D3142 | Dividers, input borders |
| --color-text-primary | #111827 | #F9FAFB | Headings, primary content |
| --color-text-secondary | #6B7280 | #9CA3AF | Labels, metadata |
| --color-text-muted | #9CA3AF | #6B7280 | Placeholders, disabled |
| --color-success | #10B981 | #34D399 | Online, active, success |
| --color-warning | #F59E0B | #FBBF24 | Warnings, pending |
| --color-error | #EF4444 | #F87171 | Errors, offline, delete |
| --color-info | #3B82F6 | #60A5FA | Info, neutral status |

## 4. Typography

Font stack: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
(Or replace Inter with your chosen font)

| Scale | rem | px | Weight | Tailwind | Usage |
|-------|-----|----|--------|---------|-------|
| display | 2rem | 32px | 700 | text-3xl font-bold | Page heroes |
| h1 | 1.5rem | 24px | 600 | text-2xl font-semibold | Page titles |
| h2 | 1.25rem | 20px | 600 | text-xl font-semibold | Section headings |
| h3 | 1rem | 16px | 500 | text-base font-medium | Card headings |
| body | 0.875rem | 14px | 400 | text-sm | Primary content |
| small | 0.75rem | 12px | 400 | text-xs | Metadata, captions |
| label | 0.75rem | 12px | 500 | text-xs font-medium | Form labels, tags |

## 5. Spacing System

Base: 4px (0.25rem)

| Token | rem | px | Tailwind | Usage |
|-------|-----|----|---------|-------|
| space-1 | 0.25rem | 4px | p-1 | Tight inline gaps |
| space-2 | 0.5rem | 8px | p-2 | Icon margins |
| space-3 | 0.75rem | 12px | p-3 | Small component padding |
| space-4 | 1rem | 16px | p-4 | Standard component padding |
| space-6 | 1.5rem | 24px | p-6 | Card padding |
| space-8 | 2rem | 32px | p-8 | Section padding |
| space-12 | 3rem | 48px | p-12 | Major layout gaps |

Page max-width: 1280px (centered)
Sidebar width: 240px (collapsed: 64px)
Content padding: 24px

## 6. Component Specs

### Buttons
- Primary: `bg-[--color-primary]` white text, 6px radius, 32px height (sm) / 36px (default) / 40px (lg)
- Secondary: `border border-[--color-border]` text-primary, transparent bg
- Destructive: `bg-[--color-error]` white text
- Ghost: no border, hover shows surface-hover bg
- Disabled: opacity-50, cursor-not-allowed

### Cards / Panels
- Background: `--color-surface`
- Border: `1px solid --color-border`
- Border radius: 8px
- Padding: 24px
- Shadow: `0 1px 3px rgba(0,0,0,0.08)` (light) / none (dark — use border instead)

### Data Tables
- Header: bg `--color-surface-hover`, text `--color-text-secondary`, uppercase 11px font-medium
- Row height: 44px
- Row hover: `--color-surface-hover`
- Border: horizontal only, `--color-border`
- Zebra striping: optional, use sparingly

### Form Inputs
- Height: 36px
- Border: `1px solid --color-border`
- Border radius: 6px
- Focus: `2px solid --color-primary` outline
- Background: `--color-surface`
- Padding: 0 12px

### Status Badges
- Online/Active: green dot or `bg-success/10 text-success`
- Offline/Error: red dot or `bg-error/10 text-error`
- Pending/Warning: amber dot or `bg-warning/10 text-warning`
- Border radius: 9999px (pill)

### Sidebar Navigation
- Width: 240px
- Item height: 36px
- Active item: `bg-primary/10 text-primary font-medium`
- Icon size: 16px
- Group label: 11px uppercase text-muted, margin-top 16px

## 7. Layout Principles

- Sidebar + main content layout (not top nav for admin panels)
- Content area max-width: 1280px or full-width for data tables
- Use 12-column grid for form layouts: labels 4 cols, inputs 8 cols
- Empty states: centered, icon + heading + description + CTA button
- Loading: skeleton screens (not spinners) for content areas

## 8. Do's and Don'ts

**Do:**
- Use CSS variables for all colors — enables dark mode with zero extra CSS
- Provide hover and focus states on every interactive element
- Use consistent icon set (Lucide / Heroicons / Tabler)
- Show empty states and error states — don't just hide them

**Don't:**
- Don't use `#000` or `#fff` directly — use tokens
- Don't mix spacing scales (no arbitrary `margin: 13px`)
- Don't use color alone to convey status — add icon or text
- Don't make buttons less than 32px tall

## 9. Agent Prompt Guide

**Quick color reference:**
- Primary: [PRIMARY_HEX]
- Background: [BG_HEX]
- Surface: [SURFACE_HEX]
- Border: [BORDER_HEX]

**Ready-to-use prompts:**

Build a page:
> "Using DESIGN.md, build a [PageName] page in React with Tailwind CSS. Apply the color system via CSS variables, use the typography scale, and follow the card and table component specs."

Build a component:
> "Using DESIGN.md, create a reusable [ComponentName] component with props: [xxx]. Match the spacing tokens and button/input specs exactly."

Dark mode audit:
> "Check this component against DESIGN.md. Replace any hardcoded colors with CSS variables and ensure dark mode works by testing with data-theme='dark'."
```
