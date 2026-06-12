# PhD Paper Analysis

`phd-paper-analysis` 是一個 Codex skill，用來針對單篇學術論文產生博士層級的繁體中文 HTML 深度分析報告。它特別適合需要完整閱讀論文、拆解方法與公式、分析實驗結果、評估可重現性，並延伸討論音訊 Deepfake 偵測關聯性的研究工作流。

## 功能特色

- 嚴格限制一次分析一篇論文，避免把任務變成泛泛的文獻綜述。
- 支援 PDF、URL、DOI、arXiv ID、精確標題或 citation 作為輸入。
- 在分析前要求驗證論文身份，包括標題、作者、來源、年份與識別資訊。
- 要求完整閱讀可取得的論文內容，涵蓋摘要、方法、實驗、圖表、附錄與補充資料。
- 輸出語意化 HTML 報告，並以繁體中文撰寫。
- 重要公式必須使用 MathML，不使用 LaTeX 文字或 Unicode 近似表示。
- 能抽取圖表時，要求以 base64 圖片嵌入 HTML。
- 內建音訊 Deepfake 偵測相關性分析，即使原論文不是該領域也會明確標示推論部分。

## 適用情境

- 深入理解單篇 AI、ML、訊號處理或安全相關論文。
- 為博士班研究、實驗設計、paper meeting 或研究筆記產出高密度報告。
- 檢查論文方法、架構、公式與實驗設計是否可重現。
- 分析方法是否能轉用於 spoofing、synthetic speech、replay 或 voice conversion detection。
- 將論文內容整理成可直接閱讀、保存或後續加工的 HTML 研究報告。

## 輸入格式

請提供且只提供一篇論文，例如：

```text
Use $phd-paper-analysis to produce an exhaustive Traditional Chinese HTML analysis of this paper: https://arxiv.org/abs/xxxx.xxxxx
```

也可以使用：

- 本地或上傳的 PDF
- 論文 URL
- DOI
- arXiv ID
- 精確論文標題
- 完整 citation

如果一次提供多篇論文，skill 會要求使用者確認只分析第一篇，或分成多次獨立執行。

## 報告內容

產出的 HTML 報告應包含以下章節：

1. Executive Summary
2. Research Context
3. Method Deep Dive
4. Formula Analysis
5. Architecture Figures
6. Experimental Analysis
7. Ablation Study Analysis
8. Reproducibility
9. Critical Review
10. Audio Deepfake Detection Relevance
11. Research Notes

報告會優先使用論文中的頁碼、章節、圖號、公式與表格作為引用依據。若部分內容無法存取，例如附錄、補充資料或圖像抽取失敗，報告必須明確說明限制，不得補造不存在的細節。

## HTML 與公式要求

報告輸出必須是有效 HTML，並使用語意化結構：

```html
<article>
  <h1></h1>
  <section></section>
  <h2></h2>
  <h3></h3>
  <table></table>
  <figure></figure>
  <figcaption></figcaption>
</article>
```

重要公式必須使用 MathML：

```html
<math xmlns="http://www.w3.org/1998/Math/MathML">
  ...
</math>
```

寬公式應放在可水平捲動的容器中，避免破壞版面。交付前需確認 MathML 標籤完整、沒有未解析的公式 placeholder，且公式不會超出報告版面。

## Repository 結構

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── LICENSE
└── README.md
```

- `SKILL.md`: Codex skill 的主要行為規格與品質要求。
- `agents/openai.yaml`: OpenAI/Codex 介面顯示名稱、簡介與預設 prompt。
- `LICENSE`: 專案授權條款。

## 使用方式

在支援 Codex skills 的環境中安裝或引用此 repository 後，使用 `$phd-paper-analysis` 呼叫 skill：

```text
Use $phd-paper-analysis to produce an exhaustive Traditional Chinese HTML analysis of this paper: [PDF, DOI, arXiv ID, title, citation, or URL].
```

建議在 prompt 中補充你特別關心的分析角度，例如：

- 方法與架構細節
- 公式推導與符號解釋
- 實驗結果與 ablation
- 可重現性與實作陷阱
- 音訊 Deepfake 偵測可遷移性

## 品質原則

- 不分析多篇論文，除非使用者明確要求拆成多次獨立分析。
- 不宣稱已閱讀無法取得的章節、附錄或補充資料。
- 不編造 citation、實驗數據、圖表內容或 released code 狀態。
- 區分論文證據與研究者推論。
- 對缺失資訊、負面結果與限制保持明確描述。

