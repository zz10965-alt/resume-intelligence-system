# Resume Intelligence System · 简历智能系统

A resume intelligence system built with **[Claude Code](https://claude.ai/code)** — a human-in-the-loop system that turns raw evidence into targeted, bilingual, fact-checkable résumés (DOCX + PDF) plus a public portfolio site.

> This repo shows the **methodology and automation** (rules + Claude Code skills). The actual personal résumé data is kept private — see [What's public vs private](#whats-public-vs-private).

## Why

Applying to DA/BA/DS roles across **both China and the US** means one set of real experiences mapped onto many target positions, two languages, two formats — under a hard rule that **no fact may be fabricated**. Hand-editing résumés across all of that is slow and error-prone. This system makes it repeatable and traceable.

## Pipeline

```
RAW EVIDENCE → INGEST → EXPERIENCE BANK (source of truth) → MASTER RESUME
→ MARKET PROFILES → BASE VARIANTS → TARGET JD ANALYSIS → JD↔EVIDENCE MATCH
→ TARGETED GENERATION → FACT / ATS / FORMAT VALIDATION → DOCX + PDF + MATCH REPORT
```

## Human × AI division

| | Human (me) | AI (Claude Code) |
|---|---|---|
| **Role** | Sole source of truth; owns the "no fabrication" rule; reviews every output; makes final decisions | Executes: reads files → writes code → runs → verifies |
| **Examples** | Supplied all real facts; caught and corrected AI mistakes | OOXML hyperlink injection; DOCX→PDF via Word COM; Chart.js + i18n for the site; structured bilingual copy |
| **Authority** | Final veto on any fact | None — AI never invents a fact |

## Core challenges & solutions

1. **AI hallucination vs. truth** — AI tends to fill gaps with plausible but fake facts. Solution: a `source-of-truth` architecture with evidence statuses (`VERIFIED / SAFE_INTERPRETATION / UNVERIFIED / CONFLICT / DO_NOT_CLAIM`); the AI only reorganizes and restyles, never creates facts. The AI did once misclassify real contact info as "template residue" — I caught and reverted it. That's exactly why the human review loop is non-negotiable.
2. **Word/WPS flattens hyperlinks on re-save** — links turn into dead blue text. Solution: inject links at the OOXML level (`w:hyperlink` + relationship) via python-docx, and export PDF through MS Word COM to preserve them.
3. **Bilingual consistency** — one toggle, no lost info, contact info split by market. Solution: content lives in `data.js` as `{ en, zh }` with a runtime language switch.

## What's public vs private

**Public (this repo):**
- `rules/` — the constraint system: fact integrity, cross-variant consistency, ATS safety, role classification, writing & format rules
- `.claude/skills/` — 7 Claude Code skills (the automation): `ingest-evidence`, `analyze-jd`, `analyze-market`, `generate-resume`, `validate-resume`, `compare-resume`, `export-resume`
- `resume/templates/` — a clean, reusable résumé template
- `CLAUDE.md` — the operation manual

**Private (not published):**
- `source/` (raw evidence, experience bank, evidence registry), `resume/master`, `resume/base_variants`, `jd/`, `output/` — all real personal data.

## Live result

A companion portfolio built in the same workflow is live at **[zz10965-alt.github.io](https://zz10965-alt.github.io/)** — bilingual, with experience, projects, charts, and publications.
