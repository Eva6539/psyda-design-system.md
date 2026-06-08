---
name: psyda-design-system
description: PSYDA 心理測評題庫管理系統的 UI/UX 設計規範。Use when designing or implementing UI components for the PSYDA platform — including color palette, typography, spacing, component patterns (cards, buttons, badges, modals, tables), interaction patterns (step forms, cascade dropdowns, batch operations, dual-pane pickers), and anti-patterns to avoid. Provides ready-to-copy Tailwind CSS class combinations and Alpine.js patterns.
---

# PSYDA 設計系統

> 為「沒有資訊背景的一般用戶（HR、輔導老師、行政人員）」打造的後台管理體驗。

本文件記錄了 PSYDA 心理測評題庫管理系統的視覺與互動規範。所有規則都從**降低非技術用戶的使用門檻**這個核心目標推導而來。

---

## 1. 核心設計原則

| 原則 | 說明 | 反例 |
|------|------|------|
| **說人話** | 所有界面用語以 HR、老師、行政人員的日常語言為準 | 「Prompt」「技能 ID」「父分類」 |
| **Excel 為師** | 表格化呈現、匯入匯出、批次操作對齊用戶熟悉的工作流 | 樹狀結構、級聯下拉、單筆操作 |
| **所見即所得** | 視覺化參數、即時預覽、可試聽，讓設定結果立刻可感 | 純數字輸入、無預覽、無回饋 |
| **安全網** | 刪除確認、預設「停用」取代「刪除」、操作後即時回饋 | 一鍵刪除、無確認、無撤銷 |
| **AI 輔助** | 導入 AI 生成、自動填寫，把繁瑣工作降到最低 | 強迫用戶手寫所有內容 |

---

## 2. 色彩系統

### 2.1 主色（Brand）

| Token | Hex | Tailwind | 用途 |
|-------|-----|----------|------|
| `primary` | `#2563EB` | `blue-600` | 主要 CTA、品牌色、active 狀態 |
| `primary-dark` | `#1E40AF` | `blue-700` | 主要 CTA hover、強調文字 |
| `primary-soft` | `#DBEAFE` | `blue-100` | 背景強調、活躍區塊 |
| `primary-tint` | `#EFF6FF` | `blue-50` | 最淺背景、hover 區 |

### 2.2 中性色（Neutral）

| Token | Hex | Tailwind | 用途 |
|-------|-----|----------|------|
| `dark` | `#0F172A` | `slate-900` | 章節分隔頁背景、最重文字 |
| `dark-sec` | `#1E293B` | `slate-800` | 主要文字 |
| `muted` | `#64748B` | `slate-500` | 輔助文字、說明、placeholder |
| `light` | `#F1F5F9` | `slate-100` | 卡片背景、區塊區隔 |
| `border` | `#E2E8F0` | `slate-200` | 邊框 |
| `white` | `#FFFFFF` | `white` | 主背景、白卡 |

### 2.3 語意色（Semantic）

| Token | Hex | Tailwind | 用途 | **絕不能用在** |
|-------|-----|----------|------|-------------|
| `success` | `#10B981` | `emerald-500` | 成功、完成、進行中 | 一般資訊 |
| `info` | `#3B82F6` | `blue-500` | 資訊提示、補充說明 | 動作按鈕（用 primary） |
| `warning` | `#F59E0B` | `amber-500` | 警告、即將截止 | 純資訊（會嚇到用戶）|
| `danger` | `#EF4444` | `red-500` | 錯誤、刪除、嚴重風險 | 一般強調 |

**重要規則**：`warning` 黃色只用在「需要注意、可能後悔」的場景。**單純展示資訊一律用 `info` 藍色**，這是業主明確指出的設計失誤。

### 2.4 分類色條（Category Stripes）

群組列表的左側色條，用於視覺分群（最多 5 種，循環使用）：

```css
.color-1 { background: #3b82f6; }  /* 藍 */
.color-2 { background: #10b981; }  /* 綠 */
.color-3 { background: #f59e0b; }  /* 琥珀 */
.color-4 { background: #ef4444; }  /* 紅 */
.color-5 { background: #8b5cf6; }  /* 紫 */
```

**避免**：把這些色條同時用在文字標籤上，會造成「彩虹頁」視覺疲勞。

### 2.5 配色禁忌

```
❌ 一列內出現超過 3 個飽和色塊（L1 藍 + L2 綠 + L3 橘 = 視覺噪音）
❌ 用 warning 黃色當作 info 提示
❌ 用紅色強調非危險的訊息
❌ 同一頁面使用 5+ 種飽和色

✅ 麵包屑用文字 + 灰色分隔符
✅ 一頁只有 1 個主色 + 適度語意色
✅ 用「色塊重量」（淺背景 / 邊框 / 文字色）做層次
```

---

## 3. 字型與字級

### 3.1 字型家族

```css
font-family: -apple-system, BlinkMacSystemFont, "PingFang TC",
             "Microsoft JhengHei", sans-serif;
```

繁體中文：`PingFang TC`（Mac）/ `Microsoft JhengHei`（Windows）
簡體中文：`PingFang SC` / `Microsoft YaHei`

### 3.2 字級階層

| 層級 | 字級 | Tailwind | 行高 | 用途 |
|------|------|----------|------|------|
| 主標題 | 28px | `text-2xl` | `leading-tight` | 頁面標題 |
| 區段標題 | 20px | `text-xl` | `leading-snug` | 卡片標題、區塊標題 |
| 子標題 | 16px | `text-base` | `leading-normal` | 欄位 label、表格表頭 |
| 內文 | 14px | `text-sm` | `leading-relaxed` | 一般文字 |
| 說明文字 | 12px | `text-xs` | `leading-normal` | 輔助說明、metadata |
| 微標籤 | 10px | `text-[10px]` | `leading-tight` | 標籤、計數、chip |

### 3.3 字重

- `font-normal` (400)：內文
- `font-medium` (500)：欄位 label
- `font-semibold` (600)：區段標題、表格表頭
- `font-bold` (700)：主標題、強調數字

**避免**：用 `font-light` (300) 顯示中文（中文細體可讀性差）。

---

## 4. 間距系統

### 4.1 間距尺度（沿用 Tailwind 預設）

| Tailwind | 用途 |
|----------|------|
| `gap-1` (4px) | 緊密元件（icon + 文字） |
| `gap-2` (8px) | 標籤群、按鈕群 |
| `gap-3` (12px) | 表單欄位垂直 |
| `gap-4` (16px) | 卡片內區塊 |
| `gap-6` (24px) | 區段間 |

### 4.2 卡片內距

| 卡片大小 | padding | Tailwind |
|---------|---------|----------|
| 緊湊（列表項） | 8-12px | `p-2` / `p-3` |
| 標準（內容卡） | 16-20px | `p-4` / `p-5` |
| 寬鬆（焦點卡） | 24-32px | `p-6` / `p-8` |

### 4.3 圓角

- `rounded` (4px)：表單輸入、chip
- `rounded-lg` (8px)：卡片、按鈕、modal
- `rounded-xl` (12px)：主要卡片、彈窗
- `rounded-full`：頭像、徽章圓點

---

## 5. 元件規範

### 5.1 按鈕（Buttons）

**Primary（主要動作，每頁最多 1-2 個）**
```html
<button class="px-4 py-2 bg-blue-600 text-white rounded-lg
               hover:bg-blue-700 text-sm font-medium
               flex items-center gap-2">
  <svg class="w-4 h-4">...</svg>
  建立群組
</button>
```

**Secondary（次要動作）**
```html
<button class="px-4 py-2 bg-white border border-gray-300 rounded-lg
               hover:bg-gray-50 text-sm font-medium
               flex items-center gap-2">
  匯入 Excel
</button>
```

**Danger（危險動作，需配確認流程）**
```html
<button class="px-4 py-2 bg-red-600 text-white rounded-lg
               hover:bg-red-700 text-sm font-medium">
  確認刪除
</button>
```

**Ghost（淡按鈕，table row 內動作）**
```html
<button class="px-2 py-1 rounded text-xs text-gray-700 hover:bg-gray-100">
  編輯
</button>
```

**禁用狀態**
```html
<button disabled class="px-4 py-2 bg-blue-600 text-white rounded-lg
                        disabled:bg-gray-100 disabled:text-gray-400
                        disabled:cursor-not-allowed">
  下一步
</button>
```

### 5.2 徽章（Badges / Status Pills）

**狀態徽章**
```html
<!-- 進行中 -->
<span class="px-2 py-0.5 bg-green-100 text-green-700 rounded-full
             text-xs font-medium">進行中</span>

<!-- 未發布 -->
<span class="px-2 py-0.5 bg-gray-100 text-gray-600 rounded-full
             text-xs font-medium">未發布</span>

<!-- 已關閉 -->
<span class="px-2 py-0.5 bg-slate-200 text-slate-500 rounded-full
             text-xs font-medium">已關閉</span>
```

**計數徽章（搭配 tab）**
```html
<button class="px-4 py-2 rounded-lg bg-blue-600 text-white">
  進行中
  <span class="px-1.5 py-0.5 rounded-full text-xs bg-white/20">5</span>
</button>
```

### 5.3 卡片（Cards）

**標準卡片（白底 + 邊框）**
```html
<div class="bg-white border border-gray-200 rounded-xl p-5
            hover:shadow-md transition">
  ... 內容 ...
</div>
```

**焦點卡片（藍邊強調）**
```html
<div class="border-2 border-blue-300 rounded-lg overflow-hidden shadow-sm">
  <div class="bg-blue-600 px-4 py-3 text-white">標題</div>
  <div class="p-4 bg-white">內容</div>
</div>
```

**左色條分群卡片**
```html
<div class="bg-white border border-gray-200 rounded-xl overflow-hidden flex">
  <div class="w-1.5 bg-blue-500"></div>
  <div class="flex-1 p-5">... 內容 ...</div>
</div>
```

### 5.4 表單輸入

**標準輸入框**
```html
<label class="block text-sm font-medium mb-1">
  群組名稱 <span class="text-red-500">*</span>
</label>
<input type="text"
       class="w-full px-3 py-2 border border-gray-300 rounded-lg
              text-sm focus:outline-none focus:ring-2 focus:ring-blue-500
              focus:border-transparent" />
<p class="text-xs text-gray-500 mt-1">輔助說明文字</p>
```

**Textarea**
```html
<textarea rows="3"
          class="w-full px-3 py-2 border border-gray-300 rounded-lg
                 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
```

**Select（級聯下拉）**
```html
<select class="px-3 py-2 border border-gray-300 rounded-lg text-sm
               focus:outline-none focus:ring-2 focus:ring-blue-500
               disabled:bg-gray-100 disabled:text-gray-400">
  <option value="">全部第一層</option>
  <option>校園心理測評</option>
</select>
```

### 5.5 Modal（彈窗）

**標準 Modal 結構**
```html
<div class="fixed inset-0 bg-black/50 z-50
            flex items-center justify-center p-4">
  <div class="bg-white rounded-xl shadow-2xl
              max-w-3xl w-full max-h-[90vh]
              overflow-hidden flex flex-col">

    <!-- Header -->
    <div class="px-6 py-4 border-b border-gray-200
                flex items-center justify-between">
      <h2 class="text-lg font-bold">彈窗標題</h2>
      <button class="p-1 hover:bg-gray-100 rounded">×</button>
    </div>

    <!-- Body (可捲動) -->
    <div class="flex-1 overflow-y-auto p-6 space-y-4">
      ... 內容 ...
    </div>

    <!-- Footer -->
    <div class="px-6 py-4 border-t border-gray-200
                flex items-center justify-end gap-2">
      <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg">取消</button>
      <button class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm">儲存</button>
    </div>
  </div>
</div>
```

### 5.6 表格

**標準表格**
```html
<table class="w-full text-sm">
  <thead class="bg-gray-50 border-b border-gray-200 text-left">
    <tr>
      <th class="px-4 py-3 font-medium text-gray-700">欄位</th>
    </tr>
  </thead>
  <tbody>
    <tr class="border-b border-gray-100 hover:bg-blue-50/30">
      <td class="px-4 py-3">資料</td>
    </tr>
  </tbody>
</table>
```

**禁忌**：表格內不要再嵌套表格。需要展示層級時用「摘要 + 展開」模式。

### 5.7 提示框（Info / Warning / Success）

**Info（藍色，預設用於資訊性提示）**
```html
<div class="bg-blue-50 border border-blue-200 rounded-lg p-3
            flex items-start gap-2">
  <svg class="w-5 h-5 text-blue-600 flex-shrink-0 mt-0.5">...</svg>
  <div class="text-xs text-blue-800">補充說明文字</div>
</div>
```

**Warning（黃色，僅用於需要注意的事項）**
```html
<div class="bg-amber-50 border border-amber-200 rounded-lg p-3 text-sm
            text-amber-800">
  即將截止 / 操作後不可復原
</div>
```

**Success（綠色，操作成功確認）**
```html
<div class="bg-green-50 border border-green-200 rounded-lg p-3 text-sm
            text-green-800">
  已成功儲存
</div>
```

### 5.8 空狀態（Empty State）

```html
<div class="flex flex-col items-center justify-center py-12 text-gray-400">
  <svg class="w-10 h-10 mb-3 opacity-50">...</svg>
  <p class="text-sm">尚未選擇任何題目</p>
  <p class="text-xs mt-1">請從左側題庫勾選想加入的題目</p>
</div>
```

### 5.9 Toast（操作回饋）

```html
<div class="fixed bottom-6 right-6
            bg-gray-900 text-white px-4 py-3 rounded-lg shadow-lg
            z-50 flex items-center gap-2">
  <svg class="w-5 h-5 text-green-400">...</svg>
  <span>已成功儲存</span>
</div>
```

---

## 6. 互動模式

### 6.1 步驟式表單（Step Modal）

當一個表單超過 5 個欄位或涉及多個概念，**拆成步驟**。

**步驟指示器**
```html
<div class="px-6 py-4 bg-gray-50 border-b border-gray-200">
  <div class="flex items-center justify-between">
    <!-- 已完成步驟 -->
    <div class="flex items-center gap-2">
      <div class="w-8 h-8 rounded-full bg-emerald-500 text-white
                  flex items-center justify-center text-sm">
        ✓
      </div>
      <span class="text-sm text-gray-500">基本資料</span>
    </div>
    <div class="flex-1 h-px bg-gray-300 mx-3"></div>
    <!-- 進行中 -->
    <div class="flex items-center gap-2">
      <div class="w-8 h-8 rounded-full bg-blue-600 text-white
                  flex items-center justify-center text-sm">2</div>
      <span class="text-sm font-medium text-blue-600">選擇題目</span>
    </div>
    <!-- ... 後續步驟用 bg-gray-200 text-gray-500 ... -->
  </div>
</div>
```

**步驟按鈕（footer）**
```html
<div class="px-6 py-4 border-t border-gray-200 flex items-center justify-between">
  <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg"
          :disabled="step === 0">上一步</button>
  <span class="text-xs text-gray-500">2 / 4</span>
  <button class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm">
    下一步
  </button>
</div>
```

**經驗值**：步驟數 3-5 個最佳。超過 5 個用戶會放棄。

### 6.2 批次操作列（Batch Operation Bar）

當用戶勾選列表中的項目，頂部出現浮動操作列。

```html
<div x-show="selectedIds.length > 0"
     class="bg-blue-50 border border-blue-200 rounded-lg p-3
            flex items-center justify-between">
  <div class="text-sm text-blue-900">
    已選取 <span class="font-bold" x-text="selectedIds.length"></span> 個項目
  </div>
  <div class="flex items-center gap-2">
    <button class="px-3 py-1.5 bg-white border border-gray-300
                   rounded-md text-sm hover:bg-gray-50">批次啟用</button>
    <button class="px-3 py-1.5 bg-white border border-red-300
                   text-red-600 rounded-md text-sm
                   hover:bg-red-50">批次刪除</button>
    <button class="text-sm text-gray-600 px-2"
            @click="selectedIds = []">取消</button>
  </div>
</div>
```

### 6.3 級聯下拉（Cascade Dropdowns）

選了上層才啟用下層，提供清楚的視覺禁用狀態。

```html
<div class="grid grid-cols-3 gap-2">
  <select x-model="level1"
          @change="level2 = ''; level3 = ''"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm">
    <option value="">第一層</option>
    <template x-for="opt in level1Options">
      <option :value="opt" x-text="opt"></option>
    </template>
  </select>

  <select x-model="level2"
          :disabled="!level1"
          @change="level3 = ''"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm
                 disabled:bg-gray-100 disabled:text-gray-400">
    <option value="">第二層</option>
    <template x-for="opt in level2OptionsFor(level1)">
      <option :value="opt" x-text="opt"></option>
    </template>
  </select>

  <select x-model="level3"
          :disabled="!level2"
          class="px-3 py-2 border border-gray-300 rounded-lg text-sm
                 disabled:bg-gray-100 disabled:text-gray-400">
    <option value="">第三層</option>
    <template x-for="opt in level3OptionsFor(level1, level2)">
      <option :value="opt" x-text="opt"></option>
    </template>
  </select>
</div>
```

**Alpine 對應方法**
```js
level1Options: [...new Set(items.map(i => i.level1))],
level2OptionsFor(l1) {
  return [...new Set(items.filter(i => i.level1 === l1).map(i => i.level2))];
},
```

### 6.4 雙欄選擇器（5:7 Picker）

從一個池子挑東西進另一個列表的場景，**左 5 / 右 7 比例**，讓「已選」視覺更重。

```html
<div class="grid grid-cols-12 gap-4 h-[28rem]">
  <!-- 左：來源池（5/12，視覺輕量） -->
  <div class="col-span-5 border border-gray-200 rounded-lg flex flex-col
              overflow-hidden bg-gray-50/30">
    <div class="bg-gray-50 border-b border-gray-200 p-2">
      ... 搜尋 + 篩選 ...
    </div>
    <div class="flex-1 overflow-y-auto p-2">
      ... 可勾選項目 ...
    </div>
  </div>

  <!-- 右：已選列表（7/12，視覺主角） -->
  <div class="col-span-7 border-2 border-blue-300 rounded-lg flex flex-col
              overflow-hidden shadow-sm">
    <div class="bg-blue-600 px-4 py-3 text-white">已選項目</div>
    <div class="flex-1 overflow-y-auto p-3 bg-white">
      ... 已選項目卡片 ...
    </div>
  </div>
</div>
```

**為什麼 5:7？**：使用者注意力應放在「已選」這個結果上，給它較多視覺重量。

### 6.5 搜尋 + 篩選 + 條件 chip

複雜列表需要支援：關鍵字搜尋、級聯篩選、清除條件。

```html
<!-- 條件 chip（已套用篩選） -->
<div x-show="search || filterA || filterB"
     class="flex flex-wrap items-center gap-1">
  <span class="text-[10px] text-gray-500">已套用：</span>
  <span class="inline-flex items-center gap-0.5 px-1.5 py-0.5
               bg-white border border-gray-300 text-gray-700
               rounded text-[10px]">
    關鍵字「<span x-text="search"></span>」
    <button @click="search = ''">×</button>
  </span>
  <!-- ... 每個條件一個 chip ... -->
  <button @click="clearAll()" class="text-[10px] text-gray-500 hover:underline">
    清除全部
  </button>
</div>
```

**配色規則**：所有 chip 用同一個（灰邊白底）顏色，**不要**用多色區分條件類型。

### 6.6 麵包屑分類路徑

呈現多層分類時，**用文字 + 分隔符**，不要用多色色塊。

```html
<!-- ✅ 對：純文字麵包屑（不喧賓奪主） -->
<div class="text-xs text-gray-500">
  <span>校園心理測評</span> ›
  <span>情緒壓力</span> ›
  <span class="text-gray-700 font-medium">壓力預防</span>
</div>

<!-- ❌ 錯：三個色塊（視覺噪音） -->
<div>
  <span class="bg-blue-100 text-blue-700">校園心理測評</span>
  <span class="bg-green-100 text-green-700">情緒壓力</span>
  <span class="bg-amber-100 text-amber-700">壓力預防</span>
</div>
```

### 6.7 進度視覺化

數字 + 進度條 + 顏色階梯，比純百分比更直覺。

```html
<div class="bg-gray-50 rounded-lg p-3">
  <div class="text-xs text-gray-500 mb-1">受測進度</div>
  <div class="text-sm font-medium">3 / 10 人完成</div>
  <div class="w-full bg-gray-200 rounded-full h-1.5 mt-1.5">
    <!-- 30% 完成度，顏色依進度變化 -->
    <div class="bg-amber-500 h-1.5 rounded-full" style="width: 30%"></div>
    <!-- ≥70%: bg-green-500, 30-70%: bg-blue-500, <30%: bg-amber-500 -->
  </div>
  <div class="text-xs text-gray-500 mt-0.5">30% 完成率</div>
</div>
```

### 6.8 倒數警示

```html
<div class="text-xs font-medium"
     :class="daysLeft < 3 ? 'text-red-600' :
            (daysLeft < 7 ? 'text-amber-600' : 'text-gray-500')"
     x-text="daysLeft > 0 ? '還剩 ' + daysLeft + ' 天' : '已結束'">
</div>
```

### 6.9 刪除確認流程

刪除是高風險動作，**至少要有確認 + 替代選項**。

```html
<div class="bg-white rounded-xl shadow-2xl max-w-md p-6">
  <div class="flex items-start gap-3 mb-4">
    <div class="w-10 h-10 bg-red-100 rounded-full flex items-center justify-center">
      <svg class="w-5 h-5 text-red-600">...</svg>
    </div>
    <div>
      <h3 class="font-bold mb-1">確定要刪除這個分類嗎？</h3>
      <p class="text-sm text-gray-600">
        將刪除「<span class="font-medium">壓力預防</span>」
        <span class="text-red-600 font-medium">
          此分類下還有 3 道題目，題目將一併移到「未分類」
        </span>
      </p>
    </div>
  </div>
  <!-- 提供替代方案 -->
  <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-3
              text-sm text-yellow-800 mb-4">
    建議改用「停用」取代刪除，停用後可隨時恢復
  </div>
  <!-- 三個選項：取消 / 改為停用 / 確認刪除 -->
  <div class="flex items-center justify-end gap-2">
    <button class="px-4 py-2 text-sm border border-gray-300 rounded-lg">取消</button>
    <button class="px-4 py-2 text-sm bg-gray-600 text-white rounded-lg">改為停用</button>
    <button class="px-4 py-2 text-sm bg-red-600 text-white rounded-lg">確認刪除</button>
  </div>
</div>
```

### 6.10 動作分層

把動作按使用頻率分三層，**核心動作不該藏在 ⋮ 選單**。

| 層級 | 呈現方式 | 範例 |
|------|---------|------|
| **主動作（每天用）** | 顯眼按鈕（藍色 / 主色） | 查看結果、受測員工 |
| **次要動作（偶爾用）** | ⋮ 選單 | 複製、管理範本 |
| **危險動作（罕用）** | ⋮ 選單最下方（紅字） | 刪除 |

---

## 7. Anti-patterns（避免事項）

| ❌ 不要 | ✅ 應該 |
|---------|---------|
| 「Prompt 提示語」 | 「AI 評估指引」 |
| 「父分類」 | 「上層分類」或「歸屬於」 |
| 「技能 ID」要用戶填 | 改成下拉選單，由系統管理 |
| 開發者語言（API、Endpoint） | 用業務語言（送出、儲存、發布） |
| 巢狀表格 | 摘要 + 展開模式 |
| 把主操作藏在 ⋮ | 拉出來作按鈕 |
| 用 warning 色顯示資訊 | 用 info 藍色 |
| 一鍵刪除無確認 | 確認彈窗 + 替代方案 |
| 全文字輸入時間 | 視覺化時間軸 |
| 級聯下拉建大量項目 | 雙欄勾選 + 批次 |
| 預設 markdown 暴露 `###` | 富文本工具列 |
| 表格內所有字同大小 | 主資料粗體、metadata 淺色 |
| 同列出現 3+ 飽和色塊 | 統一灰色麵包屑 |
| 「儲存並創建另一個」（直譯英文） | 「儲存並繼續新增」 |

---

## 8. 響應式與無障礙

### 8.1 斷點

```css
sm: 640px   /* 平板直立 */
md: 768px   /* 平板橫向 */
lg: 1024px  /* 桌機 */
xl: 1280px  /* 大桌機 */
```

**桌面後台優先**：PSYDA 是 B2B 後台系統，桌機為主。手機版只需保證**檢視**功能可用，建立與編輯允許跳出「請使用桌機」提示。

### 8.2 對比度

- 文字 / 背景：至少 WCAG AA（4.5:1）
- 大標題：至少 3:1
- 互動元素：聚焦狀態（focus）需明顯（`focus:ring-2 focus:ring-blue-500`）

### 8.3 鍵盤操作

- 所有按鈕 / 連結可 Tab 到
- Modal 開啟時 trap focus
- Esc 關閉 modal
- Enter 提交表單主動作

---

## 9. 命名與檔案結構

### 9.1 元件命名

- 卡片：`Card`、`StatCard`、`QuestionCard`
- 列表項：`Item`、`Row`、`ListItem`
- 彈窗：`Modal`、`Dialog`、`ConfirmModal`
- 表單：`FormField`、`InputField`、`SelectField`

### 9.2 CSS 類別命名（如有自訂）

採用 BEM-like 結構，但盡量用 Tailwind utility：

```css
.timeline-bar { ... }
.timeline-bar__segment { ... }
.timeline-bar__segment--think { ... }
```

---

## 10. 完整範例：題目卡片

把所有原則組合成一個完整範例：

```html
<div class="question-card bg-white border border-gray-200 rounded-xl p-5
            hover:shadow-md transition">
  <!-- 1. 頂部：勾選 + 分類路徑 + 啟用 -->
  <div class="flex items-start justify-between mb-3">
    <div class="flex items-start gap-2 flex-1">
      <input type="checkbox" class="mt-1 rounded" />
      <!-- 麵包屑（純文字） -->
      <div class="text-xs text-gray-500">
        <span>校園心理測評</span> ›
        <span>情緒壓力</span> ›
        <span class="text-gray-700 font-medium">壓力預防</span>
      </div>
    </div>
    <!-- 啟用 toggle -->
    <button class="relative inline-flex h-5 w-9 items-center rounded-full
                   bg-blue-600">
      <span class="inline-block h-3.5 w-3.5 rounded-full bg-white
                   transform translate-x-5"></span>
    </button>
  </div>

  <!-- 2. 題目內容（最重要，最大字） -->
  <div class="mb-4 text-gray-800 leading-relaxed">
    請描述你最近一週的主要壓力來源，以及這些壓力如何影響你的心情？
  </div>

  <!-- 3. 時間軸視覺化 -->
  <div class="mb-4">
    <div class="text-xs text-gray-500 mb-1 flex justify-between">
      <span>題目播報 → 思考 10s → 答題 30s</span>
      <span class="text-red-600">最少 20s 才可跳過</span>
    </div>
    <!-- 時間軸 bar ... -->
  </div>

  <!-- 4. 底部：語音 + 操作 -->
  <div class="flex items-center justify-between pt-3 border-t border-gray-100">
    <button class="flex items-center gap-1.5 text-xs text-blue-600
                   hover:bg-blue-50 rounded px-2 py-1">
      <svg class="w-3.5 h-3.5">...</svg>
      女聲 · 台灣 · 試聽
    </button>
    <div class="flex items-center gap-1">
      <button class="p-1.5 hover:bg-gray-100 rounded text-blue-600">編輯</button>
      <button class="p-1.5 hover:bg-red-50 rounded text-red-600">刪除</button>
    </div>
  </div>
</div>
```

---

## 11. 技術棧建議

PSYDA prototype 採用：

| 層級 | 工具 | 理由 |
|------|------|------|
| 樣式 | **Tailwind CSS** (CDN) | 零建置、原型快速、與設計系統一致 |
| 反應式 | **Alpine.js** v3 | 輕量、模板語法接近 Vue、適合 prototype |
| 字型 | 系統字型 | 無載入時間、跨平台 |
| 圖示 | 內嵌 SVG（Heroicons style） | 無依賴、可控色彩 |

**進入生產後**建議遷移：
- Next.js + React + Tailwind
- shadcn/ui 元件庫（風格相容）
- React Hook Form + Zod 處理表單驗證
- TanStack Table 處理複雜表格

---

## 附錄 A：色彩快速對照表

```
主色 primary       #2563EB  blue-600
深色 dark          #0F172A  slate-900
輔助 muted         #64748B  slate-500
背景 light         #F1F5F9  slate-100
邊框 border        #E2E8F0  slate-200

成功 success       #10B981  emerald-500
資訊 info          #3B82F6  blue-500
警告 warning       #F59E0B  amber-500
危險 danger        #EF4444  red-500

分群色 1-5
color-1 (藍)       #3B82F6
color-2 (綠)       #10B981
color-3 (橘)       #F59E0B
color-4 (紅)       #EF4444
color-5 (紫)       #8B5CF6
```

---

## 附錄 B：開發 Checklist

新增頁面 / 元件前，自問：

- [ ] 沒有資訊背景的 HR 看得懂這個畫面嗎？
- [ ] 有沒有用到「Prompt」「ID」「API」這類技術詞？
- [ ] 主操作有沒有藏在 ⋮ 選單裡？
- [ ] 一頁有沒有超過 3 個飽和色？
- [ ] 警告 (warning) 是不是用在「需要注意」的場景？
- [ ] 表格內有沒有嵌套表格？
- [ ] 刪除動作有沒有確認流程？
- [ ] 步驟超過 5 個了嗎？
- [ ] 篩選後的空狀態有沒有提供「清除篩選」？
- [ ] 進度資訊是不是「乾巴巴的數字」（缺視覺化）？

任何一個答 yes，回頭修。

---

*Version 1.0 · 2026.05 · 來自 PSYDA UI/UX 優化專案實踐*
