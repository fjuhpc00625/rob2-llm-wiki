# 5 篇 RCT 測試集執行紀錄、驗證結果與 Workflow 反思

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

---

## 三、步驟四反思（Reflection）

### 1. 哪一個節點最常出錯？
**節點 3（`RoB 2 Assessment Skill`）最常出錯**，尤其在測試集包含「開放標籤醫材試驗」時最明顯：
- 容易看到 Open-label 就過度懲罰 D4（忽略客觀終點例外 V2）。
- 容易在 Overall Risk 做出人性化折衷，違反 RoB 2 一票否決強制規則（V1）。

### 2. 你發現問題後，把檢查往前移到了哪一個步驟？
原本若等到 HTML 簡報全部寫完才檢查內容，只要一個測試案例的燈號或規則判錯，就得重改簡報表格、案例卡片與互動測驗。因此將 `Rule Validation Skill` **往前移到節點 4（評量測試集完成後、HTML 簡報生成之前）**，先確認所有測試結果 100% 符合 `wiki/` 規則，才放行生成簡報。

### 3. 你有沒有因此修改 Workflow / Graph？為什麼？
**有，而且做了兩項關鍵架構修正：**
1. **知識庫與測試集分離**：初期曾誤把 5 篇受測 RCT 直接放進 `raw/` 當 Wiki 來源，後來發現這會混淆「評估規則（RoB 2 方法學）」與「受測對象（RCT 測試集）」。因此重構為 `raw/`（5 篇 RoB 2 官方方法學）→ `wiki/`，並獨立出 `test-cases/`（5 篇真實 RCT）作為雙 Skill 的測試輸入。
2. **兩段式雙迴圈 Graph**：拆分為「前置規則驗證迴圈（節點 3↔4，上限 3 次）」與「後置視覺教學迴圈（節點 5↔6，上限 2 次）」，各自擁有明確的檢查標準與停止條件。
