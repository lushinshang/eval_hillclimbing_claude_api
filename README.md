# 讓 Claude 幫你設計評測、爬坡優化，又不騙到自己

Anthropic〈Automating eval design and hillclimbing with Claude〉（Lance Martin，claude.dev Blog，2026-09-28）的繁體中文（台灣用語）深度導讀網頁：如何設計可靠的評測（eval）、如何用 hillclimbing 爬坡優化又不被分數騙到，以及 `claude-api` skill 的 `build-eval`、`hillclimb` 兩個指令與兩個實例。

🌐 **線上閱讀：https://lushinshang.github.io/eval_hillclimbing_claude_api/**

## 200字介紹

同一套設定，在搜尋用工單答對 98.9%，換到 14 張沒看過的保留工單，只剩 90.5%。這是 Anthropic 公開的內部案例，點出評測的常見陷阱：分數升了，不代表真的變好。文章談如何設計可靠的評測，並用 hillclimbing 一次只改一處，靠保留的測試集抓過擬合。兩個實例：客服工單成本約降為五分之一；claude-api skill 通過率由 66% 升到約 88%。數字皆為原文自述，未經獨立重現。導讀附 9 張原文圖表繁中版。

## 檔案說明

| 檔案 | 說明 |
|---|---|
| `index.html` | 導讀網頁本體（CSS／JS 內嵌，不依賴外部函式庫；手機顯示 9:16 圖、桌面顯示 16:9 圖，點圖可放大） |
| `eval_hillclimbing_claude_api.md` | 導讀 Markdown 原稿 |
| `images/web/zh/` | 原文圖 1–9 的繁體中文版（圖內文字已翻譯並保留數值；每張 16:9 與 9:16 兩版） |
| `images/web/extra/` | 導讀者依原文整理繪製的補充示意圖（圖角落標註「導讀示意圖」，並非原文圖片） |
| `images/web/hero/` | 頁面頂端全覽圖 |
| `images/hero/og_1200x630.png` | LINE／社群分享預覽圖 |

## 原始素材

- 類型：文章（部落格）
- 標題：Automating eval design and hillclimbing with Claude
- 作者：Lance Martin｜發布：2026-09-28
- 網址：https://claude.dev/blog/automating-eval-design-and-hillclimbing/
- 逐字稿：不適用（非影音來源）

## 查證來源與限制

- 主要來源為上述原文，文中所有數字與流程皆出自該文。原文的實驗數據（44 張工單的成本案例、claude-api skill 的通過率 66% → 約 88%）為 Anthropic 內部自述結果，沒有公開的獨立重現。
- 原文圖 3、圖 4、圖 7 在原文中標註為示意（schematic／illustration），圖中數字並非實測。
- Opus 5.5 相對 Opus 4.8 的 token 定價差異（輸入輸出便宜 20%、cache 讀取便宜 60%）為原文說法，本導讀未另行查證。
- 原文以「我們」（Anthropic）的口吻撰寫，同時是自家 claude-api skill 的使用指南，文中比較的也是 Anthropic 自家模型，讀者宜自行斟酌。

## 著作權與圖片說明

本頁為個人導讀與學習筆記。圖 1–9 由原文圖表重繪並將圖內文字翻譯為繁體中文，版面與數據來自原文，著作權屬原作者與 Anthropic；如原權利人要求下架，請開 issue 聯絡。標註「導讀示意圖」的圖片為導讀者所繪。圖片製作方式：多數圖由 AI（imagegen）重繪；表格與文字密集的幾張因 AI 重繪出現空白或錯字，改由程式繪製或修補——圖 4（橫式、直式）、圖 7 直式版與檢查表直式版為程式繪製，圖 7 橫式版是 AI 重繪後再以程式修補提示詞欄文字。所有圖的數值均經目視逐張比對原圖，未以 OCR 自動驗證。
