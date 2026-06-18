# PSYDA Design System

PSYDA 心理測評題庫管理系統的 UI 設計規範。符合 [Skills Package Specification](https://github.com/kuanntw/skills-spec) v0.1.0 的標準 skill 套件。

## 結構（spec-compliant）

```
psyda-design-system/
├── SKILL.md            ← 主檔，AI 自動載入（~70 行）
├── skill.json          ← Package manifest（spec required）
└── references/
    ├── tokens.md       ← 顏色、字型、間距、圓角
    ├── components.md   ← 原子元件（button、card、input、modal）
    ├── patterns.md     ← 複合模式（step modal、5:7 picker）
    └── rules.md        ← Do/Don't 規則 + 反面教材
```

| 檔案 | 何時載入 |
|------|---------|
| `SKILL.md` | 自動（小，~70 行）|
| `skill.json` | CLI / SDK 工具讀取 |
| `references/*.md` | 按需，AI 引用時才讀 |

## 安裝

### 為 Claude Code skill 安裝（建議）

```bash
# 全域安裝
git clone https://github.com/Eva6539/psyda-design-system.md.git \
  ~/.claude/skills/psyda-design-system

# 或使用 spec 推薦的 .agents/skills/ 路徑
git clone https://github.com/Eva6539/psyda-design-system.md.git \
  ~/.agents/skills/psyda-design-system

# 專案級別安裝
git clone https://github.com/Eva6539/psyda-design-system.md.git \
  .claude/skills/psyda-design-system
```

安裝後 Claude 會根據 SKILL.md 的 description 自動判斷何時載入。

## 符合的 Spec 規範

- **Core skill format**：`SKILL.md` + YAML frontmatter ✓
- **Package manifest**：`skill.json` 含 schema_version、name、version、entrypoint ✓
- **Progressive disclosure**：主檔精簡，詳情拆檔到 `references/` ✓
- **Naming**：lowercase kebab-case（`psyda-design-system`）✓
- **Capability declarations**：filesystem read-only, no network/secrets ✓
- **Versioning**：SemVer (`1.0.0`) ✓
- **Source metadata**：git repo URL + branch ✓

## 適用情境

- 為 PSYDA 平台撰寫或審查前端程式碼
- 選擇 Tailwind CSS class string
- 實作複合互動模式（步驟表單、雙欄選擇器等）
- 程式碼審查時對照規範

## 技術棧

- **Prototyping**: Tailwind CSS (CDN) + Alpine.js v3
- **Production target**: Next.js + React + shadcn/ui

## 相關專案

完整互動原型：[Eva6539/PSYDA-UI-UX](https://github.com/Eva6539/PSYDA-UI-UX)

## 版本

v4 — Spec-compliant（符合 [kuanntw/skills-spec](https://github.com/kuanntw/skills-spec) v0.1.0）

---

## 其他內容（非本 skill）

本 repo 另含一份**獨立的設計交付**，與上述 PSYDA skill 分開、互不影響：

- [`簡易自測心理測評-前端交付/`](./簡易自測心理測評-前端交付/) — **2026-06-18 新增（最新・規範定案版）**。給前端工程師的交付包：設計系統規範頁、首頁與測評流程原型(純 HTML/CSS/JS)、設計 token(`tokens.css`)、完整交付說明、設計提案簡報。識別色＝暖珊瑚 #F5806C、材質＝黏土×液態玻璃。**以此版為準。**
- [`簡易自測心理測評-UI改版/`](./簡易自測心理測評-UI改版/) — 2026-06-17。早期探索版(Mochi 療癒陪伴)；已被上方「前端交付」資料夾取代。
