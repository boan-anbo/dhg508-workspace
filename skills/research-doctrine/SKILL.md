---
name: research-doctrine
description: How we run a research project in a DAIHUM workspace — the cross-project operating doctrine. Use when starting or working a research project (in research/sources/artifacts/code), acquiring sources, deciding where files go, moving from sources → notes → draft, or deciding whether to fix a tool vs. escalate. Tool-agnostic and secret-free: safe to distribute.
---

# Research doctrine

The single cross-project rulebook for working a research project in a DAIHUM
workspace. It is **tool-agnostic** (it never names or embeds a specific product,
account, or key) and **secret-free**, so it is safe to distribute with the
workspace template. Product-specific operational detail lives in the operator's
own private layer, never here.

## 1. The workspace is the unit of work

Every project is one directory with a fixed shape:

```
<project>/
├── research/   design/ · journal/ · notes/ · drafts/ · outputs/ · references/
├── sources/    raw/ (never edit in place) · processed/ (OCR/clean/index)
├── artifacts/  large generated output / indexes / caches / DBs (git-ignored)
└── code/       project-specific scripts/notebooks (only when needed)
```

- **`sources/raw/`** is sacred — original materials, never edited in place.
  Cleaned / OCR'd / transcribed / indexed material goes to `sources/processed/`.
- **`research/`** is the intellectual record: `design/` (plan), `journal/`
  (dated decisions + progress — write here continuously), `notes/`, `drafts/`,
  `outputs/` (reports/figures/exports), `references/` (citations/bibliography).
- **`artifacts/`** holds heavy generated stuff (page-JSON, embeddings, live DBs).
  Git-ignored; record in a manifest *what it is and how to rebuild it*.

## 2. The research loop

```
design → acquire sources → process → read+note → draft → outputs
              ↑                                              │
              └──────────── journal every decision ─────────┘
```

Start in `research/design/design_doc.md` (question, scope, what counts as a
source). Log decisions in `research/journal/` as you go — the journal is the
memory across sessions and the place to record *why*, not just *what*.

## 3. Acquiring sources — legit-first cascade

Acquiring a source follows the **access cascade**. Try in order; never default to
the last rung:

1. **Open access** — OA / Unpaywall / repository copies.
2. **Entitled / institutional** — your own credentials via library proxy
   (CrossAsia / SBB / EZproxy …).
3. **Preservation libraries** — HathiTrust / Internet Archive controlled lending.
4. **Gray sources** — last resort only, and only with your *own* credentials.

The detailed how-to lives in the published, secret-free skill set
`@daihum/scholar-sources/skills` — `source-access-doctrine`, `find-a-paper`,
`get-a-paywalled-paper`, `download-a-book`, `configure-*-key`. Load those for the
step-by-step; this doctrine just fixes the *order* and the principle:
**legit-first, never default gray, only ever the user's own credentials.**

> Operationally you'll **download and translate** sources with your research CLI.
> The concrete CLI commands are product-specific and live in your private operator
> layer — they are intentionally NOT in this distributable doctrine.

## 4. Dogfooding & escalation — don't hack around the tool

Research is the **honest dogfood**: we use the *published* tools as a real user
would (consume released versions; version bumps are deliberate). So when a tool
falls short:

- **Do NOT** patch around it inside the research repo or fork the tool here.
- **DO** record the friction in `research/journal/` (what you wanted, what failed),
  then **escalate it to the tribe that owns the tool** as a real requirement.
- Continue the research with the best available fallback; re-consume the tool once
  it ships the fix.

This keeps the research repo clean (research, not tool-dev) and turns real
research friction into the platform's requirements stream.

## 5. Coordination

Cross-tribe / cross-squad coordination and worktree isolation follow the
`hacksquad-teamwork` skill (escalations, supervisions, issues-as-SSOT). Use it
when routing a tool gap to another tribe or coordinating parallel work — don't
reinvent the protocol here.

## 6. What stays out of this skill (distribution boundary)

To keep this safe to distribute: **no product names, no account/host/key values,
no private internals.** Anything product-specific (the exact research-CLI
invocations, private endpoints, credentials) belongs in the operator's own
private skill layer, loaded alongside this one but never bundled with the
distributable workspace template.
