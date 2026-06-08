---
name: psyda-design-system
description: Engineer reference for implementing PSYDA UI. Use when writing or reviewing frontend code for the PSYDA platform (Tailwind CSS + Alpine.js). Provides copy-paste class strings for colors, spacing, components (buttons, cards, modals, tables), composite patterns (step modals, 5:7 picker, cascade dropdowns, batch ops, action menus), and concrete do/don't rules with code examples. Skip if working on backend logic or non-UI tasks.
---

# PSYDA Design System — Engineer Reference

This is a code-first implementation reference. For every UI element you build, find the matching template here and copy. Deviation requires justification.

---

## Quick Reference

Look up by what you need to build:

| Need | Template / Token |
|------|------------------|
| Primary CTA | `bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 text-sm font-medium` |
| Secondary button | `bg-white border border-gray-300 px-4 py-2 rounded-lg hover:bg-gray-50 text-sm font-medium` |
| Danger button | `bg-red-600 text-white px-4 py-2 rounded-lg hover:bg-red-700 text-sm font-medium` |
| Card (standard) | `bg-white border border-gray-200 rounded-xl p-5` |
| Card (focus) | `border-2 border-blue-300 rounded-lg shadow-sm` |
| Input | `w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500` |
| Status pill (active) | `px-2 py-0.5 bg-green-100 text-green-700 rounded-full text-xs font-medium` |
| Status pill (draft) | `px-2 py-0.5 bg-gray-100 text-gray-600 rounded-full text-xs font-medium` |
| Info banner | `bg-blue-50 border border-blue-200 rounded-lg p-3 text-xs text-blue-800` |
| Warning banner | `bg-amber-50 border border-amber-200 rounded-lg p-3 text-xs text-amber-800` |
| Modal backdrop | `fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4` |
| Modal panel | `bg-white rounded-xl shadow-2xl max-w-3xl w-full max-h-[90vh] overflow-hidden flex flex-col` |
| Table header row | `bg-gray-50 border-b border-gray-200 text-left` (cells: `px-4 py-3 font-medium text-gray-700`) |
| Page header | `text-xl font-bold` + `text-sm text-gray-500` for subtitle |
| Toast | `fixed bottom-6 right-6 bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg z-50` |

---

## Tokens

### Color (use Tailwind classes; never inline hex)

```
primary       blue-600    #2563EB    Main CTA, brand, active state
primary-dark  blue-700    #1E40AF    Primary hover, emphasized text
primary-soft  blue-100    #DBEAFE    Highlight background, active region
primary-tint  blue-50     #EFF6FF    Faint background, hover region

dark          slate-900   #0F172A    Title slide background, headlines
dark-sec      slate-800   #1E293B    Body text
muted         slate-500   #64748B    Helper text, placeholder
light         slate-100   #F1F5F9    Card background, separator
border        slate-200   #E2E8F0    Borders
white         white       #FFFFFF    Page background

success       emerald-500 #10B981    Completion, "active" state
info          blue-500    #3B82F6    Informational hint
warning       amber-500   #F59E0B    Caution, deadline approaching
danger        red-500     #EF4444    Error, destructive action
```

### Category color stripes (cycle through 1-5 for grouping)

```css
.color-1 { background: #3b82f6; }  /* blue */
.color-2 { background: #10b981; }  /* emerald */
.color-3 { background: #f59e0b; }  /* amber */
.color-4 { background: #ef4444; }  /* red */
.color-5 { background: #8b5cf6; }  /* violet */
```

### Typography

```
Font family: -apple-system, BlinkMacSystemFont, "PingFang TC", "Microsoft JhengHei", sans-serif

text-2xl  font-bold       Page title (28px)
text-xl   font-semibold   Section header (20px)
text-base font-medium     Subsection (16px)
text-sm                   Body (14px)
text-xs                   Helper / metadata (12px)
text-[10px]               Tags, chips, micro labels

Use tabular-nums for numeric columns.
Never use font-light (300) for Chinese text.
```

### Spacing

```
gap-1   4px    Icon + text
gap-2   8px    Tag groups, button groups
gap-3   12px   Form field stacks
gap-4   16px   Card internal sections
gap-6   24px   Major section gaps

Card padding:
  p-3  small list items
  p-4  default cards
  p-5  major content cards
  p-6  dense content / hero areas

Radius:
  rounded     4px   inputs, chips
  rounded-lg  8px   cards, buttons, modals
  rounded-xl  12px  major content cards
  rounded-full        avatars, dots, status badges
```

---

## Components

### Button — Primary

Use for the most important action on the page. Max 1-2 primary buttons per view.

```html
<button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm font-medium flex items-center gap-2">
  <svg class="w-4 h-4">...</svg>
  Save
</button>
```

### Button — Secondary

```html
<button class="px-4 py-2 bg-white border border-gray-300 rounded-lg hover:bg-gray-50 text-sm font-medium">
  Cancel
</button>
```

### Button — Danger

Only for destructive actions. Always pair with confirmation flow (see Patterns).

```html
<button class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 text-sm font-medium">
  Delete
</button>
```

### Button — Ghost

For row actions in tables / list items.

```html
<button class="px-2 py-1 rounded text-xs text-gray-700 hover:bg-gray-100">
  Edit
</button>
```

### Button — Disabled state

```html
<button disabled class="px-4 py-2 bg-blue-600 text-white rounded-lg disabled:bg-gray-100 disabled:text-gray-400 disabled:cursor-not-allowed">
  Next
</button>
```

### Badge — Status pill

```html
<!-- Active / 進行中 -->
<span class="px-2 py-0.5 bg-green-100 text-green-700 rounded-full text-xs font-medium">Active</span>

<!-- Draft / 未發布 -->
<span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded-full text-xs font-medium">Draft</span>

<!-- Closed / 已關閉 -->
<span class="px-2 py-0.5 bg-slate-200 text-slate-500 rounded-full text-xs font-medium">Closed</span>
```

### Badge — Counter (for tabs)

```html
<button class="px-4 py-2 rounded-lg bg-blue-600 text-white">
  Active
  <span class="px-1.5 py-0.5 rounded-full text-xs bg-white/20">5</span>
</button>
```

### Card — Standard

```html
<div class="bg-white border border-gray-200 rounded-xl p-5 hover:shadow-md transition">
  ...
</div>
```

### Card — Focus (emphasis)

For the primary card in a paired layout (e.g., right side of a picker).

```html
<div class="border-2 border-blue-300 rounded-lg overflow-hidden shadow-sm">
  <div class="bg-blue-600 px-4 py-3 text-white">Title</div>
  <div class="p-4 bg-white">Content</div>
</div>
```

### Card — Left stripe (for grouping)

```html
<div class="bg-white border border-gray-200 rounded-xl overflow-hidden flex">
  <div class="w-1.5 bg-blue-500"></div>
  <div class="flex-1 p-5">Content</div>
</div>
```

### Input — Text

```html
<label class="block text-sm font-medium mb-1">
  Name <span class="text-red-500">*</span>
</label>
<input type="text" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" />
<p class="text-xs text-gray-500 mt-1">Helper text</p>
```

### Input — Textarea

```html
<textarea rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
```

### Input — Select

```html
<select class="px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 disabled:bg-gray-100 disabled:text-gray-400">
  <option value="">Option</option>
</select>
```

### Modal

```html
<div x-show="open" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4" @click.self="open = false">
  <div class="bg-white rounded-xl shadow-2xl max-w-3xl w-full max-h-[90vh] overflow-hidden flex flex-col">

    <!-- Header -->
    <div class="px-6 py-4 border-b border-gray-200 flex items-center justify-between">
      <h2 class="text-lg font-bold">Modal Title</h2>
      <button @click="open = false" class="p-1 hover:bg-gray-100 rounded">
        <svg class="w-5 h-5">...</svg>
      </button>
    </div>

    <!-- Body (scrollable) -->
    <div class="flex-1 overflow-y-auto p-6 space-y-4">
      ...
    </div>

    <!-- Footer -->
    <div class="px-6 py-4 border-t border-gray-200 flex items-center justify-end gap-2">
      <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg">Cancel</button>
      <button class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm">Save</button>
    </div>
  </div>
</div>
```

### Table

```html
<table class="w-full text-sm">
  <thead class="bg-gray-50 border-b border-gray-200 text-left">
    <tr>
      <th class="px-4 py-3 font-medium text-gray-700">Column</th>
    </tr>
  </thead>
  <tbody>
    <tr class="border-b border-gray-100 hover:bg-blue-50/30">
      <td class="px-4 py-3">Cell</td>
    </tr>
  </tbody>
</table>
```

### Alert — Info (blue)

Default for non-warning informational hints.

```html
<div class="bg-blue-50 border border-blue-200 rounded-lg p-3 flex items-start gap-2">
  <svg class="w-5 h-5 text-blue-600 flex-shrink-0 mt-0.5">...</svg>
  <div class="text-xs text-blue-800">Informational message</div>
</div>
```

### Alert — Warning (amber)

Only for "needs attention" or "deadline approaching" content. Never use for plain information.

```html
<div class="bg-amber-50 border border-amber-200 rounded-lg p-3 text-sm text-amber-800">
  Deadline approaching / action required
</div>
```

### Alert — Success (green)

```html
<div class="bg-green-50 border border-green-200 rounded-lg p-3 text-sm text-green-800">
  Saved successfully
</div>
```

### Empty state

```html
<div class="flex flex-col items-center justify-center py-12 text-gray-400">
  <svg class="w-10 h-10 mb-3 opacity-50">...</svg>
  <p class="text-sm">No items yet</p>
  <p class="text-xs mt-1">Click "Add" to create one</p>
</div>
```

### Toast

```html
<div x-show="toast" class="fixed bottom-6 right-6 bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg z-50 flex items-center gap-2">
  <svg class="w-5 h-5 text-green-400">...</svg>
  <span x-text="toast"></span>
</div>
```

---

## Patterns (Composite Components)

### Pattern: Step Modal

Use when a form has 5+ fields or covers multiple concepts. Max 5 steps.

**Step indicator (in modal header):**

```html
<div class="px-6 py-4 bg-gray-50 border-b border-gray-200">
  <div class="flex items-center justify-between">
    <template x-for="(step, idx) in steps">
      <div class="flex items-center flex-1">
        <div class="flex items-center gap-2">
          <div class="w-8 h-8 rounded-full flex items-center justify-center text-sm font-medium"
               :class="current > idx ? 'bg-emerald-500 text-white' :
                       current === idx ? 'bg-blue-600 text-white' :
                       'bg-gray-200 text-gray-500'">
            <span x-show="current <= idx" x-text="idx + 1"></span>
            <svg x-show="current > idx" class="w-4 h-4">...</svg>
          </div>
          <span class="text-sm" :class="current === idx ? 'font-medium text-blue-600' : 'text-gray-500'" x-text="step"></span>
        </div>
        <div x-show="idx < steps.length - 1" class="flex-1 h-px bg-gray-300 mx-3"></div>
      </div>
    </template>
  </div>
</div>
```

**Step footer:**

```html
<div class="px-6 py-4 border-t border-gray-200 flex items-center justify-between">
  <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg" :disabled="current === 0">Back</button>
  <span class="text-xs text-gray-500" x-text="(current + 1) + ' / ' + steps.length"></span>
  <button class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm">
    <span x-show="current < steps.length - 1">Next</span>
    <span x-show="current === steps.length - 1">Finish</span>
  </button>
</div>
```

### Pattern: Picker (5:7 dual pane)

Use when selecting items from a pool into a list. Right side is the visual focus.

```html
<div class="grid grid-cols-12 gap-4 h-[28rem]">
  <!-- Left: source pool (5/12, visually light) -->
  <div class="col-span-5 border border-gray-200 rounded-lg flex flex-col overflow-hidden bg-gray-50/30">
    <div class="bg-gray-50 border-b border-gray-200 p-2">
      <!-- Search + filters -->
    </div>
    <div class="flex-1 overflow-y-auto p-2">
      <!-- Checkbox items -->
    </div>
  </div>

  <!-- Right: selected list (7/12, visual focus) -->
  <div class="col-span-7 border-2 border-blue-300 rounded-lg flex flex-col overflow-hidden shadow-sm">
    <div class="bg-blue-600 px-4 py-3 text-white">Selected items</div>
    <div class="flex-1 overflow-y-auto p-3 bg-white">
      <!-- Selected items as numbered cards -->
    </div>
  </div>
</div>
```

### Pattern: Cascade Dropdowns (3 levels)

```html
<div class="grid grid-cols-3 gap-2">
  <select x-model="l1" @change="l2 = ''; l3 = ''" class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
    <option value="">Level 1</option>
    <template x-for="opt in l1Options"><option :value="opt" x-text="opt"></option></template>
  </select>

  <select x-model="l2" :disabled="!l1" @change="l3 = ''"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm disabled:bg-gray-100 disabled:text-gray-400">
    <option value="">Level 2</option>
    <template x-for="opt in l2Options(l1)"><option :value="opt" x-text="opt"></option></template>
  </select>

  <select x-model="l3" :disabled="!l2"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm disabled:bg-gray-100 disabled:text-gray-400">
    <option value="">Level 3</option>
    <template x-for="opt in l3Options(l1, l2)"><option :value="opt" x-text="opt"></option></template>
  </select>
</div>
```

**Alpine methods:**

```js
get l1Options() { return [...new Set(items.map(i => i.l1))]; },
l2Options(l1) { return [...new Set(items.filter(i => i.l1 === l1).map(i => i.l2))]; },
l3Options(l1, l2) { return [...new Set(items.filter(i => i.l1 === l1 && i.l2 === l2).map(i => i.l3))]; },
```

### Pattern: Batch Operation Bar

Appears when items are selected.

```html
<div x-show="selectedIds.length > 0" x-transition
     class="bg-blue-50 border border-blue-200 rounded-lg p-3 flex items-center justify-between">
  <div class="text-sm text-blue-900">
    Selected <span class="font-bold" x-text="selectedIds.length"></span> items
  </div>
  <div class="flex items-center gap-2">
    <button class="px-3 py-1.5 bg-white border border-gray-300 rounded-md text-sm hover:bg-gray-50">Enable</button>
    <button class="px-3 py-1.5 bg-white border border-red-300 text-red-600 rounded-md text-sm hover:bg-red-50">Delete</button>
    <button class="text-sm text-gray-600 px-2" @click="selectedIds = []">Cancel</button>
  </div>
</div>
```

### Pattern: Action Menu (three-dot)

Use this ONLY for low-frequency or destructive actions. High-frequency actions belong as visible buttons.

```html
<div class="relative">
  <button @click="open = !open" class="p-2 hover:bg-gray-100 rounded">
    <svg class="w-4 h-4 text-gray-500" fill="currentColor" viewBox="0 0 20 20">
      <path d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z"/>
    </svg>
  </button>
  <div x-show="open" @click.outside="open = false" x-transition
       class="absolute right-0 top-9 bg-white border border-gray-200 rounded-lg shadow-lg z-10 w-48 py-1">
    <button class="w-full text-left px-3 py-2 text-sm hover:bg-gray-50 text-gray-700">Duplicate</button>
    <button class="w-full text-left px-3 py-2 text-sm hover:bg-gray-50 text-gray-700">Edit</button>
    <div class="border-t border-gray-100 my-1"></div>
    <button class="w-full text-left px-3 py-2 text-sm hover:bg-red-50 text-red-600">Delete</button>
  </div>
</div>
```

### Pattern: Delete Confirmation

Required for any destructive action.

```html
<div class="bg-white rounded-xl shadow-2xl max-w-md p-6">
  <div class="flex items-start gap-3 mb-4">
    <div class="w-10 h-10 bg-red-100 rounded-full flex items-center justify-center flex-shrink-0">
      <svg class="w-5 h-5 text-red-600">...</svg>
    </div>
    <div>
      <h3 class="font-bold mb-1">Delete this item?</h3>
      <p class="text-sm text-gray-600">
        Will delete "<span class="font-medium" x-text="item.name"></span>"
        <span class="text-red-600 font-medium">and X dependent records.</span>
      </p>
    </div>
  </div>
  <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3 text-sm text-yellow-800 mb-4">
    Consider "Disable" instead — can be restored anytime.
  </div>
  <div class="flex items-center justify-end gap-2">
    <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg">Cancel</button>
    <button class="px-4 py-2 text-sm bg-gray-600 text-white rounded-lg">Disable instead</button>
    <button class="px-4 py-2 text-sm bg-red-600 text-white rounded-lg">Confirm delete</button>
  </div>
</div>
```

### Pattern: Progress Bar with Threshold

For showing values with colored bands (used for completion %, scores, risk levels).

```html
<div class="text-sm font-medium" x-text="value + ' / ' + total"></div>
<div class="w-full bg-gray-200 rounded-full h-1.5 mt-1.5">
  <div class="h-1.5 rounded-full"
       :class="ratio >= 0.7 ? 'bg-green-500' : ratio >= 0.3 ? 'bg-blue-500' : 'bg-amber-500'"
       :style="`width: ${ratio * 100}%`"></div>
</div>
```

### Pattern: Days Remaining Indicator

```html
<div class="text-xs font-medium"
     :class="daysLeft < 3 ? 'text-red-600' :
             daysLeft < 7 ? 'text-amber-600' : 'text-gray-500'"
     x-text="daysLeft > 0 ? `Remaining ${daysLeft} days` : 'Ended'">
</div>
```

### Pattern: Breadcrumb Path (categories)

```html
<!-- Plain text breadcrumb, no colored chips -->
<div class="text-xs text-gray-500">
  <span x-text="l1"></span> ›
  <span x-text="l2"></span> ›
  <span class="text-gray-700 font-medium" x-text="l3"></span>
</div>
```

---

## Concrete Rules

### Colors

- **Use** Tailwind class names (`text-blue-600`).
- **Don't** inline hex (`color: #2563EB`).
- **Use** `warning` (amber) only for content that needs attention.
- **Don't** use `warning` for plain informational content (use `info` blue).
- **Use** at most 3 saturated colors per row (e.g., 3 status pills).
- **Don't** chain 3+ colored badges per item (creates noise — see `breadcrumb` pattern).

### Forms

- **Use** cascade dropdowns with `:disabled="!parent"` for L2/L3.
- **Don't** allow user to skip parent levels.
- **Use** step modal for forms with 5+ fields.
- **Don't** put step indicators outside the modal — keep them in the header.

### Pickers (selecting items from a list)

- **Use** the 5:7 grid (`col-span-5` / `col-span-7`).
- **Don't** use 50/50 layout — the selected list deserves more visual weight.
- **Use** plain-text breadcrumb for category hierarchy.
- **Don't** use 3 colored chips per item.

### Modals

- **Use** `max-h-[90vh]` + scrollable body (`flex-1 overflow-y-auto`).
- **Don't** allow the modal to overflow the viewport.
- **Use** `@click.self="open = false"` on the backdrop to close.
- **Don't** put close logic on the modal panel itself.

### Tables

- **Use** flat tables.
- **Don't** nest tables inside table cells (use summary + expand instead).

### Action Buttons

- **Use** visible buttons for top 2-3 most-used actions per row.
- **Don't** hide high-frequency actions in `⋮` menu.
- **Use** `⋮` menu only for low-frequency or destructive actions.

### Destructive Actions

- **Use** confirmation modal for any delete or destructive op.
- **Don't** ship one-click delete.
- **Offer** a non-destructive alternative (e.g., "Disable" instead of "Delete").

### Loading & Feedback

- **Use** Toast for "save success", "delete success" feedback.
- **Don't** use Toast for errors (use inline alert in context).
- **Use** disabled state with `disabled:opacity-50 disabled:cursor-not-allowed`.

### Empty States

- **Use** icon + 1-line title + 1-line action hint.
- **Don't** just show a blank area.
- **Include** a CTA button when applicable ("Click to add the first one").

### Typography

- **Use** `font-medium` (500) for labels.
- **Use** `font-semibold` (600) or `font-bold` (700) for headings.
- **Don't** use `font-light` (300) for Chinese text.
- **Use** `tabular-nums` for numeric columns to align.

### Spacing

- **Use** padding values from the spacing scale (p-3, p-4, p-5, p-6).
- **Don't** use arbitrary values (`p-[17px]`) unless absolutely necessary.

### Accessibility

- **Use** `focus:ring-2 focus:ring-blue-500` on all interactive elements.
- **Use** semantic HTML (`button`, `label`, `nav`, `main`).
- **Don't** rely on color alone — pair with text or icon.
- **Use** `aria-*` attributes for non-obvious interactive elements.

---

## Anti-Patterns (Never Do)

```html
<!-- ❌ Tech jargon in user-facing labels -->
<label>Prompt</label>
<label>Skill ID</label>

<!-- ✅ Use plain language -->
<label>AI evaluation guide</label>
<label>Linked skill (dropdown)</label>


<!-- ❌ Nested tables -->
<table>
  <tr><td><table>...</table></td></tr>
</table>

<!-- ✅ Summary + expand -->
<div>
  <span>12 items · 4 categories</span>
  <button @click="expanded = !expanded">Expand</button>
</div>


<!-- ❌ Three saturated chips per row -->
<span class="bg-blue-100 text-blue-700">L1</span>
<span class="bg-green-100 text-green-700">L2</span>
<span class="bg-amber-100 text-amber-700">L3</span>

<!-- ✅ Plain breadcrumb text -->
<div class="text-xs text-gray-500">
  <span>L1</span> › <span>L2</span> › <span class="font-medium">L3</span>
</div>


<!-- ❌ Warning yellow for plain info -->
<div class="bg-amber-50 border border-amber-200">
  This category's AI scoring guide: ...
</div>

<!-- ✅ Info blue -->
<div class="bg-blue-50 border border-blue-200">
  This category's AI scoring guide: ...
</div>


<!-- ❌ Hide primary action in ⋮ menu -->
<div class="dropdown">
  <button>⋮</button>
  <menu>
    <item>View results</item>      <!-- primary action buried -->
    <item>Manage employees</item>  <!-- primary action buried -->
  </menu>
</div>

<!-- ✅ Surface primary actions as buttons -->
<button class="bg-blue-600 text-white">View results</button>
<button class="border">Manage employees</button>
<button class="dropdown">⋮</button>


<!-- ❌ Markdown syntax exposed in input -->
<textarea>### Header\n**bold**</textarea>

<!-- ✅ Rich text toolbar -->
<div class="toolbar"><button>B</button><button>I</button></div>
<textarea>...</textarea>


<!-- ❌ One-click delete -->
<button @click="delete()">🗑</button>

<!-- ✅ Confirm + offer alternative -->
<button @click="confirmDelete()">🗑</button>
<!-- Then show modal with: Cancel / Disable instead / Confirm delete -->


<!-- ❌ Inline hex / 8-char hex -->
<div style="color: #2563EB">
<div shadow="color: 00000020">

<!-- ✅ Tailwind classes + opacity prop -->
<div class="text-blue-600">
<div class="shadow-lg"> <!-- or shadow with opacity: 0.12 -->


<!-- ❌ Cascade picker for selecting many items -->
<select>L1</select><select>L2</select><select>L3</select>
<!-- ...user repeats 30 times to add 10 items -->

<!-- ✅ Use 5:7 picker pattern with multi-select checkboxes -->
<!-- See Pattern: Picker (5:7 dual pane) -->


<!-- ❌ Translated "Save and create another" verbatim -->
<button>儲存並創建另一個</button>

<!-- ✅ Natural Chinese -->
<button>儲存並繼續新增</button>
```

---

## Responsive & Accessibility

- **Primary target:** desktop (1024px+). PSYDA is a B2B admin tool.
- **Mobile:** read-only ok; show "use desktop" notice for create/edit flows.
- **Contrast:** WCAG AA minimum (4.5:1 for text).
- **Focus visible:** `focus:ring-2 focus:ring-blue-500` on all interactive elements.
- **Keyboard:** Tab order, Esc to close modal, Enter to submit primary action.

---

## Stack

- **Tailwind CSS** (CDN for prototypes; PostCSS build for production)
- **Alpine.js v3** for interactivity (prototypes)
- **Production migration target:** Next.js + React + shadcn/ui (styles compatible)

---

## Appendix: Color Quick Lookup

```
Brand
  primary           bg-blue-600 text-blue-600
  primary-dark      bg-blue-700 text-blue-700
  primary-soft      bg-blue-100
  primary-tint      bg-blue-50

Neutral
  dark              text-slate-900   bg-slate-900
  dark-sec          text-slate-800
  muted             text-slate-500
  light             bg-slate-100
  border            border-slate-200

Semantic
  success           bg-emerald-500   text-emerald-600  bg-emerald-100 text-emerald-700
  info              bg-blue-500      text-blue-600     bg-blue-100 text-blue-700
  warning           bg-amber-500     text-amber-600    bg-amber-100 text-amber-700
  danger            bg-red-500       text-red-600      bg-red-100 text-red-700

Category stripes
  color-1 blue      bg-blue-500
  color-2 emerald   bg-emerald-500
  color-3 amber     bg-amber-500
  color-4 red       bg-red-500
  color-5 violet    bg-violet-500
```

---

*v2 — Engineer reference. For design rationale and case studies, see project repo.*
