# 第一里程碑執行手冊(T1 × 文學翻譯 × 條件 A/C)

## 範圍

- 文本:T1《Les Fenêtres》
- 文體:文學翻譯(LIT)
- 條件:A(直接移植)、C(裸跑)
- 每格 3 次(已定案 2–3 次;建議取 3,變異數較可判讀。若免費額度吃緊,至少 2 次)
- 合計:2 條件 × 3 runs = 6 筆 Gemini 輸出
- Claude 參照組(REF):由 Claude 端跑 3 次,不佔你的 Gemini 額度

## 執行規則

1. **每一 run 開新對話**:同一 Gem 內,每次都從全新對話開始,不得在同一對話連跑(前文會污染)。
2. **同日跑完同條件**(已定案慣例):A 的 3 次同一天;C 的 3 次同一天;最好 A、C 同天。
3. **訊息逐字貼**:使用下方標準訊息模板,不增刪一字。
4. **輸出逐字複製**:包含 Gemini 輸出的所有格式(標題、列表、勾選符號),不修飾、不補全。若輸出被截斷,照實保留並在異常備註記「輸出截斷」。
5. **記錄介面顯示的模型名稱**(如 2.5 Flash 等字樣,可見就照抄;不可見填 N/A)。
6. **建 Gem 時記錄**:指令欄是否觸發字數上限;若截斷,記下最後保留的段落或規則 ID。

## 標準使用者訊息模板(LIT × T1,凍結版)

以下整段為一則訊息,逐字貼入:

```
目標文體:文學翻譯(保留詩性語言與意象密度)

請將以下法文文本轉換為繁體中文。

LES FENÊTRES

Celui qui regarde du dehors à travers une fenêtre ouverte, ne voit jamais autant de choses que celui qui regarde une fenêtre fermée. Il n’est pas d’objet plus profond, plus mystérieux, plus fécond, plus ténébreux, plus éblouissant qu’une fenêtre éclairée d’une chandelle. Ce qu’on peut voir au soleil est toujours moins intéressant que ce qui se passe derrière une vitre. Dans ce trou noir ou lumineux vit la vie, rêve la vie, souffre la vie.

Par delà des vagues de toits, j’aperçois une femme mûre, ridée déjà, pauvre, toujours penchée sur quelque chose, et qui ne sort jamais. Avec son visage, avec son vêtement, avec son geste, avec presque rien, j’ai refait l’histoire de cette femme, ou plutôt sa légende, et quelquefois je me la raconte à moi-même en pleurant.

Si c’eût été un pauvre vieux homme, j’aurais refait la sienne tout aussi aisément.

Et je me couche, fier d’avoir vécu et souffert dans d’autres que moi-même.

Peut-être me direz-vous : « Es-tu sûr que cette légende soit la vraie ? » Qu’importe ce que peut être la réalité placée hors de moi, si elle m’a aidé à vivre, à sentir que je suis et ce que je suis ?
```

(說明:卷次編號「XXXV」為版本體例,非詩文內容,不納入;標題保留。)

## 歸檔命名

`outputs/{條件}-{文體}-{文本}-r{次}-{日期}.md`
例:`outputs/A-LIT-T1-r1-2026-07-18.md`

(規格原命名無 run 編號;因先導階段每格多次,加 `-r{n}`。)

## 每檔開頭 metadata(逐欄填)

```
---
條件: A
文體: LIT
文本: T1
run: r1
日期: 2026-07-18
介面顯示模型: (照抄或 N/A)
Gem指令截斷: 無 / 截至「…」
異常備註: 無
---
```

metadata 之後貼 Gemini 完整輸出。歸檔後告知 Claude,由 Claude 檢查完整性、執行盲測編排。
