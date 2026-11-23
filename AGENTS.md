# AGENTS.md — RoB 2 LLM Wiki 與教學簡報工作流規則

本專案遵循 **LLM Wiki（先編譯、後查詢）** 與 **Loop / Graph 工作流** 設計，主題為 **RoB 2（Cochrane Risk of Bias 2）偏差風險評量與規則驗證**。

## 1. 目錄分工與權限

| 目錄 | 角色 | 寫入規則 |
| :--- | :--- | :--- |
| `raw/` | 原始資料層（真相來源） | **唯讀**：放入原始論文摘要、網址與研究設計資料後不再修改。 |
| `wiki/` | 編譯後知識庫（Obsidian 相容） | AI 依本規則編譯維護，必須使用雙向連結 `[[頁面名稱]]` 與來源引用。 |
| `skills/` | 專職 Agent 技能規範 | 拆分為 `rob2-assessment`（評量生成）與 `rule-validation`（規則稽核）。 |
| `logs/` | 執行與驗證紀錄 | 每次執行 Workflow 必須留下輸入、驗證錯誤、重試與修正紀錄。 |
| `slides/` | 教學型 HTML 簡報產出 | 必須以 `wiki/` 為唯一知識來源，面向 RoB 2 初學者。 |

## 2. LLM Wiki 核心操作規範

### A. Ingest（資料匯入與編譯）
1. 讀取 `raw/` 中的新文獻，萃取：研究設計、樣本數、隨機分派與隱藏、盲法設計、缺失資料、主要終點與臨床試驗登錄號。
2. 在 `wiki/trials/` 建立或更新對應試驗頁，並同步更新 `wiki/concepts/` 中的跨文獻歸納頁（例如開放標籤試驗 vs 雙盲試驗比較）。
3. 更新 `wiki/index.md` 索引與 `wiki/log.md` 變更紀錄。

### B. Query（知識查詢）
- 回答問題或撰寫簡報時，**禁止脫離 `wiki/` 憑空捏造數據或題號**；每項 RoB 2 判定皆須對應 `wiki/concepts/rob2-decision-rules.md`。

### C. Lint（知識庫健康檢查）
- 檢查是否存在孤立頁面、斷掉的 `[[wikilinks]]`、或跨頁數據矛盾。

## 3. Loop / Graph 執行與停止條件

1. **角色分離原則**：不得由同一個步驟同時「評量」與「自評通過」。必須由 `rob2-assessment` 產出草稿，再交由 `rule-validation` 稽核。
2. **前置驗證原則（Shift-Left Validation）**：所有 RoB 2 評量與教學案例**必須在生成 HTML 簡報前通過 `rule-validation`**，避免排版完成後才發現邏輯錯誤導致整頁重工。
3. **停止條件（Stopping Condition）**：
   - `Assessment ↔ Validation` 迴圈：最多重試 **3 次**。
   - `HTML Slide Generation ↔ Readability Check` 迴圈：最多重試 **2 次**。
   - 若達上限仍未通過，停止自動重試並將未解錯誤標記為 `NEEDS_HUMAN_REVIEW` 寫入 `logs/`。
