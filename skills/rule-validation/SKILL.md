---
name: rule-validation
description: 作為 Workflow Graph 的前置檢查關卡，依據 RoB 2 官方演算法與證據一致性規則，稽核 RoB 2 Assessment Skill 的評量草稿與教學內容。
---

# Rule Validation Skill

## 角色定位
在整體 Workflow Graph 中負責 **「前置規則稽核（Validator / Gatekeeper）」**。本 Skill 不負責重新撰寫評量，而是以確定性規則檢查 `rob2-assessment` 的產出，決定 `PASS`（放行進入簡報生成）或 `FAIL`（退回重修）。

## 驗證規則清單（Deterministic Rules）

### Rule V1：Overall Risk 最高風險強制規則
- 若 D1–D5 中**任一 Domain 為 `High`**，則 Overall Risk **必須為 `High`**。
- 若所有 Domain 均為 `Low`，則 Overall Risk **必須為 `Low`**。
- 若無 `High`，但有 1 個以上 Domain 為 `Some concerns`，Overall Risk 至少為 `Some concerns`（若多個 Domain 為 `Some concerns` 且大幅降低可信度，可升為 `High`，但須註明理由）。

### Rule V2：D4 客觀終點防護規則（防過度懲罰）
- 即使試驗為 **Open-label（開放標籤）**，若主要終點為客觀量測指標（如體重公斤數、血中肌酸酐、肺功能 FEV1 機器量測），不可僅因「未盲化」就自動將 D4 判為 `High`；須檢查「知悉分組是否可能影響測量結果」（Signaling Question 4.4 / 4.5）。

### Rule V3：D1 隨機化與分配隱藏規則
- 若文獻僅寫「randomized」但未說明隨機序列產生方式與分配隱藏（Allocation concealment），且基線無明顯失衡，D1 應判為 **`Some concerns`** 而非 `Low`。
- 若出現明顯基線不平衡或無法解釋的不等比例分組且缺乏隱藏說明，需檢視是否涉及分配偏差。

### Rule V4：證據可追溯規則（防幻覺）
- 所有樣本數、分組人數、主要終點與試驗登錄號必須與 `wiki/trials/` 及 `raw/` 一致，不得憑空捏造 Signaling Question 題號或數據。

### Rule V5：初學者可讀性規則
- 每一個 Domain 評量皆須附帶白話解釋，不得僅堆砌未解釋的英文縮寫（如 `PCWP`、`ITT`、`FEV1` 首次出現須加註中文說明）。

## 輸出格式
```text
VALIDATION_RESULT: PASS | FAIL
VIOLATIONS:
  - [Rule ID] 錯誤說明與修正指引
NEXT_ACTION: PROCEED_TO_SLIDES | LOOP_BACK_TO_ASSESSMENT (retry N/3)
```
