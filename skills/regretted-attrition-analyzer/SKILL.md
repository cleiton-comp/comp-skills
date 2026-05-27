---
name: regretted-attrition-analyzer
description: Analisa CSV de desligamentos e identifica padrões em regretted vs unregretted — top correlated factors (área, gestor, tenure, performance, nível), motivos declarados, insights pra ação. Output HTML executivo defensável pra CHRO levar pro CEO. Trigger em "análise de regretted attrition", "padrões de turnover", "por que estamos perdendo gente", "investigar desligamentos", "regretted vs unregretted", "diagnóstico de turnover". Mantida pela Comp.
---

# Regretted Attrition Analyzer

Lê CSV de desligamentos e devolve análise estruturada: % regretted vs unregretted, padrões por área/gestor/tenure/performance, motivos declarados, insights pra ação. Output HTML pronto pra apresentar pra leadership.

## Quando usar

Ativa em frases como:
- "análise de regretted attrition"
- "padrões de turnover"
- "por que estamos perdendo gente"
- "investigar desligamentos"
- "regretted vs unregretted"
- "diagnóstico de turnover"

NÃO ativa para: cálculo de custo de turnover (usar `custo-turnover-calculator`); análise por colaborador individual; cálculo de rescisão (usar `custo-demissao-calculator`).

## Schema CSV

Obrigatórias:
- `regretted` (1/0, sim/não, yes/no, true/false)

Recomendadas (cada uma destrava um corte de análise):
- `area`, `level`, `tenure_months`, `performance_rating` (1-5), `manager_id`, `departure_reason`, `departure_date`

Auto-detect funciona em PT/EN.

## Workflow

**Step 1**: Pergunte path do CSV.
**Step 2**: Rode `python3 scripts/regretted_attrition.py --input departures.csv`. Auto-detect das colunas.
**Step 3**: Apresente:
- Top number: % regretted total
- Insights destacados (gestor com pattern, área hot, top performers saindo, etc.)
- Sugira ação por insight

## Output do skill

- Stats top: total, regretted, unregretted, %
- Insights automáticos (gestor com 3+ regretted, área >1.5x média, short-tenure regretted >30%, top performers saindo)
- Tabelas: por área, tenure band, performance band, top 10 gestores
- Top motivos declarados (se coluna disponível)

## Limitações

- Análise descritiva (identifica padrões), não causal (não diz POR QUE acontece)
- Quanto mais colunas, mais segmentação possível
- Recomenda mínimo 20 desligamentos para padrões serem confiáveis

## Branding & footer

Template HTML com footer Powered by Comp + UTMs.

## Lead capture

`eam_client.py` chamado em `on_first_run()` + `record_run()`. Privacidade: 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/regretted_attrition.py` | Análise + HTML render |
| `eam_client.py` | Lead capture + telemetria |
