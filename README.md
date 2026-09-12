# skill-portability

Skill 可移植性實驗：把一份在 Claude 上建好的提示詞工作流（skill：法文原文 → 繁中，並轉成指定文體），
貼進免費版 Gemini Gems，量測效益保留多少、損耗在哪。2026-07-17 至 07-18 完成，已結案。

狀態的單一事實來源是 [PROGRESS.md](PROGRESS.md)，這份 README 只做導覽。

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

- **評分**：rubric 忠實 30 / 語域 25 / 自然 25 / 格式 20；使用者單人盲評，逐筆單獨評分。
- **次數**：M1 每格 3 次；M2 Gemini 端每格 2 次、REF 3 次（不對稱，報告方法節有註記）。

## 結果（平均分）

| 條件 | 文學 | 新聞 | 社群 |
|---|---|---|---|
| REF | 98.3 | 86.7 | 60.0 |
| A | 92.7 | 95.0 | 79.5 |
| B | 90.0 | 80.0 | 70.0 |
| B' | 90.0 | — | — |
| C | 61.7 | 52.5 | 80.0 |

- 文學格移植效益大部分保留（A−C = +31.0），損耗集中在語域與自然度（REF−A = +5.7）。
- 社群格翻盤：skill 的社群規則方向錯誤，照規則做得越徹底分數越低（內容層錯誤被執行層放大）。
- B 條件的自檢比 A 誠實；B 與 B' 在文學格沒有差異。

細節見 `eval/results_M1.md`、`eval/results_M2.md`。

## 目錄

| 路徑 | 內容 |
|---|---|
| `skill/SKILL.md` | Claude 版 skill v1 |
| `gem-instructions/` | 條件 A / B / B' / C 貼進 Gem 的指令 |
| `inputs/` | T1–T5 法文原文，來源 fr.wikisource.org，各檔含 metadata |
| `outputs/` | 35 筆原始輸出；`_excluded` 為受個人系統提示污染、不入評分的批次 |
| `eval/` | rubric、執行手冊、盲測包（`blind/S-01`–`S-31`）、對照表、評分表、結果 |
| `logs/` | 001–009 迭代日誌 |
| `report/` | 報告正文 `report_body.*`、附錄 A–E `report_appendices.*`、原始輸出包 `outputs_all_35.zip`、正文改版來源 `draft.md` |

## 已知不一致

- 「人工判準的位置」一節（commit `31d6cba`，2026-09-04）只加在 `report/report_body.docx`，
  `report_body.md` 與 `draft.md` 都沒有。
- PROGRESS 記載的改版流程用 Word COM 輸出 .docx，那是 Windows 的做法，這台 Mac 不能照跑。
- PROGRESS 末段的「檔案地圖」與「已決事項 1」（`D:\` 路徑、未 git init）是 07-17 初期內容，已過時。

## 後續

本實驗延伸出 ncucareer-skill（職涯訪談 → 社群貼文），承接社群格翻盤的發現。見 PROGRESS「後續專案銜接」。
