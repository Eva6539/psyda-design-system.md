# PSYDA Design System

PSYDA 心理測評題庫管理系統的 UI/UX 設計規範，可作為 [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) 使用。

## 內容

完整設計系統規範請見 [`psyda-design-system.md`](./psyda-design-system.md)，包含：

- 核心設計原則（5 大原則）
- 色彩系統（主色、中性、語意色、分類色條、配色禁忌）
- 字型與字級階層
- 間距系統
- 元件規範（按鈕、徽章、卡片、表單、Modal、表格、提示框、空狀態、Toast）
- 互動模式（步驟表單、批次操作、級聯下拉、5:7 雙欄選擇器、麵包屑、進度視覺化、刪除確認、動作分層）
- Anti-patterns（避免事項）
- 完整 Tailwind CSS + Alpine.js 程式碼範例

## 安裝為 Claude Code Skill

```bash
# 全域安裝（所有專案可用）
mkdir -p ~/.claude/skills
curl -L https://raw.githubusercontent.com/Eva6539/psyda-design-system.md/main/psyda-design-system.md \
  -o ~/.claude/skills/psyda-design-system.md

# 或專案安裝（僅限該專案）
mkdir -p .claude/skills
curl -L https://raw.githubusercontent.com/Eva6539/psyda-design-system.md/main/psyda-design-system.md \
  -o .claude/skills/psyda-design-system.md
```

安裝後，Claude 會在設計相關任務時自動載入規範。

## 適用情境

- 為 PSYDA 平台設計新功能或元件時
- 團隊新成員 onboarding
- 設計決策參考（包含實作建議與反面教材）
- 程式碼審查時對照規範

## 設計核心

> 為「沒有資訊背景的一般用戶（HR、輔導老師、行政人員）」打造的後台管理體驗。

所有規則都從**降低非技術用戶的使用門檻**這個核心目標推導而來。

## 相關專案

完整互動原型：[Eva6539/PSYDA-UI-UX](https://github.com/Eva6539/PSYDA-UI-UX)

## License

僅供 PSYDA 專案團隊內部參考使用。
