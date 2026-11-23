# D1：隨機分派過程（Randomization process）

- **方法學來源**：`raw/01-sterne-2019-bmj-rob2.md`、`raw/03-rob2-signaling-questions-crib-sheet.md`、`raw/04-rob2-decision-algorithms.md`

## 核心問題（Signaling Questions）
- **1.1** 隨機分派序列（Allocation sequence）是否真正隨機？（如電腦亂數、區組隨機）
- **1.2** 分派序列在受試者入組前是否有效**隱藏（Allocation concealment）**？（如中央互動式系統、不透明密封信封）
- **1.3** 各組的基線特徵或人數比例是否存在難以用機率解釋的失衡，暗示隨機分派出現問題？

## 判定演算法重點（對應 [[rob2-decision-rules]] V3）
- `1.2 = N / PN`（未隱藏分派）→ **High**
- `1.2 = Y / PY` 且 `1.1 = Y / PY / NI` 且 `1.3 = N / PN / NI` → **Low**
- `1.2 = NI`（未說明隱藏方式）且 `1.3 = N / PN / NI` → **Some concerns**（不可給 Low）
- `1.2 = NI` 且 `1.3 = Y / PY`（出現明顯基線或分組比例異常）→ **High**

## 關聯頁面
- [[rob2-overview]] | [[rob2-decision-rules]] | [[d2-deviations]] | [[index]]
