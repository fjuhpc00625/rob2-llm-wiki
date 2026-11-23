---
name: rob2-assessment
description: 依據 LLM Wiki 中的 RoB 2 規範與試驗資料，對隨機對照試驗（RCT）進行 5 大 Domain 偏差風險評量，並輸出適合教學簡報使用的結構化摘要。
---

# RoB 2 Assessment Skill

## 角色定位
在整體 Workflow Graph 中負責 **「生成與評量（Generator / Assessor）」**，讀取 `wiki/` 中的試驗資料與 `wiki/concepts/rob2-decision-rules.md`，產出結構化的 RoB 2 評量草稿與白話教學解說。

## 必要輸入
1. `wiki/concepts/rob2-decision-rules.md`（官方判定規則）
2. `wiki/trials/<trial-name>.md`（目標試驗的 Wiki 筆記）

## 執行步驟
1. **確認評量單位**：標明該試驗的介入組、對照組與主要結果指標（Primary Outcome），並判斷該指標屬於「客觀指標（如體重、實驗室數值、死亡率）」或「主觀／受臨床判斷影響指標（如症狀分數、醫師決定是否再住院）」。
2. **逐一評估 5 大 Domain**：
   - **D1**：隨機分派過程（Randomization process）
   - **D2**：偏離預期介入（Deviations from intended interventions）
   - **D3**：缺失結果資料（Missing outcome data）
   - **D4**：結果測量（Measurement of the outcome）
   - **D5**：選擇性報告結果（Selection of the reported result）
3. **標註引導問題與證據**：每個 Domain 必須列出關鍵 Signaling Question 回答（`Y / PY / PN / N / NI`）及來自 `wiki/` 的證據依據。
4. **推導 Overall Risk**：依官方邏輯推導 `Low`、`Some concerns` 或 `High`。
5. **產出教學白話版**：為初學者補充一句「白話解讀」，說明該偏差為何會影響研究可信度。

## 輸出限制
- **不可自行宣告通過**：產出結果必須標記為 `STATUS: DRAFT`，交由 `rule-validation` Skill 執行前置驗證。
- 若被 `rule-validation` 退回，必須針對 `VIOLATION_CODE` 逐項修正後重新提交（最多重試 3 次）。
