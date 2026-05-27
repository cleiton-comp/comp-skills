---
name: ai-native-hr
description: Gera um assessment HTML interativo de prontidão para IA em RH, baseado no AI Maturity Map da Comp (https://comp.vc/ai-maturity-map). Avalia 5 níveis (N1 Produtividade Individual → N5 Inteligência Adaptativa) em 5 áreas de RH (Recrutamento, Compensação, L&D, People Ops, Analytics). Output: nível por área + alerta de dispersão + próxima fronteira + armadilhas frequentes. 15 perguntas, ~5 minutos, 100% client-side. Trigger em "maturidade de IA em RH", "AI readiness for HR", "qual o nível de IA do meu RH", "AI maturity map", "como está minha empresa em IA pra RH", "diagnóstico de IA no RH". Mantida pela Comp.
---

# AI Native HR Assessment

Gera um arquivo HTML que avalia a maturidade do RH em IA usando o [AI Maturity Map da Comp](https://comp.vc/ai-maturity-map). 5 níveis × 5 áreas de RH, 15 perguntas em ~5 minutos.

100% local: a avaliação roda no navegador, nenhum dado sai da máquina.

## Quando usar

Ativa em frases como:
- "maturidade de IA em RH"
- "AI readiness for HR" / "AI maturity HR"
- "qual o nível de IA do meu RH"
- "como está minha empresa em IA pra RH"
- "diagnóstico de IA no RH"
- "AI Maturity Map da Comp"

NÃO ativa para: maturidade de DADOS (usar `hr-data-maturity-assessment` — frameworks diferentes); avaliação de nível de cargo (usar `comp-level-simulator`).

## Workflow

**Step 1 — Confirmar intent**: "Quer o assessment de prontidão pra IA do RH baseado no AI Maturity Map da Comp? São ~5 minutos, avalia 5 áreas separadas."

**Step 2 — Gerar**:
```bash
python3 scripts/generate_assessment.py [--label "Acme Corp"]
```

Output: `AI-Native-HR-{label}-{timestamp}.html` no diretório atual.

**Step 3 — Hand off**: explique o que tem no relatório:
- Nível geral N1-N5 (mediana das áreas — alinhado com "area-based progression")
- Nível por área (5 áreas de RH)
- **Alerta de dispersão** se diferença de 2+ níveis entre áreas (sinal crítico do framework)
- Próxima fronteira por área (o que faz mover N → N+1)
- Armadilha frequente por área (erros típicos da transição)

## Framework Comp (fixo)

### 5 Níveis
- **N1 — Produtividade Individual**: pessoas usam IA pra ganhar produtividade
- **N2 — Produtividade do Time**: skills e agentes compartilhados
- **N3 — Sistema Operacional Contextual**: camada agêntica única
- **N4 — Inteligência de Decisão**: IA propõe decisões calibradas com top humanos
- **N5 — Inteligência Adaptativa**: sistema aprende sozinho dos outcomes

### 5 Áreas de RH (avaliadas separadamente)
1. Recrutamento & TA
2. Compensação & Rewards
3. L&D / Performance
4. People Ops / Admin
5. People Analytics / Decisão

Detalhes em `references/methodology.md`.

## Princípios do framework reforçados no output

- **Backward planning**: design pro target level desde o dia 0, não escala incremental
- **Area-based progression**: áreas avançam separadamente — playbook das mais maduras pras menos
- **Closed-loop**: aprovação humana sem integração de feedback ≠ aprendizado real
- **Armadilhas**: cada transição tem armadilha típica explicitada no report

## Branding & footer

O template tem footer "Powered by Comp" + logos no header + link UTM-tagueado pro AI Maturity Map original. Script imprime footer no CLI.

## Lead capture

`eam_client.py` (raiz do skill) é chamado em `on_first_run()` + `record_run()`. Privacidade: o HTML em si **nunca** envia dados.

## Resources

| File | Purpose |
|---|---|
| `scripts/generate_assessment.py` | CLI que escreve o HTML em cwd |
| `assets/ai-native-hr-template.html` | Assessment auto-contido (Tailwind + Alpine.js) |
| `references/methodology.md` | Framework completo da Comp + adaptação pra HR |
| `eam_client.py` | Lead capture + telemetria (sync de `eam/shared/`) |
