# PSYDA Design System

PSYDA 心理測評題庫管理系統的 UI 設計規範。標準 [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) 結構。

## 結構

| 檔案 | 用途 | 何時載入 |
|------|------|---------|
| [`SKILL.md`](./SKILL.md) | 主檔：Quick Reference + 檔案索引 + 5 條關鍵規則 | **自動載入**（小，~70 行）|
| [`tokens.md`](./tokens.md) | 設計常數：顏色、字型、間距、圓角 | 按需 |
| [`components.md`](./components.md) | 原子元件：按鈕、卡片、輸入、Modal、表格、Alert | 按需 |
| [`patterns.md`](./patterns.md) | 複合模式：步驟表單、5:7 picker、級聯下拉、批次操作 | 按需 |
| [`rules.md`](./rules.md) | Do/Don't 規則 + 反面教材 code | 按需 |

**設計目的**：
- 主檔精簡，AI 自動載入時不會浪費 token
- 詳情拆檔，AI 需要時才讀對應檔案
- 工程師查找：直接看 Quick Reference 表或對應檔案

## 安裝為 Claude Code Skill

```bash
# 全域安裝（所有專案可用）
git clone https://github.com/Eva6539/psyda-design-system.md.git ~/.claude/skills/psyda-design-system

# 或專案安裝
git clone https://github.com/Eva6539/psyda-design-system.md.git .claude/skills/psyda-design-system
```

安裝後，Claude 會根據 SKILL.md 的 description 自動判斷何時載入此 skill。

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

v3 — 標準 Claude skill 資料夾結構（拆檔，省 token）
