# 設計系統：[專案名稱]

## 1. 視覺氛圍

（用具體形容詞描述整體情緒、資訊密度與動態強度。
範例：「克制的展覽館氛圍，非對稱版面配置，搭配流暢的彈簧物理動態。
整體感受冷靜但有溫度，像一間採光良好的建築設計工作室。」）

## 2. 色彩系統

- primary（#XXXXXX）— [描述性色彩名稱]：唯一強調色，用於 CTA、active 狀態、focus ring（飽和度 < 80%。禁用紫色／霓虹色。）
- background（#F9FAFB）— 畫布白：主要背景底色
- surface（#FFFFFF）— 純白面：卡片與容器填色
- foreground（#18181B）— 炭墨黑：主要文字
- muted（#71717A）— 霧鋼灰：次要文字、說明、metadata
- border（rgba / #XXXXXX）— 細線：卡片邊框、1px 結構線

## 3. 字型規則

- **Hero：** `font-display` → [字體名稱] — `text-6xl font-bold tracking-tight` — 頁面主標語、Banner 大字，每頁最多出現一次
- **Title：** `font-display` → [字體名稱] — `text-4xl font-semibold tracking-tight` — Section 標題、頁面 H1
- **Subtitle：** `font-sans` → [字體名稱] — `text-2xl font-medium tracking-tight` — 卡片標題、H2/H3、模組小標
- **Body-lg：** `font-sans` → [字體名稱] — `text-lg leading-relaxed max-w-[65ch]` — 文章長文、Landing page 引言段落
- **Body-sm：** `font-sans` → [字體名稱] — `text-base leading-relaxed max-w-[65ch]` — 一般正文、側欄說明、表單 helper text
- **Caption：** `font-sans` → [字體名稱] — `text-sm leading-normal text-muted` — 圖片說明、日期、metadata
- **Label：** `font-sans` → [字體名稱] — `text-sm font-medium tracking-wide` — 按鈕文字、tag、badge、表單 label
- **Mono：** `font-mono` → [字體名稱] — `text-sm` — 程式碼、SKU、時間戳記、高密度數字
- **禁用：** Inter、通用系統字體。Dashboard 禁用 `font-display`（serif）。

## 4. 元件樣式

- **按鈕：** `bg-zinc-900 text-white px-6 py-2.5 rounded-xl font-medium transition-transform active:-translate-y-px` — 無外發光，按壓觸覺回饋
- **卡片：** `rounded-2xl border border-zinc-100 bg-white p-6 shadow-sm shadow-zinc-200/50` — 僅在層級需要陰影時使用

## 5. 版面原則

（Grid 優先的響應式架構。優先使用非對稱分割版面。
`md:` 以下收合為單欄。使用 `max-w-7xl mx-auto` 約束最大寬度。
所有互動元素最小 `min-h-[44px]`。）

## 6. 動態與互動

CSS 優先 — 僅在需要彈簧物理、交錯編排或無限循環時使用 Motion library。

- **Hover：** `transition-[property] duration-200 ease-[cubic-bezier(0.4,0,0.2,1)]`
- **進場 & 離場：** `transition-[property] duration-300 ease-out`
- **跨畫面移動：** `transition-[property] duration-500 ease-in-out`
- **Spring 預設（Motion）：** `transition={{ type: "spring", stiffness: 100, damping: 20, mass: 1 }}`
- **快速 Spring（Motion）：** `transition={{ type: "spring", stiffness: 300, damping: 25, mass: 0.5 }}`

僅動畫 `transform` 與 `opacity` — 禁止動畫 layout 屬性。

## 7. 禁用模式

（明確列出所有禁用項目：禁用 emoji、禁用 Inter、禁用純黑色、
禁用霓虹外發光、禁用三欄等寬卡片、禁用 AI 文案陳腔濫調、
禁用通用佔位名稱、禁用捏造數據。）
