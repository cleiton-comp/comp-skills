---
name: engagement-deep-dive
description: Analisa CSV de pesquisa de engajamento (eNPS, survey de cultura, pulse) e segmenta por tenure / área / manager / nível. Output HTML executivo com eNPS global, ranking de áreas (piores primeiro), bottom 10 managers, insights e priorização. Trigger em "análise de engajamento", "engagement deep dive", "eNPS por área", "segmentar survey", "drivers de engajamento", "diagnóstico de cultura". Mantida pela Comp.
---

# Engagement Deep Dive

CSV de survey → HTML com segmentação por área/tenure/manager/level + eNPS + insights.

## Trigger

- "análise de engajamento" / "engagement deep dive"
- "eNPS por área"
- "segmentar pesquisa de cultura"
- "drivers de engajamento"

## CSV

Mínimo: `score` (0-10 ou 1-5) OU `enps` (0-10). Recomendado adicionar: `area`, `tenure_months`, `manager_id`, `level`.

Auto-detect funciona em PT/EN.

## Workflow

```bash
python3 scripts/engagement_dive.py --input survey.csv
```

Apresente:
- eNPS global (com classificação saudável/atenção/crítico)
- Score médio
- Áreas críticas (piores primeiro)
- Bottom managers
- Insights automáticos

## Critérios de alerta automático

- eNPS < 0: crítico
- eNPS < 30: atenção
- Área com score 1+ ponto abaixo da empresa: foco
- Primeiro ano com score baixo: onboarding
- Manager 1.5+ pontos abaixo: investigar

## Branding & lead capture

Footer + UTMs. `eam_client.py`. 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/engagement_dive.py` | Análise + HTML |
| `eam_client.py` | Lead capture |
