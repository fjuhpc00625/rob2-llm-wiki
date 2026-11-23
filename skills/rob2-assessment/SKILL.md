---
name: rob2-assessment
description: 依據 LLM Wiki 中的 RoB 2 方法學與官方規則，對外部測試集（test-cases/）中的隨機對照試驗（RCT）進行 5 大 Domain 偏差風險評量，並輸出結構化測試報告與教學案例解說。
---

# RoB 2 Assessment Skill

## 角色定位
在整體 Workflow Graph 中負責 **「評量生成器（Generator / Assessor）」**：讀取 `wiki/` 中的 RoB 2 方法學規範，對 `test-cases/` 內的真實 RCT 論文執行評量，產出結構化評量草稿與白話教學解說。

## 必要輸入
1. **方法學知識庫（唯讀查詢）**：`wiki/concepts/d1-randomization.md` ～ `d5-selective-reporting.md` 與 `wiki/concepts/rob2-decision-rules.md`
2. **受測對象（外部測試集）**：`test-cases/<trial-name>.md`

## 執行步驟
1. **確認評量單位（Outcome-level）**：標明該試驗的介入組、對照組與主要結果指標（Primary Outcome），並依 `wiki/concepts/d4-outcome-measurement.md` 區分其屬於「客觀指標」或「主觀／臨床裁量指標」。
2. **逐一評估 5 大 Domain**：依 `wiki/concepts/` 查詢對應 Signaling Questions（1.1–5.3），對 D1–D5 給出回答（`Y / PY / PN / N / NI`）與證據依據。
3. **推導 Overall Risk**：依 `wiki/concepts/rob2-decision-rules.md` 推導 `Low`、`Some concerns` 或 `High`。
4. **產出教學白話版**：為初學者補充一句白話解讀，並將首次出現的專業縮寫（如 `PCWP`、`FEV1`、`ITT`）加上中文說明。

## 輸出限制
- **不可自行宣告通過**：所有測試評量輸出皆須標記 `STATUS: DRAFT`，交由 `rule-validation` Skill 執行前置驗證。
- 若被退回，須針對 `VIOLATIONS` 清單逐項修正後重新提交（最多重試 3 次）。
