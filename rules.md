# Rules & Anti-Patterns

Concrete do/don't rules. Each rule has code examples showing what to avoid and what to use instead.

## Colors

- Use Tailwind class names (`text-blue-600`). Never inline hex.
- Use `warning` (amber) only for content that needs attention or has a deadline.
- Use `info` (blue) for plain informational content.
- Max 3 saturated chips per row.

```html
<!-- ❌ Wrong: inline hex -->
<div style="color: #2563EB; background: #FEF3C7">...</div>

<!-- ✅ Right: Tailwind classes -->
<div class="text-blue-600 bg-amber-100">...</div>
```

```html
<!-- ❌ Wrong: warning for plain info -->
<div class="bg-amber-50 border border-amber-200 text-amber-800">
  This category's AI scoring guide: ...
</div>

<!-- ✅ Right: info blue -->
<div class="bg-blue-50 border border-blue-200 text-blue-800">
  This category's AI scoring guide: ...
</div>
```

```html
<!-- ❌ Wrong: three colored chips per item -->
<span class="bg-blue-100 text-blue-700">L1</span>
<span class="bg-green-100 text-green-700">L2</span>
<span class="bg-amber-100 text-amber-700">L3</span>

<!-- ✅ Right: plain breadcrumb text -->
<div class="text-xs text-gray-500">
  <span>L1</span> › <span>L2</span> › <span class="text-gray-700 font-medium">L3</span>
</div>
```

## Forms

- Use cascade dropdowns with `:disabled="!parent"` for nested levels.
- Use step modal for forms with 5+ fields or multiple concepts.
- Always show "Required" with red asterisk: `<span class="text-red-500">*</span>`.

```html
<!-- ❌ Wrong: allow user to skip parent level -->
<select x-model="l1">...</select>
<select x-model="l2">...</select> <!-- not disabled until l1 selected -->

<!-- ✅ Right: enforce cascade -->
<select x-model="l1" @change="l2 = ''">...</select>
<select x-model="l2" :disabled="!l1" class="... disabled:bg-gray-100 disabled:text-gray-400">...</select>
```

## Tech Jargon in Labels

Never expose developer terminology to end-users.

```html
<!-- ❌ Wrong: tech jargon -->
<label>Prompt</label>
<label>Skill ID</label>
<label>父分類</label>

<!-- ✅ Right: plain language -->
<label>AI evaluation guide</label>
<label>Linked skill (dropdown)</label>
<label>上層分類</label>
```

## Pickers (multi-item selection)

Use 5:7 grid layout. Right pane (selected items) gets more visual weight.

```html
<!-- ❌ Wrong: 50/50 layout -->
<div class="grid grid-cols-2 gap-4">
  <div>Source pool</div>
  <div>Selected</div>
</div>

<!-- ✅ Right: 5:7 with right pane emphasized -->
<div class="grid grid-cols-12 gap-4">
  <div class="col-span-5 bg-gray-50/30">Source pool</div>
  <div class="col-span-7 border-2 border-blue-300 shadow-sm">Selected</div>
</div>
```

```html
<!-- ❌ Wrong: cascade picker for selecting many items -->
<select>L1</select><select>L2</select><select>L3</select>
<!-- user repeats 30 times to add 10 items -->

<!-- ✅ Right: 5:7 picker with multi-select checkboxes -->
<!-- See patterns.md for full template -->
```

## Tables

- Never nest tables inside table cells.
- Replace nested data with "summary + expand" pattern.

```html
<!-- ❌ Wrong: nested table -->
<table>
  <tr>
    <td>Item</td>
    <td>
      <table>
        <tr><td>Sub L1</td><td>Sub L2</td></tr>
      </table>
    </td>
  </tr>
</table>

<!-- ✅ Right: summary with expand -->
<div>
  <div>Item · 12 sub-items · 4 categories</div>
  <button @click="expanded = !expanded">Expand</button>
  <div x-show="expanded">... sub items ...</div>
</div>
```

## Action Hierarchy

- Surface high-frequency actions as visible buttons.
- Hide only low-frequency or destructive actions in `⋮` menu.

```html
<!-- ❌ Wrong: hide primary actions in ⋮ -->
<div>
  <button>⋮</button>
  <menu>
    <item>View results</item>     <!-- primary action buried -->
    <item>Manage employees</item> <!-- primary action buried -->
    <item>Duplicate</item>
    <item>Delete</item>
  </menu>
</div>

<!-- ✅ Right: surface primary actions as buttons -->
<button class="bg-blue-600 text-white">View results</button>
<button class="border">Manage employees</button>
<button class="dropdown">⋮ (Duplicate / Delete)</button>
```

## Destructive Actions

- Confirm every delete with a modal.
- Offer a non-destructive alternative (e.g., "Disable").
- Show impact ("Will delete X dependent records").

```html
<!-- ❌ Wrong: one-click delete -->
<button @click="delete()">🗑</button>

<!-- ✅ Right: confirm + alternative -->
<button @click="confirmDelete()">🗑</button>

<!-- In modal -->
<div>
  <h3>Delete this item?</h3>
  <p>Will delete "Name" and 5 dependent records.</p>
  <div class="bg-yellow-50">Consider "Disable" instead — can be restored anytime.</div>
  <button>Cancel</button>
  <button>Disable instead</button>
  <button class="bg-red-600">Confirm delete</button>
</div>
```

## Markdown / Rich text

- Never expose raw markdown syntax (###, **, etc.) in user-facing inputs.
- Use a rich-text toolbar instead.

```html
<!-- ❌ Wrong: raw markdown in input -->
<textarea>### Header\n**bold text**</textarea>

<!-- ✅ Right: rich text toolbar -->
<div class="toolbar">
  <button><b>B</b></button>
  <button><i>I</i></button>
  <button>H1</button>
  <button>List</button>
</div>
<textarea>...</textarea>
```

## Modal Sizing

- Use `max-h-[90vh]` to prevent overflow.
- Body must be scrollable: `flex-1 overflow-y-auto`.
- Close on backdrop click: `@click.self="open = false"` on backdrop.

```html
<!-- ❌ Wrong: modal can overflow viewport -->
<div class="bg-white rounded-xl p-6">
  ... 100 form fields ...
</div>

<!-- ✅ Right: scrollable body with sticky header/footer -->
<div class="bg-white rounded-xl max-w-3xl w-full max-h-[90vh] overflow-hidden flex flex-col">
  <div class="px-6 py-4 border-b">Header (sticky)</div>
  <div class="flex-1 overflow-y-auto p-6">Body (scrollable)</div>
  <div class="px-6 py-4 border-t">Footer (sticky)</div>
</div>
```

## Empty States

- Always show icon + 1-line title + 1-line action hint.
- Never just show blank space.

```html
<!-- ❌ Wrong: blank area -->
<div></div>

<!-- ✅ Right: empty state with CTA -->
<div class="flex flex-col items-center py-12 text-gray-400">
  <svg class="w-10 h-10 opacity-50">...</svg>
  <p class="text-sm mt-3">No items yet</p>
  <p class="text-xs mt-1">Click "Add" to create one</p>
  <button class="mt-4 text-blue-600">+ Add first item</button>
</div>
```

## Loading & Feedback

- Use Toast for success feedback (save, delete).
- Don't use Toast for errors — use inline alert in context.
- Show pending state with `disabled:opacity-50 disabled:cursor-not-allowed`.

```html
<!-- ❌ Wrong: toast for error -->
<!-- Toast: "Error: validation failed on field X" -->

<!-- ✅ Right: inline alert beside the failed field -->
<input class="border-red-500" />
<p class="text-xs text-red-600 mt-1">This field is required</p>
```

## Typography

- Use `font-medium` (500) for labels.
- Use `font-semibold` (600) or `font-bold` (700) for headings.
- Never use `font-light` (300) for Chinese text.
- Use `tabular-nums` for numeric columns.

```html
<!-- ❌ Wrong: numbers don't align -->
<td>5.5</td>
<td>10.2</td>

<!-- ✅ Right: tabular-nums -->
<td class="tabular-nums">5.5</td>
<td class="tabular-nums">10.2</td>
```

## Spacing

- Use values from the spacing scale (p-3, p-4, p-5, p-6).
- Don't use arbitrary values unless absolutely necessary.

```html
<!-- ❌ Wrong: arbitrary value -->
<div class="p-[17px]">...</div>

<!-- ✅ Right: scale value -->
<div class="p-4">...</div>
```

## Localization (Chinese)

- Translate UI labels to natural Chinese, not English literal.

```html
<!-- ❌ Wrong: English literal -->
<button>儲存並創建另一個</button>  <!-- "Save and create another" -->

<!-- ✅ Right: natural Chinese -->
<button>儲存並繼續新增</button>
```

## Accessibility

- All interactive elements: `focus:ring-2 focus:ring-blue-500`.
- Use semantic HTML (`button`, `label`, `nav`, `main`).
- Never rely on color alone — pair with text or icon.
- Contrast: WCAG AA (4.5:1 for text).

```html
<!-- ❌ Wrong: color-only indicator -->
<span class="text-red-600">High risk</span>
<span class="text-green-600">Low risk</span>

<!-- ✅ Right: color + icon -->
<span class="text-red-600 flex items-center gap-1">
  <svg>⚠</svg>
  High risk
</span>
```

## Shadow & Opacity

- Use `opacity` prop on shadows, never encode in 8-char hex.

```html
<!-- ❌ Wrong: 8-char hex (corrupts in some libraries) -->
<div style="box-shadow: 0 2px 6px #00000020"></div>

<!-- ✅ Right: opacity prop -->
<div class="shadow-md"></div>
<!-- or in JS: { color: "000000", opacity: 0.12 } -->
```
