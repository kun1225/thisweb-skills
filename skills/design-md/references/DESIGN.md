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

- **專案語言：** [說明主要內容語言：Latin only / CJK primary / Mixed。若為 Mixed，說明哪些 token 使用 Latin 字體、哪些 token 使用 CJK 字體。]
- 字體 token 名稱必須直接對應語義層級，禁止把多個層級共用成 `font-sans` 或 `font-display`
- **Hero：** `font-hero` → [字體名稱] — `text-[clamp(2.75rem,6vw,5rem)] font-bold` — 頁面主標語、Banner 大字，每頁最多出現一次
- **Title：** `font-title` → [字體名稱] — `text-[clamp(2rem,4vw,3.5rem)] font-semibold` — Section 標題、頁面 H1
- **Subtitle：** `font-subtitle` → [字體名稱] — `text-[clamp(1.25rem,2.4vw,2rem)] font-medium` — 卡片標題、H2/H3、模組小標
- **Body-lg：** `font-body-lg` → [字體名稱] — `text-lg leading-relaxed max-w-[65ch]` — 文章長文、Landing page 引言段落
- **Body-sm：** `font-body-sm` → [字體名稱] — `text-base leading-relaxed max-w-[65ch]` — 一般正文、側欄說明、表單 helper text
- **Caption：** `font-caption` → [字體名稱] — `text-sm leading-normal text-muted` — 圖片說明、日期、metadata
- **Label：** `font-label` → [字體名稱] — `text-sm font-medium` — 按鈕文字、tag、badge、表單 label
- **Mono：** `font-mono` → [字體名稱] — `text-sm` — 程式碼、SKU、時間戳記、高密度數字
- **規則：**
  - CJK 正文的 `line-height` 維持在 `1.2em` 到 `1.5em` 之間，依密度與字級調整，不要為了緊湊而再壓低
  - 標題優先使用 `clamp(...)` 做 responsive scaling，正文維持穩定
  - Dashboard / software UI 禁用 serif-backed title tokens
  - 禁用 Inter。若使用 serif，避免 generic serifs（如 `Times New Roman`、`Georgia`、`Garamond`）

## 4. 元件樣式

所有帶顏色語意的 class（`text-*`、`bg-*`、`border-*`、`ring-*`、`shadow-*`、`hover:*`、`focus:*`、`active:*`、`from-*`/`to-*` 等）一律只能使用第 2 節定義的語義 token。

禁止範例：`text-zinc-900`、`bg-white`、`border-zinc-200`、`hover:bg-zinc-100`、`text-[#ddd]`、`ring-zinc-400`

- **主要按鈕：** `bg-foreground text-background px-6 py-2.5 rounded-xl font-medium transition-all duration-200 hover:bg-foreground/90 active:-translate-y-px focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary` — 無外發光，按壓觸覺回饋
- **次要按鈕：** `bg-transparent text-foreground border border-border px-6 py-2.5 rounded-xl font-medium transition-all duration-200 hover:bg-surface active:-translate-y-px focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary`
- **卡片：** `rounded-2xl border border-border bg-surface p-6 shadow-sm shadow-border/50 hover:shadow-md hover:shadow-border/30 transition-shadow duration-200` — 僅在層級需要陰影時使用；高密度版面改用 `border-t border-border` 分隔線取代

## 5. 版面原則

- 每個 section 依內容型態、資訊密度、層級與互動需求決定版面，不預設整頁只能有單一 layout
- 描述每個 section 為什麼需要某種結構，例如比較型 grid、editorial stack、tool workspace、data-dense panel，而不是套用通用模板
- Grid-first responsive architecture，但不要把 `max-w-* mx-auto` 當成預設頁面 containment
- 定義動態 page-edge token，並以 `padding-inline` 做頁面邊緣約束：

```css
:root {
  --spacing-contain-max: 1600px;
  --spacing-edge: max(
    max(min(3.5vw, 96px), 8px),
    calc((100vw - var(--spacing-contain-max)) / 2)
  );
}
```

- 頁面邊緣統一使用 `px-edge`，不要用 `mx-edge`；這樣在有 scrollbar 時寬度計算較一致
- 非對稱在有助於層級或掃視時優先，但每個 section 可依內容選擇 stacked、split、grid、rail 或 freeform composition
- 多欄版面在 `md:` 以下收合為單欄

## 6. 動態與互動

CSS 優先 — 僅在需要彈簧物理、交錯編排或無限循環時使用 Motion library。

**Easing 選法（三步驟）：**

1. **選 easing family** — 依品牌個性挑選（SINE 最柔、QUAD/CUBIC 日常 UI、QUART/QUINT 強調感、EXPO 戲劇性、BACK/ANTICIPATE 有彈性）
2. **選方向變體** — `Out`（元素進場、減速到位，最常用）、`InOut`（畫面間移動）、`In`（元素離場，少用）
3. **套用對應 cubic-bezier**

**常用模式：**

- **Hover：** `transition-[property] duration-200 ease-[cubicOut]`
- **進場 & 離場：** `transition-[property] duration-300 ease-[cubicOut]` 或 `ease-[quartOut]`
- **跨畫面移動：** `transition-[property] duration-500 ease-[cubicInOut]`
- **Spring 預設（Motion）：** `transition={{ type: "spring", stiffness: 100, damping: 20, mass: 1 }}`
- **快速 Spring（Motion）：** `transition={{ type: "spring", stiffness: 300, damping: 25, mass: 0.5 }}`

僅動畫 `transform` 與 `opacity` — 禁止動畫 layout 屬性。

## 7. 禁用模式

（明確列出所有禁用項目：禁用 emoji、禁用 Inter、禁用純黑色、
禁用霓虹外發光、禁用三欄等寬卡片、禁用 AI 文案陳腔濫調、
禁用通用佔位名稱、禁用捏造數據。）
