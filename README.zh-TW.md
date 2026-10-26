# skill-portability

[English](README.md) | 繁體中文

Skill 可移植性實驗：把一份在 Claude 上建好的提示詞工作流（skill：法文原文 → 繁中，並轉成指定文體），
貼進免費版 Gemini Gems，量測效益保留多少、損耗在哪。2026-07-17 至 07-18 完成，已結案。

## 主要結果

| 條件 | 文學 | 新聞 | 社群 |
|---|---|---|---|
| REF | 98.3 | 86.7 | 60.0 |
| A | 92.7 | 95.0 | 79.5 |
| B | 90.0 | 80.0 | 70.0 |
| B' | 90.0 | — | — |
| C | 61.7 | 52.5 | 80.0 |

平均分，滿分 100。

- **文學格的移植效益大部分保留**：A−C = +31.0。損耗集中在語域與自然度（REF−A = +5.7）。
- **社群格翻盤**：C 80.0 / A 79.5 / B 70.0 / REF 60.0。skill 的社群規則方向錯誤，照規則做得越徹底分數越低，也就是內容層的錯誤被執行層放大。
- **壓縮版自檢比較誠實**：新文體裡條件 B 的自檢 4/4 誠實標出 ✗，條件 A 0/4。B 與 B'（加回範例）在文學格沒有差異。

細節見 [`eval/results_M1.md`](eval/results_M1.md)、[`eval/results_M2.md`](eval/results_M2.md)，方法上的決定與結論整理在 [`docs/DECISIONS.md`](docs/DECISIONS.md)。

## 實驗設計

- **文本**：T1 波特萊爾〈窗〉（Les Fenêtres）。`inputs/` 另有 T2–T5，未進入評測。
- **目標文體**：文學（LIT）、新聞（NEWS）、社群（SOC）。
- **條件**：

  | 代號 | 內容 |
  |---|---|
  | REF | Claude 參照組，隔離 subagent 執行完整 skill |
  | A | Gemini Gem，指令欄貼 `SKILL.md` 全文（9,981 字元） |
  | B | Gemini Gem，壓縮版指令（3,665 字元） |
  | B' | B 加回範例（5,192 字元），只跑文學 |
  | C | Gemini Gem，baseline 指令 `Follow the user's request.` |

- **評分**：rubric 忠實 30／語域 25／自然 25／格式 20；使用者單人盲評，逐筆單獨評分。
- **次數**：M1 每格 3 次；M2 Gemini 端每格 2 次、REF 3 次（不對稱，報告方法節有註記）。

## 目錄

| 路徑 | 內容 |
|---|---|
| `skill/SKILL.md` | Claude 版 skill v1 |
| `gem-instructions/` | 條件 A／B／B'／C 貼進 Gem 的指令 |
| `inputs/` | T1–T5 法文原文，來源 fr.wikisource.org，各檔含 metadata |
| `outputs/` | 35 筆原始輸出；`_excluded` 是受個人系統提示污染、不入評分的批次 |
| `eval/` | rubric、執行手冊、盲測包（`blind/S-01`–`S-31`）、對照表、評分表、結果 |
| `logs/` | 001–009 迭代日誌 |
| `report/` | 交給老師的正文 `report_body.docx` 與附錄 A–E `report_appendices.docx`；文字版 `report_body.md`、`report_appendices.md`；正文改版來源 `draft.md`；大綱 `outline_v0.md` |
| `docs/DECISIONS.md` | 方法上的決定、兩個里程碑的結論、已知資料瑕疵 |

## 閱讀時要注意

- **M1 解盲以 [`eval/blind_key.md`](eval/blind_key.md) 為準。** 盲測包當天產生過兩次，另一份對照表（`blind_key_DO_NOT_OPEN.md`）屬於被覆蓋掉的那批，和實際的 `eval/blind/S-01`～`S-09` 對不上，已刪除。報告附錄與 `eval/scoring_sheet_M1.md` 仍寫著那個舊檔名；報告已交出，維持原樣。評分沒有受影響，交叉驗證見 [`docs/DECISIONS.md`](docs/DECISIONS.md)。
- **正文的完整版是 `report_body.docx`。** 「人工判準的位置」一節（2026-09-04）只加在 docx，`report_body.md` 與 `draft.md` 都沒有。
- 交給老師的 zip 附件（39 檔）就是 `outputs/` 加 `gem-instructions/`，repo 裡都有逐字相同的副本，所以沒有另外存一份 zip。

## 後續

本實驗延伸出 ncucareer-skill（職涯訪談 → 社群貼文），承接社群格翻盤的發現，見 [`docs/DECISIONS.md`](docs/DECISIONS.md)。
