# RoB 2 官方判定邏輯與規則驗證標準

本頁由 `raw/04-rob2-decision-algorithms.md` 與 `raw/05-cochrane-handbook-ch8-bias.md` 編譯而成，作為 `Rule Validation Skill` 在 Workflow Graph 節點 4 執行的確定性檢核規則（V1–V5）。

## 1. 引導問題五種回答
- `Y`（Yes）／ `PY`（Probably yes）／ `PN`（Probably no）／ `N`（No）／ `NI`（No information）／ `NA`（Not applicable）

## 2. Rule V1：Overall Risk 強制演算法（一票否決制）

| 條件 | Overall Risk 判定 |
| :--- | :--- |
| D1–D5 **全部為 `Low`** | **`Low`**（低偏差風險） |
| 沒有任何 `High`，但有 **至少 1 個 `Some concerns`** | **`Some concerns`**（有些疑慮） |
| **任一 Domain 為 `High`**，或多個 `Some concerns` 嚴重削弱可信度 | **`High`**（高偏差風險） |

## 3. Rule V2：D4 客觀終點防護規則（防過度懲罰）
- 對應 [[d4-outcome-measurement]] 題號 `4.3` 與 `4.4`：即使試驗為 **Open-label（`4.3 = Y`）**，只要主要終點屬於客觀儀器或磅秤量測（如體重、PCWP、肌酸酐、FEV1），使 `4.4 = N / PN`，D4 必須判為 **`Low`**，不可因「未盲化」反射性判 `High`。

## 4. Rule V3：D1 分配隱藏與不平衡規則
- 對應 [[d1-randomization]] 題號 `1.2` 與 `1.3`：
  - `1.2 = NI` 且 `1.3 = N/PN/NI` → 至少 **`Some concerns`**（不可給 `Low`）。
  - `1.2 = NI` 且 `1.3 = Y/PY`（如難以解釋的不等比例分組或明顯基線失衡）→ **`High`**。

## 5. Rule V4：證據與來源可追溯規則（防幻覺）
- 所有樣本數、分組人數、主要終點、題號與演算法引用必須分別追溯至 `test-cases/` 與 `wiki/`，嚴禁捏造數據或不存在的題號。

## 6. Rule V5：初學者可讀性規則
- 輸出至教學簡報的每個評量與案例解說，首次出現專業縮寫（如 `PCWP`、`ITT`、`FEV1`）皆須附白話中文說明。

## 關聯頁面
- [[rob2-overview]] | [[d1-randomization]] | [[d4-outcome-measurement]] | [[index]]
