---
name: span-of-control-diagnostic
description: Diagnóstico de Span of Intelligence — evolução do span of control tradicional. Lê CSV/XLSX da org (employee, manager, opcionalmente ai_agents + automation_pct) e gera relatório HTML com classificação dos gestores em Tradicional / Híbrido / Orquestração / Subutilizado / Sobrecarregado-sem-IA. Recomendações reframed (em vez de "quebre time grande", sugere "automatize ou senior-ize"). Baseado no artigo Comp na Cajuína. Trigger em "span of control", "span of intelligence", "diagnóstico organizacional", "análise de org", "estrutura organizacional", "camadas", "manager-to-IC ratio", "layers". Mantida pela Comp.
---

# Span of Intelligence Diagnostic

Lê o org chart da empresa (CSV/XLSX) e gera relatório HTML com diagnóstico de estrutura organizacional usando o framework **Span of Intelligence** (artigo Cajuína), evolução do span of control tradicional.

100% local: dados nunca saem da máquina.

## Quando usar

Ativa em frases como:
- "span of control", "span of intelligence"
- "diagnóstico organizacional", "análise de org"
- "estrutura organizacional", "camadas", "layers"
- "manager-to-IC ratio"
- "como está minha org chart"
- "avaliação de span"

## Workflow

**Step 1 — Pegar o arquivo**: pergunte ao usuário o caminho do CSV/XLSX. Schema:
- Obrigatórias (auto-detect): `employee_id`, `name`, `manager_id`
- Opcionais (auto-detect): `area`, `level`
- **Opcionais críticas pra SoI completo**: `ai_agents` (nº agentes IA do time), `automation_pct` (% trabalho automatizado), `complexity` (low/medium/high)

**Step 2 — Auto-detect das colunas**: rode o script e veja quais colunas foram detectadas. Se algo faltar, pergunte ao usuário e use as flags `--<col>-col`.

**Step 3 — Rodar**:
```bash
python3 scripts/span_analysis.py --input org.csv
```

**Step 4 — Apresentar**:
- Highlights do summary (HC, gestores, camadas)
- Classificação SoI: quantos em cada categoria
- Recomendações específicas (não "quebre se >15" — em vez disso "avalie agentes ou senior-ize")
- Se sem dados de IA, mencione que análise completa requer essas colunas

## Framework Span of Intelligence

Tradicional: "quantos diretos um gestor tem?"
Intelligence: "quanta inteligência aquele time gera?"

Classificação por gestor:
- **Tradicional** — humanos puros, span razoável, zero IA. Estrutura clássica.
- **Híbrido** — 1+ agente ou 20-60% automação. Transição em curso.
- **Orquestração** — 2+ agentes ou 60%+ automação. Gestor é orquestrador.
- **Subutilizado** — span <4 sem IA. Oportunidade pra senior-izar (eliminar camada).
- **Sobrecarregado (sem IA)** — span >12 sem IA. Avalie agentes antes de splitting.

Detalhes + 12 critérios qualitativos do artigo em `references/methodology.md`.

## Recomendações automáticas

O skill gera recomendações específicas baseadas no padrão da org:
- Sobrecarregados sem IA → "automatize antes de quebrar time"
- Subutilizados → "senior-ize"
- Muitas camadas (>6) → "achatamento via agentificação"
- Sem dados de IA → "adicione colunas pra análise completa"

## Branding & footer

Template HTML tem footer "Powered by Comp" + link UTM-tagueado pro artigo original.

## Lead capture

`eam_client.py` chamado em `on_first_run()` + `record_run()`. Privacidade: processamento 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/span_analysis.py` | Análise + HTML render |
| `references/methodology.md` | Span of Intelligence framework + 12 critérios |
| `eam_client.py` | Lead capture + telemetria |
