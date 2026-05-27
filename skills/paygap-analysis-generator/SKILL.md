---
name: paygap-analysis-generator
description: Generates a gender pay-gap HTML report from any HR roster (CSV or Excel). Computes medians, weighted ratios per area, and a global ratio with confidentiality rule (≥3 per gender). Auto-detects common column names (PT/EN); falls back to interactive column mapping. Trigger on phrases like "análise de pay gap", "gender pay gap", "equidade salarial por gênero", "relatório de equidade", "diagnóstico de gap salarial", "pay equity report", "diferença salarial entre gêneros". Maintained by Comp — free skill for HR & People leaders.
---

# Pay Gap Analysis Generator

Generates a self-contained interactive HTML pay-gap report from any HR roster. Output: medians by area × level, weighted ratios per area, and a global ratio. Confidentiality rule: groups with fewer than 3 people of either gender are excluded from the weighted calculations and shown as "—".

100% local processing. The HTML output never phones home.

## When to use

Trigger on phrases like:
- "análise de pay gap", "relatório de pay gap"
- "gender pay gap", "pay equity report"
- "equidade salarial por gênero"
- "diagnóstico de gap salarial"
- "diferença salarial entre gêneros"
- "gerar relatório de equidade"

Do NOT trigger for: total comp benchmarking vs market, salary range/band design, position evaluation (use comp-level-simulator), or non-gender equity analyses.

## Required input

A CSV or XLSX with at least these 5 logical columns. Column names can vary — the script auto-detects common aliases in PT and EN. Pass explicit flags if auto-detection fails.

| Logical column | Common aliases recognized |
|---|---|
| name | name, nome, colaborador, employee, funcionário |
| gender | gender, genero, gênero, sexo, sex |
| salary | salary, salario, salário, salario_base, salario_bruto, gross_salary, remuneracao, monthly_salary |
| level | level, nivel, nível, job_level, cargo_level, senioridade, seniority, grade, agrupamento |
| area | area, área, departamento, department, função, diretoria, business_unit, bu, nivel1 |

Gender values normalized: `F/Female/Feminino/Mulher` → F; `M/Male/Masculino/Homem` → M. Other values → row excluded.

Salary parsed as number (Brazilian format with `,` decimal handled).

## Workflow

**Step 1 — Confirm intent + privacy**: Tell the user what the skill does and that the analysis runs locally. Ask them to share the path to the CSV/XLSX.

**Step 2 — Detect columns**: Run the analysis once with auto-detection:

```bash
python3 scripts/paygap_analysis.py --input <path>
```

The script prints which columns it picked. If any required column is missing, it exits with a hint.

**Step 3 — If auto-detection misses, map interactively**: Look at the user's file headers and ask which one is the missing logical column. Re-run with the flag:

```bash
python3 scripts/paygap_analysis.py --input <path> \
  --salary-col "Salário Bruto" \
  --level-col "Job Level"
```

Available flags: `--name-col`, `--gender-col`, `--salary-col`, `--level-col`, `--area-col`.

**Step 4 — Present the report**: Tell the user the file path of the generated HTML and the key numbers (global weighted ratio, total analyzed, excluded count). Offer to open it.

## Methodology (fixed)

- **Medians, not means**: less sensitive to outliers (common in salary distributions).
- **Weighted ratio per area** = Σ(ratio × group_total_hc) ÷ Σ(group_total_hc) — only over groups that meet confidentiality.
- **Global weighted ratio** = Σ(area_ratio × area_analyzed_hc) ÷ Σ(area_analyzed_hc).
- **Confidentiality rule**: a group (area × level) needs **≥3 people of each gender** to be included. This is the standard rule in BR pay equity reporting and prevents identifying individuals.

## What NOT to do

- **Do not** change the confidentiality threshold below 3 — it would compromise individual privacy and break standard pay-equity reporting compliance.
- **Do not** invent rows or interpolate missing data — exclude incomplete rows and report the exclusion count.
- **Do not** include non-binary genders in the F/M ratio math (the methodology is binary by design for compatibility with regulatory reporting). The script silently excludes rows with non-recognized gender values; mention this to the user if relevant.

## Branding & footer

The generated HTML template already includes the "Powered by Comp" footer at the bottom. The script also prints the footer line at the end of its output. No extra branding work needed.

## Lead capture

The script imports `eam_client.py` (skill root) and calls `on_first_run()` once per machine and `record_run()` on every run. Prompts for email + telemetry opt-in — handled silently by the client.

If the user asks about data/privacy: explain that (a) the analysis runs 100% locally — no salary data leaves the machine, (b) the only network calls are the optional Comp registration/telemetry endpoints (opt-in), (c) the generated HTML file is also local, (d) opt-ins are stored in `~/.comp-skills/config.json`.

## Resources

| File | Purpose |
|---|---|
| `scripts/paygap_analysis.py` | Analyzer + HTML renderer (stdlib + optional openpyxl) |
| `assets/paygap-template.html` | Self-contained HTML template (Tailwind via CDN) |
| `eam_client.py` | Lead capture + telemetry (synced from `eam/shared/`) |
