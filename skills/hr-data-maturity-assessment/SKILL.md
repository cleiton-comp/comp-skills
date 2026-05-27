---
name: hr-data-maturity-assessment
description: Gera um assessment HTML interativo de maturidade de dados de RH em 5 níveis (Ad-hoc, Operacional, Reporting, Analytics, AI-native) × 5 dimensões (Coleta, Governança, Reporting, Análise, Tech & AI). 15 perguntas, ~5 minutos, output com nível por dimensão + roadmap personalizado pra avançar. 100% client-side. Trigger em "maturidade de dados de RH", "HR data maturity", "diagnóstico de people analytics", "qual o nível do meu RH em dados", "avaliação de people ops", "como estamos em analytics". Mantida pela Comp.
---

# HR Data Maturity Assessment

Gera um arquivo HTML auto-contido que avalia a maturidade de dados do RH em 5 dimensões × 5 níveis. CHRO/Head of People responde 15 perguntas em ~5 minutos e recebe nível por dimensão + roadmap personalizado pra avançar ao próximo nível.

100% local: a avaliação roda no navegador, nenhum dado sai da máquina.

## Quando usar

Ativa em frases como:
- "maturidade de dados de RH", "HR data maturity"
- "diagnóstico de people analytics"
- "qual o nível do meu RH em dados"
- "avaliação de people ops"
- "como estamos em analytics"
- "roadmap pra evoluir o RH em dados"

NÃO ativa para: avaliação de nível de cargo (usar `comp-level-simulator`); diagnóstico de pay equity (usar `paygap-analysis-generator`); avaliação de prontidão pra IA em RH (usar `ai-readiness-hr` — próxima skill).

## Workflow

**Step 1 — Confirmar intent**: "Quer um assessment HTML interativo de maturidade de dados do RH, certo? São ~5 minutos, output personalizado." Pergunte se quer label específico (empresa, contexto).

**Step 2 — Gerar**:
```bash
python3 scripts/generate_assessment.py [--label "Acme Corp"]
```

Output: `HR-Data-Maturity-{label}-{timestamp}.html` no diretório atual.

**Step 3 — Hand off**: informe o caminho do arquivo e explique:
- 5 dimensões em tabs (Coleta, Governança, Reporting, Análise, Tech & AI)
- 3 perguntas por dimensão, escala A-E (mapeada pra níveis 5-1)
- Resultado mostra nível por dimensão + nível geral + roadmap específico por dimensão
- Pode compartilhar via Drive/email pra usar com mais pessoas do time

## Framework (fixo)

### 5 Níveis
1. **Ad-hoc** — RH em planilhas, dados fragmentados
2. **Operacional** — HRIS centralizado, reporting sob demanda
3. **Reporting** — Dashboards com cadência, métricas core monitoradas
4. **Analytics** — Análises causa-raiz, segmentação, predição básica
5. **AI-native** — Agentes assistentes, predição contínua, automação

### 5 Dimensões
1. **Coleta & Integração** — onde dados nascem, como integram
2. **Qualidade & Governança** — dicionário, validações, ownership
3. **Reporting & Métricas** — KPIs, cadência, audiência
4. **Análise & Decisão** — como dados viram decisão
5. **Tech & AI** — stack, modelos, agentes

Detalhes em `references/methodology.md`.

## Output

O HTML mostra:
1. Nível geral (1-5) com gradiente visual
2. Grade de níveis por dimensão (heatmap textual)
3. Recomendação por dimensão pra avançar 1 nível (personalizada pelo nível atual)
4. Opção de refazer

## Branding & footer

O template já inclui o footer "Powered by Comp" + logos no header. Script imprime footer no CLI com UTM.

## Lead capture

`eam_client.py` (raiz do skill) chamado em `on_first_run()` + `record_run()`. Privacidade: o HTML em si **nunca** envia dados (puro JS client-side). Inputs do usuário ficam só no browser.

## Resources

| File | Purpose |
|---|---|
| `scripts/generate_assessment.py` | CLI que escreve o HTML em cwd |
| `assets/hr-data-maturity-template.html` | Assessment auto-contido (Tailwind + Alpine.js) |
| `references/methodology.md` | Detalhamento dos 5 níveis × 5 dimensões |
| `eam_client.py` | Lead capture + telemetria (sync de `eam/shared/`) |
