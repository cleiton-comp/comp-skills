# research-digest

Free Claude skill for HR & People leaders. Curates a rolling 12-week digest of high-signal papers and publications on **Org Design**, **Workforce Planning**, and **AI impact on the workforce** — translated to PT-BR with executive summaries and key takeaways. Single HTML output, self-contained, share via Drive/email/static hosting.

Maintained by **Comp** ([comp.vc](https://comp.vc?utm_source=github&utm_medium=readme&utm_campaign=eam&utm_content=skill-research-digest)).

## What it does

Each time you run it:
1. Pulls the latest 12 weeks of papers/reports from academic (OpenAlex, arXiv) and practice (consultancy + thought leader) sources
2. Translates titles, abstracts, and key takeaways to PT-BR
3. Renders an executive HTML digest grouped by theme

Built for HR/People leaders who want to stay on the frontier without drowning in literature.

## Install

### Marketplace (all 4 Comp skills)
```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

This installs the whole `comp-skills` plugin (4 skills, one of which is this one).

### Manual (zip)
Download the `.zip` from our LP, then drop the unzipped folder in your `~/.claude/skills/` directory.

## Usage

Just talk to Claude. Examples:

- "Gera meu radar de papers dessa janela"
- "Quero ver as novidades em org design das últimas semanas"
- "Atualização de pesquisa sobre IA no trabalho"
- "Research review pra eu mandar pro CEO"

Claude orchestrates the 3 steps (fetch → translate → render) and gives you a `research-digest-YYYY-MM-DD.html` in your current directory.

## Scheduling (power users)

The skill is on-demand by default. To run it on a cadence, schedule it via:

**Claude Code** (if you use it):
```
/schedule weekly "rode meu research-digest"
```

**Unix cron** (manual):
```cron
0 9 * * MON cd ~/projects/my-research && claude "rode o research-digest"
```

Cadence sweet spot: **monthly** (matches the rolling 12-week window — fresh material guaranteed).

## What gets shared with Comp

On first run you'll be prompted for:
1. Your email (optional) — only used to notify you of skill updates.
2. Anonymous telemetry (default: off) — if enabled, sends skill name + timestamp on each run. **Never sends the digest content, sources, or your query inputs.**

The HTML output stays 100% on your machine. The skill fetches from public research APIs (OpenAlex, arXiv) — no credentials, no tracking.

Both opt-ins are stored locally in `~/.comp-skills/config.json`. Edit or delete that file any time to revoke.

## Source coverage

- **Academic**: OpenAlex, arXiv (works through OpenAlex)
- **Practice**: top consultancies (McKinsey, BCG, Bain, Deloitte, Mercer, WTW, Korn Ferry) + thought leaders (Josh Bersin, Galloway, etc.) via RSS

Full catalog: `references/sources.md`.

## Issues

Open an issue at [cleiton-comp/comp-skills](https://github.com/cleiton-comp/comp-skills/issues) with the `eam` label.

— Powered by Comp · Free skills for HR & People leaders.
