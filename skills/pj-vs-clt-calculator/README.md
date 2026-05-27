# pj-vs-clt-calculator

Free Claude skill for Brazilian HR & People leaders. Calculates CLT ↔ PJ salary equivalence with full tax accuracy (INSS, IRPF, FGTS, 13th, vacation, benefits, PJ costs). Use it to compare an individual offer or batch-process a CSV of multiple candidates.

Maintained by **Comp** ([comp.vc](https://comp.vc)).

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

Just talk to Claude. Example prompts:

- "Quanto preciso faturar como PJ pra equivaler a um salário CLT de R$ 10.000?"
- "Qual o salário CLT equivalente a R$ 15.000 PJ com alíquota de 6%?"
- "Tenho uma planilha com 20 candidatos PJ — me ajuda a calcular o CLT equivalente de todos."

For batch mode, your CSV needs at minimum:
- `pj_billing` (R$/month)
- `pj_aliquota` (% — e.g., 6)

Optional columns: `candidate_name`, `pj_invoices` (12/13), `pj_accounting`, `clt_vavr_desired`, `clt_bonus_desired`, `include_fgts` (1/0).

## What gets shared with Comp

On first run you'll be prompted for:
1. Your email (optional) — only used to notify you of skill updates.
2. Anonymous telemetry (default: off) — if enabled, sends skill name + timestamp on each run. **Never sends your inputs or outputs.**

Both are stored locally in `~/.comp-skills/config.json`. Edit or delete that file any time to revoke.

## Tax tables

Embedded tables are 2024/2025 Receita Federal. We ship a new version yearly in February when the tables update.

## Issues

Open an issue at [cleiton-comp/comp-skills](https://github.com/cleiton-comp/comp-skills/issues) with the `eam` label.

— Powered by Comp · Free skills for HR & People leaders.
