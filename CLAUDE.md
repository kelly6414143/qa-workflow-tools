# CLAUDE.md

測試組 AI 導入的 QA workflow 工具集(pnpm monorepo)。本檔記錄 Claude 與團隊需要的專案慣例;問卷 app 的操作細節見 `README.md`。

## 整體流程:問卷 → 訪談綱要 → 面談測試人員 → 組長訪談前彙整 → 面談組長

1. 測試組成員填前置問卷 `apps/pre-interview/index.html`,用「複製填答內容 / 下載為文字檔」匯出純文字。
2. 把匯出的 `.txt` 放進 `results/pre-interview/`。
3. 在本 repo 開 Claude Code,觸發 `interview-guide` skill 批次產出各人訪談綱要。
4. 拿綱要面談第一線測試人員,把面談紀錄(每筆標「原話 vs 歸納」+ 對應主題/題號)放進 `results/interview-notes/`。
5. 觸發 `lead-prep` skill,把多位測試人員的訪談紀錄彙整成一份「組長訪談前清單」(待組長解釋的現象清單)。
6. 拿這份清單面談組長(最終根因分析仍不在本工具範圍,留待三方訪談到齊後另支處理)。

## results/ 資料夾慣例

- 輸入:`results/pre-interview/{稱呼}_問卷填答.txt`(問卷填答,檔名任意;「稱呼」以檔案內容為準)。
- 輸出:`results/interview-guides/` —— 每人 `{稱呼}_訪談綱要.md` + 一份 `_批次彙整_訪談優先順序.md`。
- 輸入:`results/interview-notes/{稱呼}_訪談紀錄.md`(測試人員面談紀錄,格式=訪談筆記範本填好的樣子;題號為指標、非題目全文,需搭配同人訪綱對照)。
- 輸出:`results/lead-prep/_組長訪談前彙整.md`(單一彙整檔)。

## interview-guide skill

- 位置:`.claude/skills/interview-guide/`(專案層級,隨 git 版控)。
- 觸發:對話說「產生訪談綱要」或打 `/interview-guide`(預設掃 `results/pre-interview/`)。
- 轉換規則正本:`.claude/skills/interview-guide/reference/轉換提示詞.md`(唯一真實來源,改規則只改這份)。
- 已知限制:只展開問卷 02/05/06/07 四大主題;03/04 區塊會列入總覽表但不深挖。

## lead-prep skill

- 位置:`.claude/skills/lead-prep/`(專案層級,隨 git 版控)。
- 觸發:對話說「彙整組長訪談前清單」或打 `/lead-prep`(預設掃 `results/interview-notes/`)。
- 彙整規則正本:`.claude/skills/lead-prep/reference/彙整提示詞.md`(唯一真實來源,改規則只改這份)。
- 用途:把多位第一線測試人員的訪談紀錄,彙整成「待組長解釋的現象清單」——只盤點現象、不腦補成因、不合併真衝突,標記兩人關係(共識/差異/新增)並區分「現象·缺成因 vs 現象·已有第一線成因」。
- 已知限制:只處理 02/05/06/07 四大主題;**不**產出最終根因分析(那是三方訪談到齊後另一支合併分析的職責)。
