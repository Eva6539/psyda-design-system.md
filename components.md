# Atomic Components

Copy-paste templates for each UI primitive. Each section: when to use + code.

## Button — Primary

Most important action on the page. Max 1-2 primary buttons per view.

```html
<button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 text-sm font-medium flex items-center gap-2">
  <svg class="w-4 h-4">...</svg>
  Save
</button>
```

## Button — Secondary

```html
<button class="px-4 py-2 bg-white border border-gray-300 rounded-lg hover:bg-gray-50 text-sm font-medium">
  Cancel
</button>
```

## Button — Danger

Only for destructive actions. Always pair with confirmation flow (see `patterns.md`).

```html
<button class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 text-sm font-medium">
  Delete
</button>
```

## Button — Ghost (table row actions)

```html
<button class="px-2 py-1 rounded text-xs text-gray-700 hover:bg-gray-100">
  Edit
</button>
```

## Button — Disabled state

```html
<button disabled class="px-4 py-2 bg-blue-600 text-white rounded-lg disabled:bg-gray-100 disabled:text-gray-400 disabled:cursor-not-allowed">
  Next
</button>
```

## Badge — Status pill

```html
<!-- Active -->
<span class="px-2 py-0.5 bg-green-100 text-green-700 rounded-full text-xs font-medium">進行中</span>

<!-- Draft -->
<span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded-full text-xs font-medium">未發布</span>

<!-- Closed -->
<span class="px-2 py-0.5 bg-slate-200 text-slate-500 rounded-full text-xs font-medium">已關閉</span>
```

## Badge — Tab counter

```html
<button class="px-4 py-2 rounded-lg bg-blue-600 text-white">
  Active
  <span class="px-1.5 py-0.5 rounded-full text-xs bg-white/20">5</span>
</button>
```

## Card — Standard

```html
<div class="bg-white border border-gray-200 rounded-xl p-5 hover:shadow-md transition">
  ...
</div>
```

## Card — Focus (emphasis)

Use for the primary card in a paired layout (e.g., right side of a 5:7 picker).

```html
<div class="border-2 border-blue-300 rounded-lg overflow-hidden shadow-sm">
  <div class="bg-blue-600 px-4 py-3 text-white">Title</div>
  <div class="p-4 bg-white">Content</div>
</div>
```

## Card — Left stripe (grouping)

```html
<div class="bg-white border border-gray-200 rounded-xl overflow-hidden flex">
  <div class="w-1.5 bg-blue-500"></div>
  <div class="flex-1 p-5">Content</div>
</div>
```

## Input — Text

```html
<label class="block text-sm font-medium mb-1">
  Name <span class="text-red-500">*</span>
</label>
<input type="text" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" />
<p class="text-xs text-gray-500 mt-1">Helper text</p>
```

## Input — Textarea

```html
<textarea rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
```

## Input — Select

```html
<select class="px-3 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 disabled:bg-gray-100 disabled:text-gray-400">
  <option value="">Choose...</option>
</select>
```

## Input — Search with clear button

```html
<div class="relative">
  <svg class="w-4 h-4 absolute left-3 top-1/2 -translate-y-1/2 text-gray-400">...</svg>
  <input x-model="search" type="text" placeholder="搜尋..."
         class="w-full pl-9 pr-9 py-2 border border-gray-300 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-blue-500" />
  <button x-show="search" @click="search = ''"
          class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-gray-700">
    <svg class="w-4 h-4">...</svg>
  </button>
</div>
```

## Modal — Full structure

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

    <!-- Scrollable body -->
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

## Table — Standard

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

## Alert — Info (blue)

Default for non-warning informational hints.

```html
<div class="bg-blue-50 border border-blue-200 rounded-lg p-3 flex items-start gap-2">
  <svg class="w-5 h-5 text-blue-600 flex-shrink-0 mt-0.5">...</svg>
  <div class="text-xs text-blue-800">Informational message</div>
</div>
```

## Alert — Warning (amber)

Only for "needs attention" or "deadline approaching". Never use for plain information.

```html
<div class="bg-amber-50 border border-amber-200 rounded-lg p-3 text-sm text-amber-800">
  Deadline approaching / action required
</div>
```

## Alert — Success (green)

```html
<div class="bg-green-50 border border-green-200 rounded-lg p-3 text-sm text-green-800">
  Saved successfully
</div>
```

## Empty state

```html
<div class="flex flex-col items-center justify-center py-12 text-gray-400">
  <svg class="w-10 h-10 mb-3 opacity-50">...</svg>
  <p class="text-sm">No items yet</p>
  <p class="text-xs mt-1">Click "Add" to create one</p>
</div>
```

## Toast

```html
<div x-show="toast" x-transition class="fixed bottom-6 right-6 bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg z-50 flex items-center gap-2">
  <svg class="w-5 h-5 text-green-400">...</svg>
  <span x-text="toast"></span>
</div>
```

Use toast for "save success" feedback. Don't use for errors — use inline alert in context.

## Toggle switch

```html
<button @click="enabled = !enabled" class="relative inline-flex h-5 w-9 items-center rounded-full transition" :class="enabled ? 'bg-blue-600' : 'bg-gray-300'">
  <span class="inline-block h-3.5 w-3.5 transform rounded-full bg-white transition" :class="enabled ? 'translate-x-5' : 'translate-x-1'"></span>
</button>
```

## Section header with stripe

```html
<h2 class="text-base font-bold flex items-center gap-2">
  <span class="w-1 h-5 bg-blue-600 rounded-full"></span>
  Section Title
</h2>
```

Variations: change `bg-blue-600` to `bg-emerald-600` or `bg-violet-600` to differentiate sections.
