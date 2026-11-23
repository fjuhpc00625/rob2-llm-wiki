# RoB 2 LLM Wiki — 知識庫總索引 (MOC)

本 Wiki 由 AI Agent 依據 [[AGENTS]] 規則，從 `raw/` 中 **5 篇 RoB 2 官方方法學與指引文獻**編譯而成，作為 `RoB 2 Assessment Skill`、`Rule Validation Skill` 與教學 HTML 簡報（`slides/index.html`）的唯一方法學知識來源。

> **資料分層設計原則**：
> - **知識庫來源（`raw/` → `wiki/`）**：5 篇 RoB 2 官方方法學文獻（定義、22 題引導問題、確定性演算法、Cochrane Handbook 原則）。
> - **外部測試集（`test-cases/` → `logs/execution-record.md`）**：5 篇真實臨床試驗（CUORE、Hanna 2012、Hu 2020、RAPID-CHF、CAPTAIN），用來實測雙 Skill 的評量與規則驗證效能，**不混入方法學知識庫**。

## 1. 核心架構與判定演算法
- [[rob2-overview]] — 什麼是 RoB 2？為什麼以「單一結果（Outcome）」為單位評估？
- [[rob2-decision-rules]] — 官方確定性演算法與 `Rule Validation Skill` 檢核規則（V1–V5）

## 2. 五大偏差領域（Domains D1–D5）
- [[d1-randomization]] — D1：隨機分派過程（Randomization process，題號 1.1–1.3）
- [[d2-deviations]] — D2：偏離預期介入（Deviations from intended interventions，題號 2.1–2.7）
- [[d3-missing-data]] — D3：缺失結果資料（Missing outcome data，題號 3.1–3.4）
- [[d4-outcome-measurement]] — D4：結果測量偏差（Measurement of the outcome，題號 4.1–4.5）
- [[d5-selective-reporting]] — D5：選擇性報告結果（Selection of the reported result，題號 5.1–5.3）

## 3. 維護與實測連結
- Wiki 編譯與 Lint 紀錄：[[log]]
- 5 篇真實 RCT 測試集：`test-cases/`
- 雙 Skill 實測執行與抓錯紀錄：`logs/execution-record.md`
- 教學型互動 HTML 簡報：`slides/index.html`
