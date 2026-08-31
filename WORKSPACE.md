# DAIHUM Workspace

Minimal source-of-truth template for DAIHUM research workspaces.

This repository stores reusable project structure and shared working rules. By
default, it does not store project-specific research in the template repo
itself.

## Structure

```text
daihum_workspace/
├── AGENTS.md
├── README.md
├── LICENSE
├── projects/
│   └── README.md
└── templates/
    └── project_template/
```

## Start a Project In A Target Workspace

Copy the canonical template into this repository's `projects/` folder:

```bash
cp -R templates/project_template projects/chinese_ai_history
```

Use lowercase names with underscores.

After copying, all research work for that project belongs inside the copied
project directory. Do not put active research content in
`templates/project_template/`.

## Project Layout

Each project follows this structure:

```text
projects/<project_name>/
├── README.md
├── research/
│   ├── design/design_doc.md
│   ├── journal/research_journal.md
│   ├── notes/
│   ├── drafts/
│   ├── outputs/
│   └── references/
├── sources/
│   ├── raw/
│   └── processed/
├── artifacts/
│   └── README.md
└── code/
    └── README.md
```

## Rules

- `templates/project_template/` is a clean reusable template.
- Do not put project-specific research content in the template.
- Actual projects live in copied project directories, usually outside this
  template repo unless explicitly using this repo as the working workspace.
- Original source materials go in `sources/raw/` and should not be edited in
  place.
- Cleaned, OCRed, indexed, or transformed source material goes in
  `sources/processed/`.
- Large generated outputs, OCR page JSON dumps, indexes, caches, and live
  databases go in `artifacts/`, which is ignored by git except for its README.
- Research plans, notes, drafts, outputs, and references go in `research/`.
- Project-specific scripts, notebooks, apps, or libraries go in `code/` when
  needed.

## Large Files and Databases

Git should hold the project structure, notes, source manifests, curated text
exports, scripts, and small durable research files.

Avoid committing live databases, large generated JSON, caches, embeddings, or
bulk OCR artifacts. Put them under `projects/<project_name>/artifacts/` and
record what they are, where they came from, and how to rebuild them.

PDFs and assets are a project decision: commit small essential files when they
are truly part of the research record; keep large batches or restricted
materials outside git and track them with a manifest in `research/` or
`sources/`.
