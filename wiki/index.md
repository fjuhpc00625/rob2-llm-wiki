# RoB 2 LLM Wiki — 知識庫總索引 (MOC)

歡迎來到 **RoB 2 偏差風險評量與規則驗證** 知識庫。本 Wiki 由 AI Agent 依據 [[AGENTS]] 規則，從 `raw/` 中 5 篇隨機對照試驗（RCT）編譯而成，並作為教學 HTML 簡報（`slides/index.html`）與雙 Skill 工作流的唯一知識來源。

## 1. 核心概念與規則（Concepts）
- [[rob2-overview]] — 什麼是 RoB 2？5 大偏差領域白話導覽
- [[rob2-decision-rules]] — RoB 2 官方判定邏輯與 Rule Validation Skill 驗證規則（V1–V5）
- [[open-label-vs-double-blind]] — 跨文獻洞見：為什麼 4 篇心衰竭超濾試驗與 CAPTAIN 試驗風險落差如此大？

## 2. 已匯入試驗評量頁（Ingested Trials, n = 5）

| 編號 | 試驗頁面 | 領域 / 設計 | 樣本數 | 盲法 | Overall Risk（驗證後） |
| :--- | :--- | :--- | :---: | :--- | :--- |
| 01 | [[cuore-2014]] | 心衰竭超濾 RCT | 56 | Open-label | **Some concerns** |
| 02 | [[hanna-2012]] | ICU 心衰竭超濾 RCT | 36 | Open-label | **Some concerns** |
| 03 | [[hu-2020]] | 早期超濾 RCT | 100 | Open-label | **High** |
| 04 | [[rapid-chf-2005]] | 心衰竭超濾先導 RCT | 40 | Open-label | **Some concerns** |
| 05 | [[captain-2021]] | 氣喘三合一吸入劑 Phase 3A | 2,436 | Double-blind | **Low** |

## 3. 工作流與紀錄
- 變更與 Lint 日誌：[[log]]
- 實測抓錯與反思紀錄：`logs/execution-record.md`
- 教學互動簡報：`slides/index.html`
