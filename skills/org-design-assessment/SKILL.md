---
name: org-design-assessment
description: Assessment HTML interativo de maturidade em design organizacional, baseado no framework Comp (artigo Cajuína "Você confia milhões à intuição?"). 4 pilares × 3 perguntas — Maturidade de Governança (CLT/PJ), Span of Control, Pirâmide de Níveis, Disparidade Salarial Interna. Output: Score 0-100 por pilar e geral, classificação (Reativo → Estratégico) e próximo passo personalizado por pilar. ~5 minutos. Trigger em "maturidade de org design", "diagnóstico organizacional", "score de remuneração", "data-driven org design", "avaliar estrutura org". Mantida pela Comp.
---

# Org Design Maturity Assessment

Gera um HTML interativo que avalia maturidade de design organizacional em 4 pilares — Governança, Span of Control, Pirâmide de Níveis, Disparidade Salarial. Output: Score 0-100 + classificação + próximos passos.

Baseado no [artigo Cajuína "Você confia milhões à intuição?"](https://cajuina.org/principais/coluna-comp/design-organizacional/).

## Quando usar

Ativa em frases como:
- "maturidade de org design"
- "diagnóstico organizacional"
- "score de remuneração" / "score de design org"
- "data-driven org design"
- "avaliar estrutura org"
- "como meu RH está em design organizacional"

NÃO ativa para: análise de span específica (usar `span-of-control-diagnostic`); maturidade de DADOS de RH (usar `hr-data-maturity-assessment`); maturidade em IA (usar `ai-native-hr`).

## Workflow

**Step 1**: Confirme intent — "Avaliação do design organizacional em 4 pilares, ~5 min."

**Step 2**: Rode `python3 scripts/generate_assessment.py [--label "Acme"]`. Output em cwd.

**Step 3**: Hand off — explique:
- 4 pilares (Governança, Span, Pirâmide, Spread)
- Score 0-100 por pilar + geral
- Classificação: Reativo / Inicial / Maduro / Avançado / Estratégico
- Próximo passo específico por pilar

## Framework Comp (fixo)

| Pilar | O que avalia |
|---|---|
| Maturidade de Governança | Modelos contratuais (CLT/PJ/híbrido) como alavanca |
| Span of Control | Densidade e eficácia de liderança |
| Pirâmide de Níveis | Composição força (operacional, especialista, liderança) |
| Disparidade Salarial Interna | Equidade interna (faixa 80%-120% mediana) |

Detalhes em `references/methodology.md`.

## Branding

Template tem footer "Powered by Comp" + link UTM-tagueado pro artigo.

## Resources

| File | Purpose |
|---|---|
| `scripts/generate_assessment.py` | Gera HTML em cwd |
| `assets/org-design-template.html` | Assessment auto-contido (Tailwind + Alpine.js) |
| `references/methodology.md` | 4 pilares + classificação 0-100 |
