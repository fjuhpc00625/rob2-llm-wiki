# Wiki 變更與 Lint 維護紀錄

## 2026-11-24（架構重構：知識庫與測試集分離）
- **[REFACTOR]** 依據資料分層原則重構專案：將原本混放於 `raw/` 的 5 篇真實 RCT 移至 `test-cases/` 作為外部測試集，確保 `raw/` 與 `wiki/` 純粹承載 RoB 2 方法學知識。
- **[INGEST #1]** 匯入 `raw/01-sterne-2019-bmj-rob2.md`（BMJ 2019 原論文）→ 更新 [[rob2-overview]]。
- **[INGEST #2]** 匯入 `raw/02-cochrane-rob2-full-guidance.md`（官方完整指南）→ 建立 [[d1-randomization]]、[[d2-deviations]]、[[d3-missing-data]]、[[d4-outcome-measurement]]、[[d5-selective-reporting]]。
- **[INGEST #3]** 匯入 `raw/03-rob2-signaling-questions-crib-sheet.md`（22 題引導問題速查表）→ 補齊各 Domain 頁面之題號與條件分支。
- **[INGEST #4]** 匯入 `raw/04-rob2-decision-algorithms.md`（官方確定性判定演算法）→ 更新 [[rob2-decision-rules]]（V1–V5 規則）。
- **[INGEST #5]** 匯入 `raw/05-cochrane-handbook-ch8-bias.md`（Cochrane Handbook Ch.8）→ 強化 [[d4-outcome-measurement]] 開放標籤與客觀終點判斷原則。
- **[EVAL]** 以 `test-cases/` 5 篇真實 RCT 執行 `rob2-assessment` → `rule-validation` 實測，更新 `logs/execution-record.md` 與 `slides/index.html`。
- **[LINT]** 檢查所有 `[[wikilinks]]` 與檔案路徑：0 斷連、0 孤立頁、知識庫與測試集邊界清晰。
