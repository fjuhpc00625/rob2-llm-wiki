---
name: rule-validation
description: 作為 Workflow Graph 的前置檢查關卡，依據 LLM Wiki 中的 RoB 2 官方演算法規則（V1–V5），稽核 RoB 2 Assessment Skill 對 test-cases/ 產出的評量結果。
---

# Rule Validation Skill

## 角色定位
在整體 Workflow Graph 中負責 **「前置規則稽核（Validator / Gatekeeper）」**。依據 `wiki/concepts/rob2-decision-rules.md` 對 `rob2-assessment` 的測試評量結果進行確定性檢查，決定 `PASS`（寫入最終測試結果並放行至簡報生成）或 `FAIL`（退回重修）。

## 驗證規則清單（來源：`wiki/concepts/rob2-decision-rules.md`）

### Rule V1：Overall Risk 最高風險強制規則
- 若 D1–D5 中**任一 Domain 為 `High`**，Overall Risk **必須為 `High`**。
- 若所有 Domain 均為 `Low`，Overall Risk **必須為 `Low`**。
- 若無 `High` 且有 ≥ 1 個 `Some concerns`，Overall Risk 至少為 `Some concerns`。

### Rule V2：D4 客觀終點防護規則（防過度懲罰）
- 即使試驗為 **Open-label（`4.3 = Y`）**，若主要終點為客觀量測指標（體重、PCWP、肌酸酐、FEV1）使 `4.4 = N/PN`，D4 **必須判為 `Low`**，不得僅因未盲化就判 `High`。

### Rule V3：D1 隨機化與分配隱藏規則
- 若 `1.2 = NI` 且 `1.3 = N/PN/NI`，D1 至少判為 **`Some concerns`**（不可給 `Low`）。
- 若 `1.2 = NI` 且 `1.3 = Y/PY`（例如難以解釋的不等比例分組或明顯基線失衡），D1 應判為 **`High`**。

### Rule V4：證據與來源可追溯規則（防幻覺）
- 所有樣本數、分組人數、主要終點與登錄號必須與 `test-cases/` 一致；引用之 Signaling Question 題號必須與 `wiki/` 一致。

### Rule V5：初學者可讀性規則
- 教學案例解說中首次出現之專業縮寫（如 `PCWP`、`FEV1`、`ITT`）必須附帶中文白話說明。

## 輸出格式
```text
VALIDATION_RESULT: PASS | FAIL
VIOLATIONS:
  - [Rule ID] 錯誤說明與修正指引
NEXT_ACTION: PROCEED_TO_SLIDES | LOOP_BACK_TO_ASSESSMENT (retry N/3)
```
