---
name: psyda-design-system
description: Engineer reference for implementing PSYDA UI (心理測評題庫管理系統). Use when writing or reviewing frontend code for PSYDA, choosing Tailwind class strings for UI components, or implementing composite patterns (step modals, dual-pane pickers, cascade dropdowns, batch operations). Detail files (tokens.md, components.md, patterns.md, rules.md) are loaded on demand. Skip if working on backend logic, infrastructure, or non-PSYDA frontend code.
---

# PSYDA Design System

Code-first implementation reference for the PSYDA platform (Tailwind CSS + Alpine.js).

## When to read which file

| Topic | File |
|-------|------|
| Color tokens, typography, spacing, radius | [tokens.md](references/tokens.md) |
| Atomic components (button, card, input, modal, table, badge, alert) | [components.md](references/components.md) |
| Composite patterns (step modal, 5:7 picker, cascade dropdown, batch ops) | [patterns.md](references/patterns.md) |
| Do/don't concrete rules + anti-pattern code samples | [rules.md](references/rules.md) |

Read SKILL.md first. Load detail files (in `references/`) only when you need them.

---

## Quick Reference — Top 12 Templates

| Need | Class string |
|------|--------------|
| Primary CTA | `px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm font-medium` |
| Secondary button | `px-4 py-2 bg-white border border-gray-300 rounded-lg hover:bg-gray-50 text-sm font-medium` |
| Danger button | `px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 text-sm font-medium` |
| Standard card | `bg-white border border-gray-200 rounded-xl p-5` |
| Text input | `w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500` |
| Status pill (active) | `px-2 py-0.5 bg-green-100 text-green-700 rounded-full text-xs font-medium` |
| Info banner | `bg-blue-50 border border-blue-200 rounded-lg p-3 text-xs text-blue-800` |
| Warning banner | `bg-amber-50 border border-amber-200 rounded-lg p-3 text-xs text-amber-800` |
| Modal backdrop | `fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4` |
| Modal panel | `bg-white rounded-xl shadow-2xl max-w-3xl w-full max-h-[90vh] overflow-hidden flex flex-col` |
| Table header | `bg-gray-50 border-b border-gray-200 text-left` (cells: `px-4 py-3 font-medium text-gray-700`) |
| Toast | `fixed bottom-6 right-6 bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg z-50` |

---

## Top 5 Critical Rules

1. **Tokens only**. Use Tailwind class names (`bg-blue-600`); never inline hex.
2. **Info ≠ Warning**. Use blue (`info`) for plain hints. Reserve amber (`warning`) for content that needs attention.
3. **No nested tables**. Replace with summary + expand pattern (see [patterns.md](patterns.md)).
4. **Surface primary actions**. High-frequency actions belong as visible buttons. Hide only low-frequency or destructive actions in `⋮` menu.
5. **Always confirm destructive ops**. Pair every delete with a confirmation modal that offers a non-destructive alternative (e.g., "Disable").

For the full set of rules with code examples, see [rules.md](references/rules.md).

---

## Stack

- **Prototyping**: Tailwind CSS (CDN) + Alpine.js v3
- **Production target**: Next.js + React + shadcn/ui (styles compatible)
- **Chinese fonts**: PingFang TC (macOS) / Microsoft JhengHei (Windows). Never use `font-light` (300) for Chinese.

---

## Decision tree

```
Building a UI element?
├── Atomic (button, input, card, badge)        → references/components.md
├── Composite flow (step form, picker, modal)  → references/patterns.md
├── Need a color / spacing value               → references/tokens.md
└── Unsure if your approach is correct         → references/rules.md (do/don't)
```
