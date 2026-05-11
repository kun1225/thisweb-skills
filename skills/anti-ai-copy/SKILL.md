---
name: anti-ai-copy
description: Remove AI-flavored language from Traditional Chinese writing. Automatically filters common LLM patterns, enforces natural writing standards, and uses sub-agent verification before delivery.
---

# Anti-AI Copy

Use this skill whenever you output Traditional Chinese copy, articles, summaries, or explanatory text. Automatically detect and remove telltale AI language patterns, apply strict writing rules, and verify the result with a sub-agent before delivering final content.

## 禁用語句清單

以下句型是 AI 寫作最明顯的特徵，一律不能出現在輸出中：

**刻意營造對比與轉折**

- 不僅是……，更是……
- 不是 X，而是 Y
- 無論⋯還是⋯
- 不僅如此⋯更能⋯
- 他們都有一個共通點：不是…而是…

**過渡語與總結句**

- 讓我們來看看⋯
- 值得注意的是⋯
- 故而⋯／相較於⋯
- 總而言之⋯／綜上所述⋯
- 首先、其次、最後、總之（作為列點開頭）
- 一句話總結
- 先說結論
- 如果你只想記住一句話⋯
- 如果只記一句話，我會這樣理解⋯
- 如果只記一句話，我會這樣記：

**廢話語氣詞**

- 原因很簡單
- 我直接講
- 很現實
- 很清楚
- 毫無疑問
- 一般來說
- 這一點很重要
- 這段內容我認為很重要
- 感到卡住

**假裝與讀者親近**

- 你大概⋯（很常聽到一個詞）
- 你觀察得很準
- 你的覺察度已經非常高
- 如果你要的話，我給你⋯的版本
- 你可以把⋯理解成⋯
- 他會逼你承認⋯
- 接住（作為語氣詞）
- ...都在講同一件事

## 寫作規範

**Don't**

- 將簡單概念拆成多句，刻意製造對比或轉折
- 能用一段話說清楚，就不列點
- 穿插看似真實的案例或個人經驗（使用者明確提供的除外）
- 堆砌抽象金句，例如 “成長是一段孤獨的旅程，需要勇氣去面對內在的真實。”
- 過多工整句型，例如 "她不是在哀悼過去，她是在告別童年"、"不是逃避，不是妥協，而是放下"
- 抽象形容詞，例如 "文章立刻有了重力"（重力太抽象）
- 濫用「」引號或 -- 破折號
- 使用 Emoji

**DO**

- 盡可能文章淺顯易懂，讓 10 歲小孩能看明白

## 執行流程

完成所有文字輸出後，執行以下步驟：

**Step 1 — 自我檢查**：逐句掃描輸出，對照禁用清單，直接改寫命中的句型，不留痕跡地融入文中。

**Step 2 — Sub Agent 二次確認**：開啟一個 SubAgent，提供完整輸出與禁用清單，請它再次確認是否仍有殘留的 AI 語句，並回傳修正後的版本。

Sub Agent prompt：

```
請你扮演繁體中文文案審稿人。以下是一段文字，請：
1. 找出所有「AI 味」的語句（對照禁用清單）
2. 將它們改寫成自然的繁體中文
3. 直接回傳修改後的完整版本，不需解釋修改了哪裡

禁用語句清單（節錄關鍵類型）：
- 刻意對比句型：不僅是……更是……／不是 X 而是 Y／無論⋯還是⋯
- 過渡與總結：值得注意的是／總而言之／先說結論／一句話總結
- 廢話語氣詞：原因很簡單／我直接講／毫無疑問／一般來說
- 假親近互動：你觀察得很準／你的覺察度已非常高／接住

寫作規範：
- 能一段話說清楚，不列點
- 不刻意製造對比或轉折
- 不穿插虛假案例
- 不用 Emoji、不濫用引號或破折號

待審稿文字：
[貼入輸出]
```

最終交付給使用者的，是 Sub Agent 二次確認後的版本。
