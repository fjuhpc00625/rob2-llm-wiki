# 實際執行、檢查紀錄與 Workflow 反思

## 一、一次實際執行紀錄（Execution & Validation Log）

- **執行日期**：2026-11-23
- **知識庫來源**：`wiki/`（已完成 5 篇文獻 Ingest：`cuore-2014`、`hanna-2012`、`hu-2020`、`rapid-chf-2005`、`captain-2021`）
- **執行流程**：`查詢 Wiki → RoB 2 Assessment Skill（節點 3）→ Rule Validation Skill（節點 4）→ 條件 Loop → HTML 簡報生成（節點 5）→ 可讀性檢查（節點 6）`

### Round 1：初版評量草稿送交 Rule Validation Skill

**`RoB 2 Assessment Skill` 初版輸出（節錄異常項目）：**
1. `rapid-chf-2005`：因試驗為 Open-label，初版將 **D4（結果測量）判為 `High`**，Overall Risk 判為 `High`。
2. `hu-2020`：初版將 D1 判為 `High`（因 40 vs 60 不等分組且隱藏說明不足），但將 **Overall Risk 判為 `Some concerns`**（理由寫「其餘領域尚可」）。
3. 簡報大綱初稿中直接寫「PCWP ≤ 18 mm Hg 與 trough FEV1」，未對初學者加註中文白話說明。

**`Rule Validation Skill` 稽核結果（FAIL）：**
```text
VALIDATION_RESULT: FAIL
VIOLATIONS:
  - [Rule V2] rapid-chf-2005 的主要終點為「24 小時體重變化（客觀磅秤量測）」，不可僅因 Open-label 就自動將 D4 判為 High。請重新檢核 Signaling Question 4.4/4.5 並調整 D4。
  - [Rule V1] hu-2020 的 D1 為 High，違反 Overall Risk 最高風險強制規則（任一 Domain 為 High 時，Overall 必須為 High，不得判為 Some concerns）。
  - [Rule V5] 教學摘要出現未解釋之專有名詞（PCWP、FEV1），不符合初學者可讀性要求。
NEXT_ACTION: LOOP_BACK_TO_ASSESSMENT (retry 1/3)
```

### Round 2：依 `VIOLATIONS` 退回修正後再驗證

**`RoB 2 Assessment Skill` 修正動作：**
1. 依 V2 檢視 `wiki/trials/rapid-chf-2005.md`：確認 24 小時體重為客觀測量，將 D4 校正為 `Low`，Overall Risk 更新為 `Some concerns`。
2. 依 V1 強制規則：將 `hu-2020` 的 Overall Risk 由 `Some concerns` 修正為 **`High`**。
3. 依 V5 規範：於所有教學摘要與簡報大綱補上中文白話解釋（如 `PCWP（肺微血管楔壓，反映心臟充血壓力）`、`FEV1（第一秒用力呼氣容積，反映氣管通暢度）`）。

**`Rule Validation Skill` 二次稽核結果（PASS）：**
```text
VALIDATION_RESULT: PASS
VIOLATIONS: None (0/5 rules violated)
NEXT_ACTION: PROCEED_TO_SLIDES
```

### Round 3：HTML 簡報生成與可讀性檢查（節點 5 ↔ 節點 6）
- 產出 `slides/index.html`（共 9 頁互動式教學簡報），包含 RoB 2 紅黃綠燈總覽表、5 篇試驗對比卡片、互動式「你來當 Rule Validator」小測驗、以及 Loop / Graph 流程圖解。
- 檢查鍵盤方向鍵切換、進度條、響應式排版與無障礙對比度均正常 → **達停止條件，流程結束**。

---

## 二、步驟四反思（Reflection）

### 1. 哪一個節點最常出錯？
**節點 3（`RoB 2 Assessment Skill`）最常出錯**，而且錯在兩個非常典型、初學者也容易忽略的地方：
- **過度套用刻板印象**：AI 看到「Open-label（開放標籤）」就反射性把 D4（結果測量）判成 `High`，忽略了 RoB 2 規則中「客觀指標（如體重、血壓、儀器數值）不易受未盲化影響」的重要例外。
- **軟性妥協違反硬規則**：AI 在綜合評估 Overall Risk 時，傾向用「整體看起來還不錯」的語氣給出 `Some concerns`，違反了 RoB 2「只要任一 Domain 為 `High`，Overall 就必須為 `High`」的確定性演算法。

### 2. 你發現問題後，把檢查往前移到了哪一個步驟？
原本最直覺的做法是「直接叫 AI 讀完資料一口氣生成 HTML 簡報，最後再檢查簡報內容」。但在實作中發現，如果等到 HTML 寫完才抓到 `RAPID-CHF` 的 D4 判錯或 `Hu 2020` 的 Overall 判錯，就得同時改寫簡報表格、統計數字、燈號顏色與案例解說，重工成本很高。

因此我採用 **Shift-Left（檢查左移）** 策略，把 **`Rule Validation Skill` 往前移到「節點 4（Wiki 評量與教學大綱完成後、HTML 簡報生成之前）」**，先確保結構化知識與邏輯 100% 通過確定性規則，才放行進入 HTML 視覺生成。

### 3. 你有沒有因此修改 Workflow / Graph？為什麼？
**有。** 我將原本單一線性的流程，重構為**兩段式雙迴圈 Graph**：
1. **前置內容與規則迴圈（節點 3 ↔ 節點 4，上限 3 次）**：專責處理事實、演算法規則與白話術語，由 `rob2-assessment` 與 `rule-validation` 角色分離互查。
2. **後置視覺與教學迴圈（節點 5 ↔ 節點 6，上限 2 次）**：只專注在 HTML 排版、互動測驗與初學者閱讀流暢度，不再回頭懷疑數據正確性。

這樣拆分後，不僅大幅減少生成 HTML 後的返工，也讓「知識正確性」與「簡報呈現」各自有明確的檢查標準與停止條件。
