# qa-workflow-tools

> 後續文件  
>>  測試流程圖編輯器  
AI 測試導入文件  
測試案例整理工具  
Prompt 模板  
測試流程規劃文件

## 測試組訪談前置問卷

### 檔案

- `apps/pre-interview-tool/index.html`：給測試人員填寫的問卷。
- `apps/pre-interview-tool/src/flow-editor.html`：測試流程圖編輯器，參考 v11 版本並加入問卷回填功能。

### 使用方式

1. 請將兩個 HTML 檔放在同一個資料夾。
2. 開啟 `apps/pre-interview-tool/index.html`。
3. 填寫到「Q1 測試流程現況」時，點選「開啟流程圖編輯器」。
4. 在新分頁完成流程圖後，點選「回填到問卷 Q1」。
5. 回到問卷分頁確認 Q1 已出現 Markdown 流程圖。
6. 問卷填寫完成後，按「複製填答內容」或「下載為文字檔」回傳。

### 備援方式

若瀏覽器或本機檔案權限導致無法自動回填：

1. 在流程圖編輯器點選「預覽 / 複製 Markdown」。
2. 按「複製內容」。
3. 回到問卷 Q1，手動貼上流程圖 Markdown。

