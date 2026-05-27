---
name: comp-ratio-analyzer
description: Analisa compa-ratio (salário ÷ mediana da banda) de roster contra tabela salarial. Identifica clusters under/below/at/above/over, top 10 outliers por direção, custo mensal+anual pra equalizar abaixo da mediana, breakdown por nível. Output HTML executivo. Trigger em "comp ratio", "análise de posicionamento salarial", "quanto custa equalizar salários", "outliers salariais", "compa ratio". Mantida pela Comp.
---

# Comp Ratio Analyzer

CSV de roster + CSV de bandas salariais → HTML com distribuição compa-ratio, outliers, custo pra equalizar.

## Quando usar

Ativa em frases como:
- "comp ratio" / "compa ratio"
- "análise de posicionamento salarial"
- "quanto custa equalizar"
- "outliers salariais"
- "quem está abaixo/acima da banda"

## Workflow

**Step 1**: Pegue 2 CSVs:
- Roster: colunas `name`, `salary`, `level`, (opcional `area`)
- Bands: colunas `level`, `mid` (mediana). Min/max opcional.

**Step 2**:
```bash
python3 scripts/comp_ratio.py --roster roster.csv --bands bands.csv
```

**Step 3**: Apresente:
- Custo mensal pra equalizar (líder com esse número)
- Distribuição (under/below/at/above/over)
- Top outliers (under = risco; over = legacy/exceções)

## Faixas de classificação

| Faixa | Compa ratio | Interpretação |
|---|---|---|
| under | <80% | Crítico — revisão urgente |
| below | 80-95% | Abaixo do target |
| at | 95-105% | No target |
| above | 105-120% | Acima do target (ok) |
| over | >120% | Crítico — provável legacy/exceção |

## Branding

Footer + UTMs no template HTML.

## Lead capture

`eam_client.py`. Privacidade: 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/comp_ratio.py` | Análise + HTML |
| `eam_client.py` | Lead capture |
