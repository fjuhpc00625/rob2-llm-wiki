# AGENTS.md — RoB 2 LLM Wiki 與教學簡報工作流規則

本專案遵循 **LLM Wiki（先編譯、後查詢）** 與 **知識庫／測試集嚴格分離** 原則，主題為 **RoB 2（Cochrane Risk of Bias 2）偏差風險評量與規則驗證**。

## 1. 目錄分工與權限（嚴格區分「知識來源」與「測試案例」）

| 目錄 | 角色 | 寫入規則 |
| :--- | :--- | :--- |
| `raw/` | **方法學原始資料層**（5 篇 RoB 2 官方文獻） | **唯讀**：僅放 RoB 2 方法學原論文、指引、題目表與演算法，**不放受測 RCT 論文**。 |
| `wiki/` | **編譯後方法學知識庫**（Obsidian 相容） | AI 依 `raw/` 編譯維護，必須使用雙向連結 `[[頁面名稱]]` 與來源引用。 |
| `test-cases/` | **外部測試集**（5 篇真實 RCT 臨床試驗） | 唯讀輸入資料，用來測試 `rob2-assessment` 與 `rule-validation` 的實戰表現。 |
| `skills/` | 專職 Agent 技能規範 | 拆分為 `rob2-assessment`（依 Wiki 評量測試集）與 `rule-validation`（依 Wiki 規則稽核）。 |
| `logs/` | **測試執行與驗證結果紀錄** | 記錄 5 篇 RCT 測試集的評量結果、驗證攔截錯誤、重試與修正紀錄。 |
| `slides/` | 教學型 HTML 簡報產出 | 概念知識來自 `wiki/`，實戰案例演示取自 `logs/` 之測試驗證結果。 |

## 2. LLM Wiki 核心操作規範

1. **Ingest（匯入方法學文獻）**：讀取 `raw/` 中的 RoB 2 方法學文獻，編譯為 `wiki/concepts/` 下的領域與規則頁，並更新 `wiki/index.md` 與 `wiki/log.md`。
2. **Query（查詢知識庫）**：所有 RoB 2 定義、22 題 Signaling Questions 與判定邏輯皆須查詢 `wiki/`，禁止脫離知識庫臆測。
3. **Evaluate（測試集評估）**：讀取 `test-cases/` 中的真實 RCT，呼叫 `rob2-assessment` 評量並由 `rule-validation` 稽核，將結果寫入 `logs/execution-record.md`。
4. **Lint（知識庫健康檢查）**：檢查孤立頁面、斷連 `[[wikilinks]]` 與規則一致性。

## 3. Loop / Graph 執行與停止條件

1. **角色分離原則**：不得由同一步驟自評通過；`rob2-assessment` 產出必須交由 `rule-validation` 稽核。
2. **前置驗證原則（Shift-Left Validation）**：所有評量與教學案例**必須在生成 HTML 簡報前通過 `rule-validation`**。
3. **停止條件（Stopping Condition）**：
   - `Assessment ↔ Validation` 迴圈：最多重試 **3 次**。
   - `HTML Slide Generation ↔ Readability Check` 迴圈：最多重試 **2 次**。
   - 達上限仍未通過則停止自動重試，標記為 `NEEDS_HUMAN_REVIEW`。
