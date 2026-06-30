# CLAUDE.md

測試組 AI 導入的 QA workflow 工具集(pnpm monorepo)。本檔記錄 Claude 與團隊需要的專案慣例;問卷 app 的操作細節見 `README.md`。

## 整體流程:問卷 → 訪談綱要 → 面談

1. 測試組成員填前置問卷 `apps/pre-interview/index.html`,用「複製填答內容 / 下載為文字檔」匯出純文字。
2. 把匯出的 `.txt` 放進 `results/pre-interview/`。
3. 在本 repo 開 Claude Code,觸發 `interview-guide` skill 批次產出各人訪談綱要。
4. 拿綱要進行面談(面談後的分析報告目前不在本工具範圍)。

## results/ 資料夾慣例

- 輸入:`results/pre-interview/{稱呼}_問卷填答.txt`(問卷填答,檔名任意;「稱呼」以檔案內容為準)。
- 輸出:`results/interview-guides/` —— 每人 `{稱呼}_訪談綱要.md` + 一份 `_批次彙整_訪談優先順序.md`。

## interview-guide skill

- 位置:`.claude/skills/interview-guide/`(專案層級,隨 git 版控)。
- 觸發:對話說「產生訪談綱要」或打 `/interview-guide`(預設掃 `results/pre-interview/`)。
- 轉換規則正本:`.claude/skills/interview-guide/reference/轉換提示詞.md`(唯一真實來源,改規則只改這份)。
- 已知限制:只展開問卷 02/05/06/07 四大主題;03/04 區塊會列入總覽表但不深挖。
