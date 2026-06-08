# Design Tokens

All concrete values used in PSYDA UI. Use Tailwind class names — never inline hex.

## Brand colors

| Token | Hex | Tailwind | Use |
|-------|-----|----------|-----|
| primary | `#2563EB` | `blue-600` | Main CTA, active state |
| primary-dark | `#1E40AF` | `blue-700` | CTA hover, emphasis |
| primary-soft | `#DBEAFE` | `blue-100` | Highlight background |
| primary-tint | `#EFF6FF` | `blue-50` | Faint background, hover region |

## Neutral colors

| Token | Hex | Tailwind | Use |
|-------|-----|----------|-----|
| dark | `#0F172A` | `slate-900` | Dark section background, headlines |
| dark-sec | `#1E293B` | `slate-800` | Body text |
| muted | `#64748B` | `slate-500` | Helper text, placeholder |
| light | `#F1F5F9` | `slate-100` | Card background, separator |
| border | `#E2E8F0` | `slate-200` | Borders |
| white | `#FFFFFF` | `white` | Page background |

## Semantic colors

| Token | Hex | Tailwind | Use | NEVER use for |
|-------|-----|----------|-----|---------------|
| success | `#10B981` | `emerald-500` | Completion, "active" | General info |
| info | `#3B82F6` | `blue-500` | Informational hints | Action buttons (use `primary`) |
| warning | `#F59E0B` | `amber-500` | Caution, deadline approaching | **Plain informational content** |
| danger | `#EF4444` | `red-500` | Error, destructive action | General emphasis |

Soft variants (for backgrounds): replace `-500` with `-100`. Text variants: use `-700`.

```html
<!-- info banner -->
<div class="bg-blue-50 border border-blue-200 text-blue-800">...</div>

<!-- warning banner (only for caution) -->
<div class="bg-amber-50 border border-amber-200 text-amber-800">...</div>
```

## Category stripes (for grouping rows/cards)

Cycle through 1-5 to visually distinguish groups.

```css
.color-1 { background: #3b82f6; }  /* blue */
.color-2 { background: #10b981; }  /* emerald */
.color-3 { background: #f59e0b; }  /* amber */
.color-4 { background: #ef4444; }  /* red */
.color-5 { background: #8b5cf6; }  /* violet */
```

Use as left side stripe on cards:

```html
<div class="bg-white border border-gray-200 rounded-xl flex">
  <div class="w-1.5 color-2"></div>
  <div class="flex-1 p-5">...</div>
</div>
```

## Typography

```
Font family
  -apple-system, BlinkMacSystemFont, "PingFang TC", "Microsoft JhengHei", sans-serif
```

| Level | Tailwind | Pixel | Use |
|-------|----------|-------|-----|
| Page title | `text-2xl font-bold` | 28px | Top-of-page heading |
| Section header | `text-xl font-semibold` | 20px | Card/section title |
| Subsection | `text-base font-medium` | 16px | Subsection title, form label |
| Body | `text-sm` | 14px | Regular content |
| Helper | `text-xs` | 12px | Captions, metadata |
| Micro | `text-[10px]` | 10px | Chips, tags, dense labels |

**Rules:**
- Use `tabular-nums` for numeric columns to align decimal points.
- Never use `font-light` (300) for Chinese text — readability suffers.
- Use `font-medium` (500) for labels, `font-semibold` (600) or `font-bold` (700) for headings.

## Spacing scale

Padding & margin (Tailwind defaults):

| Class | Pixel | Use |
|-------|-------|-----|
| `p-1` / `gap-1` | 4px | Icon + adjacent text |
| `p-2` / `gap-2` | 8px | Tag groups, button groups |
| `p-3` / `gap-3` | 12px | Compact list items |
| `p-4` / `gap-4` | 16px | Default cards, form fields |
| `p-5` / `gap-5` | 20px | Major content cards |
| `p-6` / `gap-6` | 24px | Hero areas, dense content |

## Radius

| Class | Pixel | Use |
|-------|-------|-----|
| `rounded` | 4px | Inputs, chips |
| `rounded-lg` | 8px | Cards, buttons, modals |
| `rounded-xl` | 12px | Major content cards |
| `rounded-full` | full | Avatars, status dots, pills |

## Shadow

| Class | Use |
|-------|-----|
| `shadow-sm` | Subtle elevation (focus card) |
| `shadow-md` | Card hover state |
| `shadow-lg` | Toast, dropdown |
| `shadow-xl` | Focused popover |
| `shadow-2xl` | Modal panel |

## Focus state

All interactive elements must include:

```html
focus:outline-none focus:ring-2 focus:ring-blue-500
```

Optional: add `focus:border-transparent` on inputs with borders.
