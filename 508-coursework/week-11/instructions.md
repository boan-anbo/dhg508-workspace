# Week 11 · Final End-to-End Run, Overleaf Design Paper (`biblatex-chicago`), and Post-Mortem

Prepare for our final class on **Wednesday 25 November 2026**.

**Minimal Overleaf-ready template in this folder:**
- Upload directly to Overleaf: [`dhg508-overleaf-template.zip`](dhg508-overleaf-template.zip)
- Unpacked source files: [`paper-template/`](paper-template/) (`main.tex`, `references.bib`, `evidence-table.tex`, `evidence.csv`, `make_evidence_table.py`)

**Mention your difficulties.**

## Overview: Finish, Run Cleanly, and Submit

Next Wednesday (**25 November**) is effectively your **final hand-in**. Once you finish the steps below and show your working build and compiled PDF paper in class, your final coursework for DHG508 is complete.

### 1. What "finished" means (end-to-end runnability, not commercial perfection)

You do **not** need commercial-studio polish or last-minute extra features. Do **not** start new modules this week. We want **one coherent work that runs cleanly from start to finish**:

1. **Public build works:** Your live `https://` URL on Cloudflare Pages (plus Worker if calling a live model API) opens and runs end-to-end on another computer or phone without dead buttons, `"TODO"` placeholders, or raw JSON dumps.
2. **Automated checks pass:** Your unit/integration tests (`Vitest` or `pytest`) and automated browser smoke test (`Playwright`) run from a single command and pass.
3. **Design paper & post-mortem compile on Overleaf (`biblatex-chicago`):** Your short paper (`main.tex` → PDF) compiles cleanly on **Overleaf** with **XeLaTeX + Biber** using **`biblatex-chicago`** (Chicago 18th ed. Notes-Bibliography), pulling its evidence table from your CSV file and its footnotes/bibliography from `references.bib`, with both the compiled PDF and `.tex`/`.bib` sources saved back into your Git repository.
4. **Clear `README.md`:** Anyone opening your GitHub repository can immediately find your live URL and run your project and tests locally.

**If a stubborn final bug remains:** Do not panic or hide it. Document the exact error message, what you tried, and how to reproduce it, and bring it to class next Wednesday—we will help diagnose and fix any remaining final bugs together before you lock in your submission.

### 2. Optional post-class upgrade with frontier models (and how grading works)

Over the coming weeks, if **anyone** wants to push their project further—for a capstone, thesis portfolio, or public showcase—**tell Bo**. Because platform Team plans do not support shared seat delegation for this workflow, Bo has set up dedicated access to **stronger frontier models** and will work with you directly over the next few weeks to upgrade and refine your project.

- **Fair grading boundary:** **Any frontier-model upgrade Bo helps run after submission will NOT count toward your course grade.** You will not lose a single point if you do not opt in, and frontier-model assistance will not inflate anyone's mark.
- **What your grade rests on:** Your grade continues to be evaluated strictly on **your own work, reasoning, and process**: your historical/cultural question and source grounding (`据 / 推断 / 设`), your own iterative workflow (`plan.md`, schematics, automated tests, user-feedback fixes), a working end-to-end build, and the honesty and precision of your **post-mortem**.

---

## Step-by-Step Guide to Completing Everything

### Step 1 · Freeze features and lock down your live build

1. **Freeze scope.** In `docs/plan.md` (or your design document), mark your feature scope as frozen. Fix broken interactions rather than adding new rooms, characters, or pages.
2. **Add a short on-page Historical & AI Note.** Somewhere visible on your start screen, footer, or `About` modal, include 3–5 clear sentences telling a public visitor:
   - what historical or cultural situation the work represents;
   - how documented facts (`据`), historical inferences (`推断`), and design inventions (`设`) are distinguished;
   - which AI models or tools power or built the experience.
3. **Audit secrets and large files.** Confirm `.env`, `.dev.vars`, and API keys are in `.gitignore` (and never in Git history or frontend JS), and keep multi-megabyte raw binaries or caches in gitignored `artifacts/` with rebuild notes.
4. **Re-deploy and re-test.** Deploy your latest clean build to Cloudflare Pages and run your `Vitest`/`pytest` and `Playwright` checks against both `localhost` and your live `https://` URL.

### Step 2 · Copy the minimal template and generate `evidence-table.tex` from your CSV

We use a simplified single-article version of our Lingnan MADHGA Overleaf template (`main.tex` + `references.bib` + `evidence-table.tex`), pre-configured with **`biblatex-chicago`** (`notes, backend=biber`) and Overleaf-safe CJK fonts (`Noto Serif CJK SC`).

1. Copy [`paper-template/`](paper-template/) into your project folder so Git tracks your paper alongside your code:
   ```bash
   cp -R 508-coursework/week-11/paper-template projects/<your_project>/paper
   ```
   *(If your project lives in its own separate Git repository, copy `508-coursework/week-11/paper-template` into `<your-repo>/paper`.)*
2. Fill `paper/evidence.csv` (or point to your existing `data/<project>-evidence.csv`) with your real project claims and design elements across five columns:
   - `claim`: the specific historical statement, character rule, spatial detail, or mechanic;
   - `evidence`: the source title or project file (`expert-1.json`, `world.json`, etc.);
   - `locator`: exact printed page (and PDF page if different) or file key/zone;
   - `level`: `据` (documented), `推断` (inferred), or `设` (invented for the design);
   - `limit`: one short phrase stating what the source does *not* prove or the temporal cutoff (`[限定]`).
3. Generate `paper/evidence-table.tex` automatically (never type LaTeX table rows by hand):
   ```bash
   python3 paper/make_evidence_table.py
   # Or, if your CSV lives in data/evidence.csv:
   python3 paper/make_evidence_table.py data/evidence.csv paper/evidence-table.tex
   ```

### Step 3 · Write your paper & post-mortem in `main.tex` (`biblatex-chicago`)

Target roughly **1,500–2,500 English words (about 3–6 compiled PDF pages)**. Keep prose concise, concrete, and honest—**you must write your own reasoning and post-mortem**, and personally verify every citation and page number against your reading notes and original pages.

#### How citations work (`biblatex-chicago` Notes-Bibliography)
- The template loads `\usepackage[notes, backend=biber, autolang=other, isbn=false]{biblatex-chicago}` and `\addbibresource{references.bib}`.
- Place `\autocite[page]{key}` **after punctuation** to generate Chicago 18th edition footnotes automatically, for example:
  ```latex
  Demand-management policy never produces a certain result.\autocite[150]{tobin1986macro}
  ```
- Export your bibliography into `references.bib` in **BibLaTeX** format (for example via Zotero + Better BibTeX; for Chinese/CJK romanization, characters, and English glosses `titleaddon` / `usere`, see the sample entries in [`paper-template/references.bib`](paper-template/references.bib) or [`cite-non-english`](https://github.com/boan-anbo/cite-non-english)).
- `\printbibliography[title={Bibliography}]` at the bottom of `main.tex` prints the formatted bibliography automatically.

#### Six required sections in `main.tex`
1. **Historical Question & Why This Medium Matters:** State both your historical/cultural question and your design question. Answer *"Why this medium?"*—what does a user understand by acting, choosing, or exploring inside your work that a plain essay or video would not show?
2. **Sources, Limits, and Scholarly Conversation:** Present your primary sources with exact locators and state their inherent limits (translation, OCR noise, edition, missing viewpoints). Engage with **at least three relevant scholarly works** cited via `\autocite[page]{key}` from `references.bib`, showing how their arguments informed or challenged your design.
3. **System Architecture & Epistemic Boundaries:** Explain how your data, rules/prompts, UI/engine, and Cloudflare deployment connect, and state the hard temporal/epistemic boundaries (`[限定]`) enforced on your system. Export your Week 10 schematic (HTML diagram, Excalidraw, or Mermaid) as `schematic.png`, uncomment the `\begin{figure}` block in `main.tex`, and include it.
4. **Reproducible Evidence Table:** Included automatically via `\input{evidence-table.tex}` from Step 2.
5. **Automated Verification & External Playtesting:** Explain what your unit, integration, and browser E2E tests verify (both software logic and historical guardrails), summarize what **at least two external playtesters** experienced on your live URL, and point to the permanent regression tests you added from their feedback.
6. **Post-Mortem & Statement of AI Use:** Ground this section in real commits and entries from your `research_journal.md`:
   - **What worked:** Where agents, skills, schematics, Browser MCP, or automated tests genuinely helped.
   - **What failed, drifted, or hallucinated:** Concrete examples (OCR misreads, goal drift, invented citations, layout/engine bugs, Worker/CORS issues) and how you detected and fixed them.
   - **What changed:** Key design or technical pivots across the term and why you made them.
   - **What this work does *not* claim:** Remaining historical gaps, simplifications, and open questions.
   - **AI disclosure:** Which models, harnesses (e.g. OpenCode), and MCP tools were used at each step, and how you checked outputs against primary and secondary sources.

### Step 4 · Upload and Compile on Overleaf (Verified Workflow)

You can draft in VS Code / OpenCode locally and compile on **Overleaf** (no 5 GB local TeX installation required), or write directly in Overleaf and sync the files back to Git:

1. **Create your Overleaf project:**
   - Open [Overleaf](https://www.overleaf.com/project) → click **New Project → Upload Project** → select [`508-coursework/week-11/dhg508-overleaf-template.zip`](dhg508-overleaf-template.zip) (or zip your own `paper/` folder containing `main.tex`, `references.bib`, `evidence-table.tex`, and `schematic.png`).
2. **Switch Compiler to `XeLaTeX` (required once for Chinese/CJK fonts):**
   - In Overleaf, click **Menu** (top-left Overleaf icon) → under **Settings → Compiler**, change `pdfLaTeX` to **`XeLaTeX`**.
3. **Click `Recompile`:**
   - Overleaf runs `XeLaTeX` and `Biber` automatically, rendering Chinese characters (`Noto Serif CJK SC`), Chicago footnotes, Table 1, and your Bibliography.
4. **Sync back to your Git repository before class:**
   - Click **Download PDF** in Overleaf and save it as `paper/design-paper.pdf` in your Git repository.
   - If you edited text inside Overleaf, also click **Menu → Download → Source** so `paper/main.tex`, `paper/references.bib`, and `paper/evidence-table.tex` in your GitHub repository match the compiled PDF 100%.

*(Optional local compilation: if you already have full TeX Live with `xelatex`, `biber`, and `biblatex-chicago` installed locally, you can also run `cd paper && xelatex main && biber main && xelatex main && xelatex main && cp main.pdf design-paper.pdf`—the exact same files compile both locally and on Overleaf.)*

**How to ask OpenCode to help check your `.tex` & `.bib` before uploading to Overleaf (without letting it ghostwrite your paper):**
> Read `@paper/main.tex`, `@paper/references.bib`, and `@paper/evidence.csv`. Run `python3 paper/make_evidence_table.py` so `evidence-table.tex` updates from my CSV, check that every `\autocite` key in `main.tex` exists in `references.bib` in valid BibLaTeX Chicago format with no unescaped `%`, `&`, or `_` characters, and pack `main.tex`, `references.bib`, `evidence-table.tex`, and `schematic.png` into `paper/overleaf-upload.zip` ready for Overleaf XeLaTeX compilation. Do not invent any citations, page numbers, or post-mortem experiences; flag any missing locator for me to fill in myself.

Open your compiled PDF and check every page yourself: verify that Chinese characters render cleanly, no bold citation keys (like **`[tobin1986macro]`**) appear unresolved, Table 1 fits inside the margins, and every page number matches your actual source.

### Step 5 · Final Repository Checklist & Next Wednesday's Walkthrough

Before class on **Wednesday 25 November**, make sure your pushed GitHub repository contains:

```text
<your_project>/
├── README.md                  # Live https:// URL + 1-command run & test instructions
├── docs/
│   ├── plan.md                # Frozen plan, scope & non-goals
│   ├── schematic.png          # Exported visual schematic (plus .html / .excalidraw / .md source)
│   └── user-feedback.md       # Raw notes from >=2 external testers + fixes & test links
├── data/ (or research/)       # Source notes, research_journal.md, design_doc.md & evidence.csv
├── src/ & tests/              # Clean application/engine source + passing unit/integration/E2E tests
└── paper/
    ├── evidence.csv           # (or linked from ../data/)
    ├── make_evidence_table.py # Script generating evidence-table.tex
    ├── evidence-table.tex     # Auto-generated LaTeX table
    ├── references.bib         # Verified BibLaTeX file (>=3 scholarly works + primary sources)
    ├── main.tex               # Complete 6-section Overleaf-compatible LaTeX source
    └── design-paper.pdf       # Cleanly compiled final PDF downloaded from Overleaf (or local XeLaTeX+Biber)
```

**In class on Wednesday 25 November (Final Class):**
1. Show your **running public URL** end-to-end.
2. Open your compiled **`paper/design-paper.pdf`** (or your live Overleaf tab), point to your Chicago footnotes, generated evidence table, and embedded schematic, and share your **most important post-mortem lesson** (what failed or drifted, and what you learned).
3. If you hit any final bug you could not resolve alone, show the exact error so we can fix it together on the spot, push your final commit, and complete your submission.
4. Let Bo know in class (or right after) if you would like to join the **optional post-class frontier-model upgrade** in the coming weeks.

---

# 第十一週 · 終版跑通、Overleaf 設計論文（`biblatex-chicago`）與專案復盤（Post-Mortem）

請為 **2026 年 11 月 25 日（星期三）**的最後一堂課做好準備。

**本資料夾附帶極簡 Overleaf 模板（已實測在 Overleaf 編譯通過）：**
- 直接上傳 Overleaf 的壓縮包：[`dhg508-overleaf-template.zip`](dhg508-overleaf-template.zip)
- 解壓後的源文件目錄：[`paper-template/`](paper-template/)（內含 `main.tex`、`references.bib`、`evidence-table.tex`、`evidence.csv`、`make_evidence_table.py`）

**請務必如實說明你遇到的困難。**

## 總覽：全流程跑通、寫完論文，下週課後即可完成提交

下週三（**11 月 25 日**）基本上就是本課程的**期末最終交付**。只要按下面步驟把作品全流程跑通、在 Overleaf 寫完並編譯好設計論文與復盤報告（Post-mortem），下週課堂演示確認無誤後即可直接完成期末提交。

### 1. 「完成」的標準：全鏈路跑通即可，不苛求商業級完美

這週**不要再加新功能**，也無需追求商業大作級的複雜包裝。我們要求的標準非常明確——**確定整套作品與證據鏈能從頭到尾乾淨跑通**：

1. **線上版本可完整走通：** 部署在 Cloudflare Pages（及 Worker，如有調用實時 API）的公開 `https://` 網址能在另一台電腦或手機正常打開操作，沒有失效按鈕、`"TODO"` 佔位符或裸露的 JSON 輸出。
2. **自動化測試通過：** 你的單元／集成測試（`Vitest` 或 `pytest`）與瀏覽器冒煙測試（`Playwright`）能一鍵執行並通過。
3. **設計論文與 Post-mortem 在 Overleaf 成功編譯（`biblatex-chicago`）：** 你的短篇設計論文（`main.tex` → PDF）使用 **`biblatex-chicago`**（芝加哥格式第 18 版註釋—書目制，`backend=biber`）在 **Overleaf（XeLaTeX）** 上順利編譯出 PDF，證據表由你的 CSV 自動生成，註腳與參考書目由 `references.bib` 自動生成，並將編譯好的 PDF 與 `.tex`/`.bib` 源文件同步回你的 Git 儲存庫。
4. **`README.md` 清晰可復現：** 任何人打開你的 GitHub 儲存庫，都能一眼看到公開網址，並按說明完成本地運行與測試。

**如果最後還剩個別修不掉的 Final Bug：** 不必焦慮，更不要掩蓋。請把完整的報錯信息、重現步驟與你嘗試過的排查方法記下來帶到下週三課堂，我們現場幫你一起排障修好，再提交最終 commit。

### 2. 課後可選「高階模型升級計劃」與公平評分原則

在接下來的幾週裏，如果**任何同學**希望把自己的專案進一步打磨升級（例如用於畢業作品集、學位論文延伸或公開展示），**歡迎直接告訴 Bo**。由於目前平台的 Teams 方案不具備這種共享席位派發功能，Bo 已專門準備好帳號資源，接下來幾週會用**更高級的前沿模型（Frontier Models）**親自幫有需要的同學把作品升級得更完善。

- **嚴格公平的評分邊界：** **課後由 Bo 用高階模型協助的升級部分，完全不計入本課程成績。** 不參加升級不會扣任何分，參加升級也不會因此額外加分。
- **成績評定依據：** 期末評分依然完全基於**你自己在本學期完成的真實工作與思考**——包括你的歷史／文化問題與史料依據（`據／推斷／設`）、你自己的規劃與測試反饋閉環（`plan.md`、示意圖、自動化測試、用戶反饋修復）、全流程跑通的成品，以及你在 **Post-mortem** 中展現的誠實反思與批判深度。

---

## 完成期末交付的分步詳細指南

### 第一步 · 凍結功能範圍，把線上版本收尾打磨乾淨

1. **凍結功能（Feature Freeze）。** 在 `docs/plan.md`（或設計文件）標明功能封版，集中精力修補現有流程中的斷點，不要再新開未完成的支線。
2. **在作品頁面加上簡短的「歷史邊界與 AI 方法說明」。** 在首頁角落、頁腳或 `About` 彈窗中用 3–5 句話向公眾訪客交代：
   - 作品呈現的歷史或文化情境；
   - 如何區分有直接史料記載的事實（`據`）、歷史推論（`推斷`）與設計虛構（`設`）；
   - 開發或運行中使用了哪些 AI 模型與工具。
3. **檢查密鑰與大型文件。** 確保 `.env`、`.dev.vars` 及各類 API Key 已寫入 `.gitignore`（前端代碼與 Git 歷史中絕無洩露），過大的原始二進制資產或緩存放在不進 Git 的 `artifacts/` 目錄並寫明重建方式。
4. **重新部署並跑通測試。** 將最新乾淨版本推送到 Cloudflare Pages，分別針對 `localhost` 與線上 `https://` 網址跑通 `Vitest`/`pytest` 與 `Playwright` 測試。

### 第二步 · 複製極簡模板，從 CSV 自動生成 `evidence-table.tex`

我們將嶺南 MADHGA 的 Overleaf 論文模板精簡為單文件課程版（`main.tex` + `references.bib` + `evidence-table.tex`），已預先配好 **`biblatex-chicago`**（`notes, backend=biber`）與 Overleaf 原生支援的中文字體（`Noto Serif CJK SC`）。

1. 在 `dhg508-workspace` 根目錄將 [`paper-template/`](paper-template/) 複製進你的專案資料夾，方便 Git 統一管理：
   ```bash
   cp -R 508-coursework/week-11/paper-template projects/<你的專案名>/paper
   ```
   *（若你的專案在獨立 Git 儲存庫，直接將 `508-coursework/week-11/paper-template` 複製到 `<你的儲存庫>/paper`。）*
2. 將你專案真實的史料主張與設計設定填入 `paper/evidence.csv`（或直接使用你現有的 `data/<專案>-evidence.csv`），確保包含五個欄位：
   - `claim`：具體的歷史陳述、人物規則、空間細節或交互機制；
   - `evidence`：史料名稱或對應工程文件名（如 `expert-1.json`、`world.json`）；
   - `locator`：精確印刷頁碼（若 PDF 頁碼不同請同時註明）或文件鍵名；
   - `level`：`據`（史料直接記載）、`推斷`（基於史料推理）或 `設`（為使設計成立而作的設定）；
   - `limit`：一句話寫明該史料**不能證明甚麼**或年代／認知邊界（`[限定]`）。
3. 用腳本自動生成 `paper/evidence-table.tex`（切勿手敲 LaTeX 表格）：
   ```bash
   python3 paper/make_evidence_table.py
   # 若你的 CSV 放在 data/evidence.csv，可傳入路徑：
   python3 paper/make_evidence_table.py data/evidence.csv paper/evidence-table.tex
   ```

### 第三步 · 在 `main.tex` 撰寫設計論文與復盤（`biblatex-chicago` 格式）

篇幅約 **1,500–2,500 英文詞（或同等深度中文，編譯後約 3–6 頁 PDF）**。行文務求簡潔具體、拒絕空洞套話——**核心論證與 Post-mortem 必須由你自己撰寫判斷**，每一條引文與頁碼都必須親自對照閱讀筆記與原頁核實。

#### 引用與書目規範（`biblatex-chicago` 註釋—書目制）
- 模板已載入 `\usepackage[notes, backend=biber, autolang=other, isbn=false]{biblatex-chicago}` 與 `\addbibresource{references.bib}`（請勿改回 `natbib` 或舊版 `bibtex`）。
- 在正文中，將 `\autocite[頁碼]{key}` 放在**標點符號之後**，即可自動生成標準芝加哥第 18 版腳註：
  ```latex
  Demand-management policy never produces a certain result.\autocite[150]{tobin1986macro}
  ```
- 請以 **BibLaTeX** 格式整理 `references.bib`（可用 Zotero + Better BibTeX 導出；中文／東亞文獻的拼音、漢字 `titleaddon` 與英譯 `usere` 寫法請直接參考 [`paper-template/references.bib`](paper-template/references.bib) 示例或 [`cite-non-english`](https://github.com/boan-anbo/cite-non-english) 插件）。
- 文末的 `\printbibliography[title={Bibliography}]` 會自動輸出完整參考書目。

#### `main.tex` 必須涵蓋的六個小節
1. **歷史／文化問題與媒介理由（Historical Question & Why This Medium Matters）：** 寫明你的歷史／文化問題與設計問題，回答*「為甚麼需要做成互動模擬／應用，而不是拍成影片或寫成普通文章？」*——使用者只有透過在其中操作、選擇或試錯才能體會到甚麼？
2. **史料依據、材料局限與學術對話（Sources, Limits & Scholarly Conversation）：** 說明所依據的一手材料及其固有限制（翻譯層、OCR 誤差、版本或視角缺失），並透過 `references.bib` 用 `\autocite[頁碼]{key}` 引用及討論**至少三項相關學術研究**，說明你的設計如何回應、延伸或質疑學者的論點。
3. **系統架構與認知邊界（System Architecture & Epistemic Boundaries）：** 說明數據、規則／Prompt、前端或遊戲引擎以及 Cloudflare 部署如何連接，以及如何防止年代穿越或角色偏移（`[限定]`）。將你在第 10 週生成的專案視覺示意圖導出為清晰的 `schematic.png`，取消 `main.tex` 中 `\begin{figure}` 的註釋並嵌入文中。
4. **可復現證據表（Reproducible Evidence Table）：** 透過 `\input{evidence-table.tex}` 自動載入第二步生成的表格。
5. **自動化驗證與外部實測（Automated Verification & External Playtesting）：** 說明你的單元、集成與 Playwright 瀏覽器測試各自驗證了哪些邏輯與史料邊界，總結**至少兩位外部朋友**在公開網址實測時的真實反饋，以及你據此新增的永久防回歸測試。
6. **誠實復盤與 AI 使用聲明（Post-Mortem & Statement of AI Use）：** 結合你的 `research_journal.md` 與真實 Git 提交歷史，具體交代五件事：
   - **哪些做法真正有效（What worked）：** Agent、Skill、視覺示意圖、Browser MCP 或自動化測試在哪一步真正幫上了忙；
   - **哪些地方失敗、跑偏或產生幻覺（What failed or drifted）：** 給出真實具體例子（例如 OCR 錯字、Goal Drift、編造引文、畫面／引擎報錯、Worker 部署踩坑），以及你如何發現並解決；
   - **設計發生過甚麼改變（What changed）：** 相比最初設想，你調整或刪減了甚麼、原因為何；
   - **本作品不主張甚麼（What this work does *not* claim）：** 坦誠列出尚未解決的史料缺口與技術局限；
   - **AI 方法聲明（AI disclosure）：** 各階段使用了哪些模型、工具（如 OpenCode）與 MCP，以及你本人如何核驗史料與引文。

### 第四步 · 上傳 Overleaf 編譯並同步回 Git（已實測流程）

無需在本機安裝數 GB 的完整 TeX 環境——你可以在本地用 VS Code / OpenCode 整理文件後上傳 **Overleaf** 編譯，也可以直接在 Overleaf 撰寫再下載回本地 Git 儲存庫：

1. **上傳至 Overleaf：**
   - 打開 [Overleaf](https://www.overleaf.com/project) → 點擊 **New Project → Upload Project** → 上傳 [`508-coursework/week-11/dhg508-overleaf-template.zip`](dhg508-overleaf-template.zip)（或將你自己填好的 `main.tex`、`references.bib`、`evidence-table.tex`、`schematic.png` 打包成 `.zip` 上傳）。
2. **將編譯器切換為 `XeLaTeX`（只需設定一次，支援中文與 CJK 字體）：**
   - 點擊左上角 **Menu** 圖標 → 在 **Settings → Compiler** 將預設的 `pdfLaTeX` 改為 **`XeLaTeX`**。
3. **點擊 `Recompile`：**
   - Overleaf 會自動調用 `XeLaTeX` 與 `Biber`，渲染中文（`Noto Serif CJK SC`）、芝加哥腳註、證據表與參考書目。
4. **課前同步回你的 GitHub 儲存庫：**
   - 在 Overleaf 點擊 **Download PDF**，存為你儲存庫中的 `paper/design-paper.pdf`。
   - 如果你在 Overleaf 網頁上修改過文字，請同時點擊 **Menu → Download → Source**，確保儲存庫 `paper/` 目錄裏的 `main.tex`、`references.bib`、`evidence-table.tex` 與最終 PDF 完全一致並提交 Git。

*（可選本地編譯：若你電腦已裝有完整 TeX Live 並包含 `xelatex`、`biber` 與 `biblatex-chicago`，也可直接在本地執行 `cd paper && xelatex main && biber main && xelatex main && xelatex main && cp main.pdf design-paper.pdf`——同一套文件在本地與 Overleaf 完全通用。）*

**如何請 OpenCode 在上傳 Overleaf 前幫你做技術檢查（絕不讓 AI 代寫內容）：**
> 請讀取 `@paper/main.tex`、`@paper/references.bib` 與 `@paper/evidence.csv`。執行 `python3 paper/make_evidence_table.py` 更新 `evidence-table.tex`，檢查 `main.tex` 中每一個 `\autocite` 的 key 是否都在 `references.bib` 中且符合 BibLaTeX Chicago 欄位格式、沒有未轉義的 `%`、`&`、`_` 符號，並將 `main.tex`、`references.bib`、`evidence-table.tex` 與 `schematic.png` 打包成 `paper/overleaf-upload.zip` 供我上傳 Overleaf 用 XeLaTeX 編譯。切勿替我編造任何文獻、頁碼或 Post-mortem 經歷；如有缺失頁碼請直接標出由我自己補齊。

編譯完成後，請務必親自打開 PDF 逐頁檢查：確認中文顯示正常、沒有未解析的粗體引用鍵（如 **`[tobin1986macro]`**）、表格沒有超出頁邊、每一處頁碼均與原書一致。

### 第五步 · 最終儲存庫檢查清單與下週三（11 月 25 日）課堂安排

在 **11 月 25 日（星期三）**上課前，確認你 push 到 GitHub 的儲存庫包含以下完整結構：

```text
<你的專案>/
├── README.md                  # 頂部放公開 https:// 網址 + 一鍵運行與測試指令
├── docs/
│   ├── plan.md                # 封版計劃、範圍與紅線（Non-goals）
│   ├── schematic.png          # 導出的專案視覺示意圖（連同 .html / .excalidraw / .md 源文件）
│   └── user-feedback.md       # 至少 2 位外部朋友的實測紀錄、修改說明與對應測試
├── data/（或 research/）       # 閱讀筆記、research_journal.md、design_doc.md 與 evidence.csv
├── src/ & tests/              # 乾淨的專案源碼 + 可通過的單元／集成／Playwright E2E 測試
└── paper/
    ├── evidence.csv           # （或指向 ../data/ 中的 CSV）
    ├── make_evidence_table.py # 自動生成表格的 Python 腳本
    ├── evidence-table.tex     # 自動生成的 LaTeX 證據表
    ├── references.bib         # 核實無誤的 BibLaTeX 書目（至少 3 項學術文獻 + 一手史料）
    ├── main.tex               # 完整的六節 Overleaf 兼容 LaTeX 論文源碼（biblatex-chicago）
    └── design-paper.pdf       # 從 Overleaf（或本地 XeLaTeX+Biber）編譯下載的最終 PDF
```

**11 月 25 日（最後一堂課）現場安排：**
1. 現場演示你**公開部署的線上版本**完整跑通。
2. 打開編譯好的 **`paper/design-paper.pdf`**（或你的 Overleaf 頁面），展示芝加哥格式腳註、同源生成的證據表與嵌入的示意圖，並分享你在 **Post-mortem 中最重要的一條經驗教訓**（哪裏失敗或跑偏過、你學到了甚麼）。
3. 如有最後未能獨自解決的 Final Bug，當場展示報錯，我們現場一起修好、提交最後一個 Git commit 即可完成期末交付。
4. 若希望在課後幾週參與 Bo 的**高階模型升級計劃**，課堂上或課後直接跟 Bo 登記即可。
