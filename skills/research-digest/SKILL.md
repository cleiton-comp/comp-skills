---
name: research-digest
description: Curates a rolling 12-week digest of high-signal papers, working papers, and publications on Org Design, Workforce Planning, and AI impact on the workforce. Sources include academic (OpenAlex, arXiv) and practice (top consultancies, thought leaders). Produces a translated PT-BR executive HTML report with abstracts, key takeaways, and source metadata. Trigger on phrases like "digest de pesquisa", "radar de papers", "novidades em org design", "research review RH", "panorama academico de workforce planning", "atualizacao de pesquisa sobre IA no trabalho", "leituras sobre future of work". Maintained by Comp — free skill for HR & People leaders.
---

# Research Digest

Builds a rolling 12-week digest covering Org Design, Workforce Planning, and AI & the Workforce. Combines academic sources (OpenAlex, arXiv, SSRN via OpenAlex) and practice sources (consultancy reports, thought leader blogs), translates titles + abstracts + key takeaways to PT-BR, and delivers a single self-contained HTML report.

The skill runs **on-demand**: each time you invoke it, it fetches the latest 12-week window. For weekly/monthly cadence, schedule the skill via your shell cron (instructions in `README.md`).

## When to use

Trigger on phrases like:
- "digest de pesquisa", "radar de papers"
- "atualizacao de research", "panorama academico"
- "novidades em org design", "novidades em workforce planning"
- "impacto da IA na forca de trabalho", "future of work"
- "research review", "research digest"
- "leituras sobre [Org Design / Workforce / AI workforce]"

Do NOT trigger for: original research (this skill curates, does not analyze); proprietary insight generation; one-off paper lookup (use a search tool); or ad-hoc topic explainers.

## Workflow

The skill has 3 steps. You (the agent) orchestrate them; the user only invokes the trigger.

### Step 1 — Fetch (script)

```bash
python3 scripts/fetch_research.py --weeks 12 --output ./research-raw.json
```

Output: JSON with deduplicated items (DOI > URL > normalized title hash). Each item has: `id`, `source`, `source_type` (academic/consultancy/thoughtleader/media), `title`, `authors`, `published_date`, `url`, `abstract`, `doi`, `topics`, `keywords`, `paywall`.

Sources catalog: `references/sources.md`. Search strings: `references/queries.md`.

### Step 2 — Translate (you, the agent)

Read `./research-raw.json` and produce `./research-translated.json` with the same items plus 4 new fields per item:

- `title_pt` — translated title
- `abstract_pt` — full abstract translation (or a 4–6 sentence summary if no abstract)
- `relevance_pt` — 2–3 sentences connecting the paper to a concrete HR/Comp problem (e.g., "implicações para career architecture", "leitura para decisões de paymix em IA")
- `key_takeaways_pt` — 3–5 short bullets with practical findings

Also produce a top-level `exec_summary_pt` field — 3 bullets: total items, dominant topic, must-read of the window.

Use clean PT-BR. Keep English terms that have no consecrated PT translation (workforce planning, span of control, talent density). NEVER invent content — if no abstract is available, mark `abstract_pt` as `"(Abstract não disponível — recomendado abrir a fonte)"`.

### Step 3 — Generate HTML (script)

```bash
python3 scripts/generate_digest.py \
  --input ./research-translated.json \
  --output ./research-digest-$(date +%Y-%m-%d).html
```

Single-file HTML (Tailwind via CDN). 3 zones:
1. Executive summary (top 5 reads + emerging themes)
2. Cards grouped by theme (Org Design / Workforce Planning / AI & Workforce)
3. Appendix with full list, filterable by source/type

## Guidance

- **Always translate to PT-BR**, regardless of source language (English, French, Spanish papers all get translated).
- **Mark paywall content explicitly** — set `paywall: true` in the JSON, the template renders a badge.
- **Prefer working papers and preprints** to books — the digest is about the frontier, not the canon.
- **If a topic comes empty**, say "Sem publicações relevantes na janela" — don't backfill with old material.
- **Exclude pure marketing** from consultancies; include reports with primary data, surveys with disclosed N, or frameworks with explicit methodology.

## Branding & footer

The HTML template already includes the "Powered by Comp" footer (rendered at the bottom of the digest). The `generate_digest.py` script prints the footer line at the end of its output. No extra branding work needed.

## Lead capture

Both scripts (`fetch_research.py` and `generate_digest.py`) call `on_first_run()` at startup and `record_run()` at the end. Email + telemetry opt-in prompted only once per machine.

If the user asks about data/privacy: explain that (a) all output stays on their machine (HTML file in cwd), (b) the only network calls are to public research APIs (OpenAlex, arXiv) + the optional Comp registration endpoint, (c) opt-in flags are stored in `~/.comp-skills/config.json`.

## Resources

| File | Purpose |
|---|---|
| `scripts/fetch_research.py` | Multi-source fetcher with dedup |
| `scripts/generate_digest.py` | Renders HTML from translated JSON |
| `assets/template.html` | Self-contained HTML template (Tailwind) |
| `eam_client.py` | Lead capture + telemetry (synced from `eam/shared/`) |
| `references/sources.md` | Catalog of sources covered, rationale, limits |
| `references/queries.md` | Search strings + topic categories |
