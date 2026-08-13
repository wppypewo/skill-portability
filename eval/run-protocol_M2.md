# 第二階段執行手冊(M2)

## 範圍(2026-07-17 定案:16 筆版,n=2)

| 批次 | 條件 × 文體 | 筆數 |
|------|------------|------|
| 一 | B × LIT × 2、B' × LIT × 2 | 4 |
| 二 | A、B、C × NEWS × 2 | 6 |
| 三 | A、B、C × SOC × 2 | 6 |

- B' 只跑文學(範例變因在文學格檢驗);新文體不跑 B'。
- REF × NEWS/SOC 已由 Claude 端以 n=3 跑完;與 Gemini 端 n=2 不對稱,報告方法節註記。
- 命名沿用:`{條件}-{文體}-T1-r{n}-{日期}.md`,B' 寫作 `Bp`(如 `Bp-LIT-r1`)。

## 執行規則(沿用 M1)

每 run 開新對話;同條件同日;訊息逐字貼;輸出逐字複製;記錄介面顯示模型名稱;metadata 格式同 M1;命名 `{條件}-{文體}-T1-r{n}-{日期}.md`(條件 B' 寫作 `Bp`)。

## 凍結版使用者訊息模板

### NEWS × T1(整段為一則訊息)

```
目標文體:新聞體改寫(資訊導向、語域中性)

請將以下法文文本轉換為繁體中文。

LES FENÊTRES

Celui qui regarde du dehors à travers une fenêtre ouverte, ne voit jamais autant de choses que celui qui regarde une fenêtre fermée. Il n’est pas d’objet plus profond, plus mystérieux, plus fécond, plus ténébreux, plus éblouissant qu’une fenêtre éclairée d’une chandelle. Ce qu’on peut voir au soleil est toujours moins intéressant que ce qui se passe derrière une vitre. Dans ce trou noir ou lumineux vit la vie, rêve la vie, souffre la vie.

Par delà des vagues de toits, j’aperçois une femme mûre, ridée déjà, pauvre, toujours penchée sur quelque chose, et qui ne sort jamais. Avec son visage, avec son vêtement, avec son geste, avec presque rien, j’ai refait l’histoire de cette femme, ou plutôt sa légende, et quelquefois je me la raconte à moi-même en pleurant.

Si c’eût été un pauvre vieux homme, j’aurais refait la sienne tout aussi aisément.

Et je me couche, fier d’avoir vécu et souffert dans d’autres que moi-même.

Peut-être me direz-vous : « Es-tu sûr que cette légende soit la vraie ? » Qu’importe ce que peut être la réalité placée hors de moi, si elle m’a aidé à vivre, à sentir que je suis et ce que je suis ?
```

### SOC × T1

同上,僅首行改為:

```
目標文體:社群短文體(口語、精簡、繁中網路語感)
```

### LIT × T1(B、B' 補跑用)

同 M1 模板(`eval/run-protocol_M1.md`),首行「目標文體:文學翻譯(保留詩性語言與意象密度)」。
