# paygap-analysis-generator

Free Claude skill for HR & People leaders. Generates a gender pay-gap HTML report from any roster (CSV or Excel) — medians, weighted ratios per area, global ratio, with the standard ≥3-per-gender confidentiality rule.

Maintained by **Comp** ([comp.vc](https://comp.vc)).

## What it does

You give it a roster file. It gives you a self-contained HTML report showing:
- Global weighted pay ratio (women's median / men's median, %)
- Per-area breakdown with group-level detail (area × level)
- Confidentiality-protected (groups with <3 per gender are flagged, not computed)
- Methodology and warnings explained inline

Built for HR/People leaders running pay-equity reviews, regulatory reporting prep, or pre-comp-cycle diagnostics.

## Install

### Marketplace (all 4 Comp skills)
```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

This installs the whole `comp-skills` plugin (4 skills, one of which is this one).

### Manual (zip)
Download the `.zip` from our LP, then drop the unzipped folder in your `~/.claude/skills/` directory.

### Excel support
The skill processes CSV out of the box. For `.xlsx` input, install `openpyxl`:
```bash
pip install openpyxl
```

## Required columns

Your file must have at least 5 logical columns. **Column names can vary** — the skill auto-detects common aliases in PT and EN.

| Logical column | Examples that work |
|---|---|
| Name | `name`, `nome`, `colaborador`, `employee` |
| Gender | `gender`, `genero`, `gênero`, `sexo` |
| Salary | `salary`, `salario`, `salário`, `salario_base`, `gross_salary` |
| Level | `level`, `nivel`, `nível`, `senioridade`, `grade` |
| Area | `area`, `área`, `departamento`, `função`, `business_unit` |

If your column names are unusual, Claude will ask which is which.

## Usage

Just talk to Claude. Examples:

- "Roda uma análise de pay gap dessa planilha aqui"
- "Gera o relatório de equidade salarial pra eu mandar pro CHRO"
- "Quero ver o gender pay gap da nossa empresa"
- "Diagnóstico de gap salarial por área"

Output: `paygap-{timestamp}.html` in your current directory. Open in any browser.

## Methodology

- **Medians (not means)** — robust to salary outliers
- **Weighted ratio per area** = Σ(ratio × group_hc) ÷ Σ(group_hc), over valid groups only
- **Global weighted ratio** = weighted average of area ratios by area headcount
- **Confidentiality**: groups (area × level) with fewer than **3 of each gender** are excluded from weighted calculations — shown as "—" in the report, headcounts still visible

## What gets shared with Comp

On first run you'll be prompted for:
1. Your email (optional) — only used to notify you of skill updates.
2. Anonymous telemetry (default: off) — if enabled, sends skill name + timestamp on each run. **Never sends your roster data, salary values, or the report.**

100% local processing. Salary data never leaves your machine. The HTML output is also local — share it with whom you want.

Both opt-ins are stored locally in `~/.comp-skills/config.json`. Edit or delete that file any time to revoke.

## Issues

Open an issue at [cleiton-comp/comp-skills](https://github.com/cleiton-comp/comp-skills/issues) with the `eam` label.

— Powered by Comp · Free skills for HR & People leaders.
