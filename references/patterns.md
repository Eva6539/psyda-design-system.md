# Composite Patterns

Higher-order patterns assembled from atomic components.

## Step Modal

Use when a form has 5+ fields or covers multiple concepts. Max 5 steps.

### Step indicator (in modal header)

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

### Step footer

```html
<div class="px-6 py-4 border-t border-gray-200 flex items-center justify-between">
  <button @click="current--" :disabled="current === 0"
          class="px-4 py-2 text-sm border border-gray-300 rounded-lg disabled:opacity-40 disabled:cursor-not-allowed">
    Back
  </button>
  <span class="text-xs text-gray-500" x-text="(current + 1) + ' / ' + steps.length"></span>
  <button @click="nextStep()" class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm">
    <span x-show="current < steps.length - 1">Next</span>
    <span x-show="current === steps.length - 1">Finish</span>
  </button>
</div>
```

---

## Picker — 5:7 dual pane

Use when selecting items from a pool into a list. Right side (selected) gets more visual weight.

```html
<div class="grid grid-cols-12 gap-4 h-[28rem]">
  <!-- Left: source pool (5/12, visually light) -->
  <div class="col-span-5 border border-gray-200 rounded-lg flex flex-col overflow-hidden bg-gray-50/30">
    <div class="bg-gray-50 border-b border-gray-200 p-2">
      <!-- Search + filters -->
    </div>
    <div class="flex-1 overflow-y-auto p-2">
      <!-- Checkbox items -->
      <template x-for="item in poolItems">
        <label class="flex items-start gap-2 p-2 hover:bg-white rounded cursor-pointer border border-transparent hover:border-gray-300">
          <input type="checkbox" :checked="selected.includes(item.id)" @change="toggleSelect(item.id)" class="mt-1" />
          <div class="flex-1 text-xs">
            <!-- Breadcrumb -->
            <div class="text-[10px] text-gray-500 mb-1">
              <span x-text="item.l1"></span> ›
              <span x-text="item.l2"></span> ›
              <span class="text-gray-700 font-medium" x-text="item.l3"></span>
            </div>
            <div class="text-gray-800" x-text="item.content"></div>
          </div>
        </label>
      </template>
    </div>
  </div>

  <!-- Right: selected list (7/12, visual focus) -->
  <div class="col-span-7 border-2 border-blue-300 rounded-lg flex flex-col overflow-hidden shadow-sm">
    <div class="bg-blue-600 px-4 py-3 flex items-center justify-between text-white">
      <span class="text-sm font-semibold">Selected (<span x-text="selected.length"></span>)</span>
      <button @click="selected = []" x-show="selected.length > 0" class="text-xs text-white/90 hover:underline">Clear all</button>
    </div>
    <div class="flex-1 overflow-y-auto p-3 space-y-2 bg-white">
      <template x-for="(id, idx) in selected">
        <div class="flex items-start gap-3 p-3 bg-blue-50/40 border border-blue-100 rounded-lg">
          <span class="inline-flex items-center justify-center w-6 h-6 rounded-full bg-blue-600 text-white text-xs font-bold flex-shrink-0" x-text="(idx+1).toString().padStart(2,'0')"></span>
          <div class="flex-1 text-sm" x-text="findItem(id).content"></div>
          <button @click="toggleSelect(id)" class="text-gray-400 hover:text-red-600">
            <svg class="w-4 h-4">...</svg>
          </button>
        </div>
      </template>
    </div>
  </div>
</div>
```

---

## Cascade Dropdowns (3 levels)

```html
<div class="grid grid-cols-3 gap-2">
  <select x-model="l1" @change="l2 = ''; l3 = ''"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
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

### Alpine methods

```js
get l1Options() { return [...new Set(items.map(i => i.l1))]; },
l2Options(l1) { return [...new Set(items.filter(i => i.l1 === l1).map(i => i.l2))]; },
l3Options(l1, l2) { return [...new Set(items.filter(i => i.l1 === l1 && i.l2 === l2).map(i => i.l3))]; },
```

---

## Filter Chips (applied conditions)

```html
<div x-show="search || filterA || filterB" class="flex flex-wrap items-center gap-1">
  <span class="text-[10px] text-gray-500">已套用：</span>
  <span x-show="search" class="inline-flex items-center gap-0.5 px-1.5 py-0.5 bg-white border border-gray-300 text-gray-700 rounded text-[10px]">
    關鍵字「<span x-text="search"></span>」
    <button @click="search = ''" class="hover:text-gray-900 ml-0.5">×</button>
  </span>
  <span x-show="filterA" class="inline-flex items-center gap-0.5 px-1.5 py-0.5 bg-white border border-gray-300 text-gray-700 rounded text-[10px]">
    <span x-text="filterA"></span>
    <button @click="filterA = ''" class="hover:text-gray-900 ml-0.5">×</button>
  </span>
  <button @click="clearAll()" class="text-[10px] text-gray-500 hover:underline ml-1">清除全部</button>
</div>
```

**Rule:** all chips use the same color (gray). Do NOT color-code by filter type.

---

## Batch Operation Bar

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

---

## Action Menu (three-dot)

Use ONLY for low-frequency or destructive actions. High-frequency actions belong as visible buttons.

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

---

## Delete Confirmation

Required for ANY destructive action. Always offer a non-destructive alternative.

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

---

## Progress Bar with Color Threshold

For showing values with colored bands (completion %, scores, risk levels).

```html
<div class="text-sm font-medium" x-text="value + ' / ' + total"></div>
<div class="w-full bg-gray-200 rounded-full h-1.5 mt-1.5">
  <div class="h-1.5 rounded-full transition-all"
       :class="ratio >= 0.7 ? 'bg-green-500' : ratio >= 0.3 ? 'bg-blue-500' : 'bg-amber-500'"
       :style="`width: ${ratio * 100}%`"></div>
</div>
```

---

## Days Remaining Indicator

```html
<div class="text-xs font-medium"
     :class="daysLeft < 3 ? 'text-red-600' :
             daysLeft < 7 ? 'text-amber-600' : 'text-gray-500'"
     x-text="daysLeft > 0 ? `Remaining ${daysLeft} days` : 'Ended'">
</div>
```

---

## Category Path Breadcrumb

For multi-level categories. Use plain text — NOT colored chips.

```html
<!-- Correct: plain breadcrumb -->
<div class="text-xs text-gray-500">
  <span x-text="l1"></span> ›
  <span x-text="l2"></span> ›
  <span class="text-gray-700 font-medium" x-text="l3"></span>
</div>
```

See `rules.md` for the anti-pattern (colored chips per level).

---

## Status Tabs with Counts

```html
<div class="flex items-center gap-1">
  <template x-for="tab in tabs">
    <button @click="active = tab.key"
            :class="active === tab.key ? 'bg-blue-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200'"
            class="px-4 py-2 rounded-lg text-sm font-medium flex items-center gap-2">
      <span x-text="tab.label"></span>
      <span :class="active === tab.key ? 'bg-white/20' : 'bg-white'"
            class="px-1.5 py-0.5 rounded-full text-xs"
            x-text="countByStatus(tab.key)"></span>
    </button>
  </template>
</div>
```

---

## View Mode Toggle (card / table)

```html
<div class="flex items-center bg-gray-100 rounded-lg p-1">
  <button @click="view = 'card'" :class="view === 'card' ? 'bg-white shadow text-blue-600' : 'text-gray-600'"
          class="px-3 py-1.5 rounded-md text-sm font-medium transition">Card</button>
  <button @click="view = 'table'" :class="view === 'table' ? 'bg-white shadow text-blue-600' : 'text-gray-600'"
          class="px-3 py-1.5 rounded-md text-sm font-medium transition">Table</button>
</div>
```
