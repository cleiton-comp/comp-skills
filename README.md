# Comp Skills

Free Claude skills for HR & People leaders, built and maintained by [Comp](https://comp.vc).

## What's here

| Skill | What it does |
|---|---|
| [pj-vs-clt-calculator](skills/pj-vs-clt-calculator/) | Brazilian CLT ↔ PJ salary equivalence with full tax accuracy (INSS, IRPF, FGTS, 13th, vacation, benefits). Single or batch CSV. |
| [comp-level-simulator](skills/comp-level-simulator/) | Self-contained interactive HTML simulator for evaluating job levels using a 4-pillar methodology. |
| [paygap-analysis-generator](skills/paygap-analysis-generator/) | Gender pay-gap HTML report from any HR roster (CSV/XLSX). Confidentiality-protected (≥3 per gender). |
| [research-digest](skills/research-digest/) | Rolling 12-week digest of papers on Org Design, Workforce Planning, and AI impact on the workforce — translated to PT-BR. |

## Install

### Recommended: marketplace install (all 4 skills at once)

```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

This installs all 4 skills. They're model-invoked — just describe what you want and Claude picks the right one (e.g., "analyze pay gap" → `paygap-analysis-generator`).

After install, run `/reload-plugins` to activate.

### Single skill via .zip (LP download)

If you want only one skill, download its `.zip` from our landing page at [tools.comp.vc](https://tools.comp.vc) (it captures your email so we can notify you of updates) and drop the unzipped folder in your `~/.claude/skills/` directory. Skills installed this way run standalone (no namespace).

## Privacy

These skills run **locally** in your Claude. Salary data, rosters, and any analysis stay on your machine — none of it phones home.

On first run, each skill asks once whether you want:
1. **Updates by email** (optional) — only to notify you of skill improvements.
2. **Anonymous usage telemetry** (default: **off**) — if enabled, sends only the skill name + timestamp per run. Never your inputs, outputs, or roster data.

Both opt-ins are stored in `~/.comp-skills/config.json`. Delete that file any time to revoke.

## Issues & feedback

Open an [issue](https://github.com/cleiton-comp/comp-skills/issues) — we read all of them.

## License

[MIT](LICENSE) — free to use, fork, redistribute. Attribution appreciated.

## About Comp

Comp is an AI-native HR service for fast-growing companies. We embed HR executives and AI engineers in our customer teams. These skills are a small slice of what we build internally — released free because better HR tooling is good for everyone.

[comp.vc](https://comp.vc)
