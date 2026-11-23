# RoB 2 官方判定邏輯與規則驗證標準

本頁定義 `Rule Validation Skill` 在 Workflow Graph 節點 4 執行的確定性檢核規則，對應 [[rob2-overview]] 的 5 大 Domain。

## 1. 引導問題（Signaling Questions）五種回答
- `Y`（Yes）：明確符合
- `PY`（Probably Yes）：可能符合
- `PN`（Probably No）：可能不符合
- `N`（No）：明確不符合
- `NI`（No Information）：論文未提供足夠資訊

## 2. 三種風險等級與 Overall Risk 強制演算法（Rule V1）

| 條件 | Overall Risk 判定 |
| :--- | :--- |
| D1–D5 **全部為 `Low`** | **`Low`**（低偏差風險） |
| 沒有任何 `High`，但有 **至少 1 個 `Some concerns`** | **`Some concerns`**（有些疑慮） |
| **任一 Domain 為 `High`**，或多個 `Some concerns` 嚴重削弱可信度 | **`High`**（高偏差風險） |

> **常見 AI 錯誤（V1 攔截重點）**：LLM 常會因為「其他 4 個 Domain 看起來還好」，就把含 1 個 `High` 的論文誤判為 `Some concerns`——這是嚴格違反 RoB 2 演算法的。

## 3. D4 客觀終點防護規則（Rule V2）
- 開放標籤（Open-label）試驗雖然在 D2 容易出現疑慮，但在 **D4（結果測量）** 必須區分終點性質：
  - **客觀終點**（如 [[rapid-chf-2005]] 的「24 小時體重變化」、[[hanna-2012]] 的「PCWP 血流動力學數值」、[[captain-2021]] 的「肺功能 FEV1」）：即使評估者知道分組，也不太可能左右磅秤或儀器讀數 → D4 不應自動判 `High`，通常為 `Low`。
  - **受臨床主觀判斷影響之終點**（如 [[cuore-2014]] 的「醫師決定是否因心衰竭再住院」、或 [[hu-2020]] 的主觀呼吸困難評分）：評估者知悉分組可能影響判斷 → D4 須判為 `Some concerns` 或 `High`。

## 4. D1 隨機與隱藏資訊不足規則（Rule V3）
- 論文只寫 "randomized" 卻未交代隨機序列產生方式與分配隱藏（Allocation Concealment），不可給 `Low`，至少應給 `Some concerns`；若同時伴隨難以解釋的不等比例分組（如 [[hu-2020]] 的 `40` vs `60`）且缺乏隱藏說明，風險會進一步升高。

## 關聯頁面
- [[rob2-overview]]
- [[open-label-vs-double-blind]]
- [[index]]
