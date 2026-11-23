# 5 篇 RCT 測試集執行與驗證紀錄

## 一、測試環境與資料邊界
- **方法學知識庫（LLM Wiki）**：`wiki/`（由 `raw/` 中 5 篇 RoB 2 官方方法學文獻編譯而成）
- **外部受測資料集（Test Cases）**：`test-cases/` 中 5 篇真實臨床 RCT 論文
  1. `01-cuore-marenzi-2014.md`（CUORE Trial, *J Card Fail* 2014, `n = 56`）
  2. `02-hanna-2012-uf-icu.md`（Hanna et al., *Congest Heart Fail* 2012, `n = 36`）
  3. `03-hu-2020-early-uf.md`（Hu et al., *BMC Cardiovasc Disord* 2020, `n = 100`）
  4. `04-rapid-chf-bart-2005.md`（RAPID-CHF, *JACC* 2005, `n = 40`）
  5. `05-captain-lee-2021.md`（CAPTAIN Trial, *Lancet Respir Med* 2021, `n = 2,436`）

---

## 二、一次實際執行與規則驗證紀錄（Round 1 → Round 2）

### Round 1：`RoB 2 Assessment Skill` 初版評量草稿 → 送交 `Rule Validation Skill`

**初版評量異常項目：**
1. `test-cases/04-rapid-chf-bart-2005.md`：因試驗為 Open-label，初版將 **D4（24 小時體重變化）誤判為 `High`**，Overall Risk 判為 `High`。
2. `test-cases/03-hu-2020-early-uf.md`：初版將 D1 判為 `High`（40 vs 60 不等分組且隱藏說明不足），但 **Overall Risk 卻判為 `Some concerns`**。
3. 簡報教學摘錄直接寫出 `PCWP` 與 `FEV1`，未加註中文白話說明。

**`Rule Validation Skill` 稽核結果（FAIL）：**
```text
VALIDATION_RESULT: FAIL
VIOLATIONS:
  - [Rule V2] rapid-chf-2005 主要終點為「24 小時體重變化（客觀磅秤量測）」，符合 4.3=Y 但 4.4=N/PN，D4 應判為 Low，不得因 Open-label 自動判 High。
  - [Rule V1] hu-2020 的 D1 為 High，違反 Overall Risk 一票否決強制規則（Overall 必須為 High，不得折衷判為 Some concerns）。
  - [Rule V5] 教學案例出現未解釋之專有名詞（PCWP、FEV1），不符合初學者可讀性規範。
NEXT_ACTION: LOOP_BACK_TO_ASSESSMENT (retry 1/3)
```

### Round 2：依 `VIOLATIONS` 退回修正後再驗證（PASS）

**最終通過驗證之 5 篇 RCT 測試結果總表：**

| 測試案例（`test-cases/`） | 樣本數 | 盲法 | D1 | D2 | D3 | D4 | D5 | Overall Risk |
| :--- | :---: | :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| 01. CUORE (Marenzi 2014) | 56 | Open-label | SC | SC | Low | SC | SC | **Some concerns** |
| 02. Hanna et al. (2012) | 36 | Open-label | SC | SC | Low | Low | SC | **Some concerns** |
| 03. Hu et al. (2020) | 100 | Open-label | **High** | SC | SC | SC | SC | **High** |
| 04. RAPID-CHF (Bart 2005) | 40 | Open-label | SC | SC | Low | **Low** | SC | **Some concerns** |
| 05. CAPTAIN (Lee 2021) | 2,436 | Double-blind | Low | Low | Low | Low | Low | **Low** |

*(註：SC = Some concerns)*

```text
VALIDATION_RESULT: PASS
VIOLATIONS: None (0/5 rules violated)
NEXT_ACTION: PROCEED_TO_SLIDES
```
