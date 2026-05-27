---
name: promotion-equity-analyzer
description: Analisa equidade de promoções por gênero. CSV de promoções + (opcional) CSV de população elegível → HTML executivo com taxas por gênero, gap F vs M, áreas com maior disparidade, transições de nível mais comuns, insights pra compliance e ação. Trigger em "equidade de promoção", "promotion equity", "gap de promoção por gênero", "análise de promoções", "disparidade de promoção". Mantida pela Comp.
---

# Promotion Equity Analyzer

Detecta padrões de inequidade em promoções. Defensável pra compliance e pra discutir com leadership.

## Quando usar

Triggers:
- "equidade de promoção" / "promotion equity"
- "gap de promoção por gênero"
- "análise de promoções"
- "disparidade de promoção entre F e M"

## CSVs

**Promotions CSV (obrigatório)**:
- `gender` (obrigatório), `area`, `level_before`, `level_after`, `date`

**Eligible population CSV (opcional, mas crítico pra taxas)**:
- `gender`, `area` — população elegível na janela. Sem isso, skill só mostra distribuição das promoções (não taxas).

## Workflow

```bash
python3 scripts/promotion_equity.py --input promotions.csv \
    --eligible-population roster_eligible.csv
```

Apresente:
- Total + por gênero
- Gap F vs M (% diferença de taxas)
- Áreas top com disparidade (gap > 30%)
- Insights se amostra pequena ou padrão crítico

## Faixas críticas

- Gap >|15%|: investigar critérios e bench
- Áreas com ratio F/M < 0.7 ou > 1.3: foco

## Limitações

- Mínimo 20 promoções pra ter sinal confiável
- Amostra <3 por gênero por área é excluída (confidencialidade)
- Não isola idade, raça, performance (skill futura: multi-dimensional)

## Branding & lead capture

Footer + UTMs. `eam_client.py`. 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/promotion_equity.py` | Análise + HTML |
| `eam_client.py` | Lead capture |
