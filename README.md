# truedano_skills

[繁體中文](#繁體中文) | [English](#english)

---

## 繁體中文

### 專案簡介

`truedano_skills` 是一個專為現代 AI Agent（包括 Claude Code、Google Antigravity、Cursor 及其他相容 Agent 規範的系統）所建置的自訂技能模組庫 (Custom Agent Skills Repository)。

本倉庫旨在將重複性高、複雜度高或領域特化（如教育、工程、自動化）的工作流程標準化為可執行的 Agent Skill，讓 AI 在執行特定任務時具備嚴謹的指引、架構規範與萃取驗證機制。

---

### 目錄結構

```text
truedano_skills/
├── README.md
└── skills/
    └── lesson-prep-converter/           # 教案多格式批次結構化轉換技能
        ├── SKILL.md                     # 技能核心提示詞與執行流程定義
        └── references/
            ├── extraction_guide.md      # 各類文檔格式的技術萃取指引
            └── lesson_schema.md         # 標準化教案結構規範 (YAML Frontmatter + Markdown)
```

---

### 已收錄技能 (Available Skills)

#### 1. `lesson-prep-converter` — 教案多格式批次結構化轉換

將指定目錄內多種格式的雜亂教學素材（書籍掃描圖檔、PDF、Word/docx、PPT/pptx、Excel/csv、TXT 等），自動萃取、清洗並結構化轉換為最適合 AI 理解與下游轉換的標準 Markdown 教案知識庫。

- **觸發情境**：
  - 「整理教案」、「教案轉格式」、「批次整理教學檔案」
  - 「將目錄內的教材轉成 AI 格式」、「建立教案知識庫」
- **核心轉換管線 (Pipeline)**：
  1. **目錄掃描與清單建立 (Catalog & Inventory)**：盤點目錄中各類型教材，分類為純文字/表格、辦公文檔、PDF、圖檔掃描，並在不污染原始檔案前提下設定輸出目錄 `_lesson_knowledge_base/`。
  2. **多格式內容萃取 (Multi-Format Extraction)**：依格式特性提取正文、表格、投影片備忘稿 (Notes)、結構階層與圖片附件。
  3. **語意結構化與補全 (Structured Synthesis)**：遵循 Bloom's Taxonomy 補齊教學目標、課堂節奏時間配置、動機提問與評量題目，輸出統一規範的 YAML Frontmatter。
  4. **標準化輸出與驗證 (Delivery)**：生成 `index.md` 課程地圖、`[單元編號]_[主題名稱].md`、內嵌圖檔庫 `images/` 以及轉換日誌 `conversion_log.md`。
  5. **下游應用串接 (Downstream Guidance)**：產出之 Markdown 可直接無縫對接 Marp (產生簡報)、Pandoc (輸出機構公版 Word/講義) 或 VitePress/Docusaurus (部署靜態教材站)。

---

### 使用方式 (Usage)

本倉庫的 Skills 遵循標準 Agent Skill 規範（以包含 YAML Frontmatter 的 `SKILL.md` 為核心）。您可透過以下方式使用：

1. **直接作為任務提示詞 (Direct Reference)**：在任何支援長文本與自訂指令的 AI 工具中，直接引用或載入對應技能的 `SKILL.md` 作為執行規範。
2. **掛載至支援 Agent Skills 的系統**：若您使用的 Coding Agent 支援外掛自訂技能，直接將 `skills/<skill-name>/` 目錄加入您的 Agent 技能路徑即可。

---

### 擴充新技能規範 (Contribution & Extension)

新增 Skill 請遵循以下規範：
1. **單一職責**：每個 Skill 資料夾置於 `skills/<skill-name>/` 下，具備獨立的 `SKILL.md`。
2. **元數據聲明**：`SKILL.md` 頂部必須具備 YAML Frontmatter，明確標註 `name` 與具體觸發時機的 `description`。
3. **漸進式揭露 (Progressive Disclosure)**：核心流程與高頻原則寫在 `SKILL.md`，深度規格、Schema 或技術細節拆分至 `references/` 資料夾內引用，避免一次佔用過多 Context Window。

---

### 授權條款 (License)

本專案採 [MIT License](LICENSE) 授權。

---

## English

### Overview

`truedano_skills` is a repository of custom agent skill modules designed for modern AI Coding Agents and Agentic Workflows (including Claude Code, Google Antigravity, Cursor, and other platforms supporting structured agent skill definitions).

The project packages complex, repetitive, and domain-specific tasks into production-ready skills with strict execution pipelines, schema constraints, and verification steps.

---

### Directory Layout

```text
truedano_skills/
├── README.md
└── skills/
    └── lesson-prep-converter/           # Multi-format batch lesson prep converter
        ├── SKILL.md                     # Skill workflow definition & core prompt
        └── references/
            ├── extraction_guide.md      # Technical extraction guidelines per format
            └── lesson_schema.md         # Schema specification (YAML Frontmatter + Markdown)
```

---

### Available Skills

#### 1. `lesson-prep-converter` — Multi-Format Batch Lesson Preparation Converter

Scans and ingests heterogeneous teaching materials (scanned book images, PDFs, Word/docx, PowerPoint/pptx, Excel/csv, plain text) from a designated folder, cleanly extracts and refactors them into standardized Markdown lesson plans with rich YAML frontmatter.

- **Trigger Keywords**:
  - "Organize lesson plans", "Convert course materials", "Batch convert curriculum files"
  - "Transform folder contents into AI knowledge base"
- **Pipeline Stages**:
  1. **Catalog & Inventory**: Discovers and categorizes files (text/data, office docs, PDFs, visual scans) and prepares an isolated output workspace at `_lesson_knowledge_base/` without mutating original source assets.
  2. **Multi-Format Extraction**: Extracts headings, body content, tables, speaker notes, and embedded illustrations tailored to each format's characteristics.
  3. **Structured Synthesis**: Applies Bloom's Taxonomy to enrich missing instructional objectives, pacing allocations (minute markers), warm-up hooks, and assessments. Emits standardized YAML frontmatter.
  4. **Delivery & Validation**: Outputs `index.md` (curriculum map), per-topic lesson units (`[Unit]_[Title].md`), an extracted `images/` folder, and an audit trail in `conversion_log.md`.
  5. **Downstream Integration**: The resulting Markdown serves as a single source of truth, easily consumed by Marp (slides), Pandoc (formatted Word handouts), or VitePress/Docusaurus (online documentation portals).

---

### Usage

The skills in this repository follow the standard Agent Skill specification (centered around `SKILL.md` with YAML frontmatter). You can use them via:

1. **Direct Reference**: Provide or load the target `SKILL.md` file as instructions/prompt in any LLM or AI coding tool.
2. **Coding Agent Integration**: If your coding agent supports custom skills directories, add or link `skills/<skill-name>/` directly into your agent's configured skills path.

---

### Extension Guidelines

When adding new skills:
1. **Single Responsibility**: Place each skill under `skills/<skill-name>/` with an independent `SKILL.md`.
2. **Metadata Header**: Include YAML Frontmatter with accurate `name` and trigger-focused `description`.
3. **Progressive Disclosure**: Keep `SKILL.md` lean and actionable; move detailed specs, schemas, and API tables to `references/` to optimize context window efficiency.

---

### License

This project is licensed under the [MIT License](LICENSE).
