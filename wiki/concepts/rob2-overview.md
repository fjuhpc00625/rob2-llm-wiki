# RoB 2 核心概念與 5 大偏差領域

**RoB 2（Revised Cochrane Risk-of-Bias tool for randomized trials）** 是目前實證醫學領域最權威的工具，用來評估一篇「隨機對照試驗（RCT）」的研究結果有多可信、會不會因為設計或執行瑕疵而產生偏差。

> 白話理解：就算論文的統計結果寫著 `p < 0.05`（有顯著差異），如果研究過程中有設計漏洞，這個「有效」可能只是假象。RoB 2 就是在幫論文做**品質體檢**。

## 5 大評估領域（Domains）

1. **D1：隨機分派過程（Randomization process）**
   - 關心重點：受試者真的是「抽籤隨機」分組的嗎？醫師在收案前會不會偷看到下一位病人分到哪一組（分配隱藏 Allocation Concealment）？
   - 相關案例：[[hu-2020]]（40 vs 60 不等比例分組與隱藏資訊不足）、[[captain-2021]]（中央化隨機分派）。
2. **D2：偏離預期介入（Deviations from intended interventions）**
   - 關心重點：病人或醫師知不知道自己分到哪一組（盲法 Blinding）？會不會因為知道組別就偷偷加藥、換組或給予不同照護？分析時是否採意向治療（ITT）？
   - 相關案例：[[cuore-2014]]、[[hanna-2012]]、[[rapid-chf-2005]]（皆為無法盲化的醫材試驗）。
3. **D3：缺失結果資料（Missing outcome data）**
   - 關心重點：有多少病人中途退出或失聯？退出原因是不是跟副作用或病情惡化有關？
4. **D4：結果測量（Measurement of the outcome）**
   - 關心重點：量測結果的方法準不準確？評估者知悉分組會不會影響評分？（**關鍵提醒**：客觀儀器／體重測量不易受主觀影響，詳見 [[rob2-decision-rules]] 的 V2 規則與 [[open-label-vs-double-blind]]）。
5. **D5：選擇性報告結果（Selection of the reported result）**
   - 關心重點：研究者是不是事前先登錄了主要指標與分析計畫，而不是跑完十種統計後只挑「看起來有效」的那一個來發表？

## 延伸閱讀
- [[rob2-decision-rules]]
- [[open-label-vs-double-blind]]
- [[index]]
