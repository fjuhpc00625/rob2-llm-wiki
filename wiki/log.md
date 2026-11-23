# Wiki 變更與 Lint 維護紀錄

## 2026-11-23
- **[INIT]** 透過「先討論、後生成」建立專案架構與 `AGENTS.md`，定義 `raw/`、`wiki/`、`skills/`、`logs/`、`slides/` 分工。
- **[CONCEPT]** 建立 [[rob2-overview]]、[[rob2-decision-rules]]、[[open-label-vs-double-blind]] 三篇核心概念頁。
- **[INGEST #1]** 匯入 `raw/01-cuore-marenzi-2014.md` → 建立 [[cuore-2014]]。
- **[INGEST #2]** 匯入 `raw/02-hanna-2012-uf-icu.md` → 建立 [[hanna-2012]]。
- **[INGEST #3]** 匯入 `raw/03-hu-2020-early-uf.md` → 建立 [[hu-2020]]。
- **[INGEST #4]** 匯入 `raw/04-rapid-chf-bart-2005.md` → 建立 [[rapid-chf-2005]]。
- **[INGEST #5]** 匯入 `raw/05-captain-lee-2021.md` → 建立 [[captain-2021]]。
- **[VALIDATION]** 執行 `rob2-assessment` → `rule-validation` 雙關卡驗證：於第 1 輪攔截 2 項規則違反（V1、V2），修正後於第 2 輪全數 `PASS`，詳見 `logs/execution-record.md`。
- **[LINT]** 檢查所有 `[[wikilinks]]` 與 `index.md` 表格一致性：0 斷連、0 孤立頁、5 篇文獻數據與 `raw/` 一致。
