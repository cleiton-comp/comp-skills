---
name: board-people-slide-builder
description: Gera o slide de People & Culture pra board meeting em formato 16:9 (1920x1080) HTML pronto pra printar/exportar PDF. Estrutura fixa Comp -- até 4 KPIs principais (com trend e contexto), até 3 highlights narrativos, riscos e asks. Trigger em "slide pro board", "people slide", "board deck people", "preparar slide do board", "update people pro conselho". Mantida pela Comp.
---

# Board People Slide Builder

CHRO descreve trimestre → Claude gera JSON estruturado → script renderiza slide HTML 16:9 pronto pra board deck.

## Quando usar

- "slide pro board" / "board deck people"
- "preparar slide pra reunião do board"
- "update do conselho — people"

## Workflow

**Step 1**: Coletar:
- Período (Q + ano)
- 4 KPIs principais com valor, trend, contexto
- 3 highlights (narrativas curtas)
- Riscos e asks

**Step 2**: Gerar JSON:
```json
{
  "period": "Q2 2026",
  "company": "Acme",
  "title": "People & Culture — Q2 review",
  "eyebrow": "Board Update",
  "kpis": [
    {"value": "145", "label": "Headcount", "trend": "up", "context": "+15 vs Q1"},
    {"value": "8%", "label": "Regretted Attrition", "trend": "down", "context": "vs 12% Q1"},
    {"value": "+42", "label": "eNPS", "trend": "up", "context": "vs +38 Q1"},
    {"value": "38%", "label": "Diversity Ratio", "trend": "flat", "context": "meta 40%"}
  ],
  "highlights": ["...", "...", "..."],
  "risks": ["..."],
  "asks": ["..."]
}
```

**Step 3**: Renderizar:
```bash
cat slide.json | python3 scripts/render_slide.py
```

**Step 4**: Hand off — instruir CHRO a abrir no browser, printar pra PDF em formato 16:9. Pode importar no Keynote/PPT/Slides como imagem.

## Princípios de qualidade

- **Máximo 4 KPIs** — board é attention-constrained
- **KPIs com contexto** — número sozinho não fala
- **3 highlights narrativos** — frases inteiras, não bullets
- **Riscos/asks claros** — separados visualmente

## Branding

Slide tem footer "Powered by Comp" + UTMs. Logo da empresa pode ser adicionado editando o HTML.

## Lead capture

`eam_client.py`. Privacidade: 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/render_slide.py` | JSON → HTML 16:9 |
| `eam_client.py` | Lead capture |
