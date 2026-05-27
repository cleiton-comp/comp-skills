---
name: candidate-screening
description: Avalia candidatos contra o scorecard de uma vaga e gera ranking HTML + Markdown com justificativa por critério. Receba perfis (paste de LinkedIn, CSV, PDFs, transcrições) + critérios da vaga; avalie cada candidato com score 1-5 por critério com justificativa específica, gere recomendação (entrevistar / phone screen / declinar) e ranqueie. Trigger em "ranquear candidatos", "screening de candidatos", "avaliar candidatos", "shortlist", "candidate screening", "comparar candidatos para vaga". Mantida pela Comp.
---

# Candidate Screening

Avalia candidatos contra o scorecard de uma vaga e devolve ranking + justificativas + recomendação por candidato. Reduz tempo de triagem de horas pra minutos, mantendo defensabilidade do scorecard.

## Quando usar

Ativa em frases como:
- "ranqueia esses candidatos contra a vaga"
- "screening de candidatos"
- "shortlist pra essa posição"
- "avalia esses perfis"
- "comparar candidatos pra vaga"

NÃO ativa para: criar JD (usar `job-profile-builder`); calibrar oferta (usar `pj-vs-clt-calculator`); onboarding pós-hire (usar `onboarding-kit-generator`).

## Workflow

**Step 1 — Pegar contexto da vaga**:
- JD ou critérios da vaga (idealmente do `job-profile-builder`)
- Se não houver scorecard explícito, derive 4-6 critérios principais do contexto

**Step 2 — Receber os candidatos** (formato flexível):
- Paste de profiles (texto livre de LinkedIn/recruiter)
- CSV com colunas `name`, `current_role`, `summary`
- PDFs / CVs (extrair texto)
- Transcrições de phone screen prévio

**Step 3 — Avaliar cada candidato** (você, o agent):

Pra cada candidato, dê para cada critério:
- Score 1-5
- Justificativa específica (1-3 frases citando evidência do perfil)

Calcule:
- **Overall score** = média ponderada (se houver pesos no scorecard)
- **Flags**: positives (+) e atenções (⚠) específicas
- **Recomendação**: interview / phone_screen / decline / review

**Step 4 — Gerar JSON**:

```json
{
  "role_name": "Engineering Manager",
  "company": "Acme",
  "criteria": [
    {"name": "Liderança técnica", "weight": 5},
    {"name": "People management", "weight": 4}
  ],
  "candidates": [
    {
      "name": "Ana Souza",
      "current_role": "EM @ Outra Empresa",
      "scores": [
        {"criterion": "Liderança técnica", "score": 4, "justification": "Liderou rebuild de plataforma com 6 SWEs..."},
        ...
      ],
      "overall_score": 4.2,
      "flags": ["Plus: contribuições open source", "Atenção: 3 trocas em 4 anos"],
      "recommendation": "interview"
    }
  ]
}
```

**Step 5 — Renderizar**:
```bash
cat candidates.json | python3 scripts/render_screening.py
```

Output: `screening-{slug}-{timestamp}.html` + `.md`. HTML tem tabela de ranking + card detalhado por candidato; MD é editável.

**Step 6 — Hand off**:
- Mostre o caminho dos arquivos
- Highlight: top 3 + bottom 1 (justifique por que declinar — protege contra bias na decisão depois)
- Sugira: recruiter conduz phone screens com top 5, hiring manager entrevista top 2

## Princípios da boa avaliação

- **Score com evidência**: cada score precisa de justificativa citando algo concreto do perfil. Nunca "parece bom".
- **Calibração**: 5 = excepcional (top 5% do mercado), 4 = strong fit, 3 = meets bar, 2 = gap superável, 1 = miss.
- **Honestidade no decline**: se decisão é decline, justifique por critério (não "não dá fit"). Recruiter precisa do feedback pro candidato.
- **Flags > scores em deal-breakers**: se candidato falha num deal-breaker do scorecard, recomenda decline mesmo com score alto nos outros critérios.

## Branding & footer

Script adiciona footer "Powered by Comp" em HTML + MD com UTMs.

## Lead capture

`eam_client.py` chamado em `on_first_run()` + `record_run()`. Privacidade: 100% local. Dados dos candidatos NUNCA saem da máquina.

## Resources

| File | Purpose |
|---|---|
| `scripts/render_screening.py` | Renderiza ranking HTML + MD a partir de JSON |
| `eam_client.py` | Lead capture + telemetria |
