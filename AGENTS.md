# Agent Instructions

This is the DAIHUM workspace template source of truth.

## Core Rules

- Do not write project-specific research content into
  `templates/project_template/`.
- To start a new project, copy `templates/project_template/` into this
  repository's `projects/` folder, as `projects/<project_name>/`.
- In this course repository, `projects/` is the working project location.
- If the target project is unclear, ask before writing files.
- Keep original source materials in `sources/raw/`; do not edit them in place.
- Put cleaned, OCRed, indexed, or otherwise transformed materials in
  `sources/processed/`.
- Put large generated outputs, OCR page JSON dumps, indexes, caches, and live
  databases in `artifacts/`; do not commit them unless the human explicitly
  asks.
- Put research planning, notes, drafts, outputs, and references in `research/`.
- Put project-specific scripts, notebooks, apps, or libraries in `code/` only
  when the project actually needs them.

## Project Naming

Use lowercase names with underscores:

```bash
cp -R templates/project_template projects/my_first_project
```

## Default Project Layout

```text
<target_workspace>/<project_name>/
├── research/
├── sources/
├── artifacts/
└── code/
```
