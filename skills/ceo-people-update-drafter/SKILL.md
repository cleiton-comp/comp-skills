---
name: ceo-people-update-drafter
description: Gera o update CHRO → CEO (mensal/trimestral) em formato 1-pager. Estruturado em resumo executivo, métricas-chave (com trend e contexto), principais movimentações (hires/promoções/exits), wins, riscos (com mitigação+owner) e asks pro CEO. Output: HTML + Markdown editável. Trigger em "update pro CEO", "people update", "report mensal de RH", "update trimestral de people", "report do CHRO". Mantida pela Comp.
---

# CHRO → CEO People Update

Gera um 1-pager estruturado pro update recorrente CHRO → CEO. Reduz tempo de preparação de horas pra minutos mantendo qualidade executiva.

## Quando usar

- "update mensal pro CEO" / "people update"
- "report trimestral de RH"
- "draft do update do CHRO"
- "estruturar update pro fundador"

## Workflow

**Step 1**: Coletar do CHRO (conversacional):
- Período (Q2 2026, Mar/2026, etc.)
- Métricas-chave (com valores atuais + anteriores + contexto)
- Movimentações importantes (hires de liderança, promoções estratégicas, exits)
- Wins do período
- Riscos (com mitigação + owner)
- Asks pro CEO (decisões pendentes, recursos, support)

**Step 2**: Gerar JSON estruturado.

**Step 3**: Renderizar:
```bash
cat update.json | python3 scripts/render_update.py
```

Output: HTML 1-pager pronto + MD editável.

## Estrutura do JSON

```json
{
  "period": "Q2 2026",
  "company": "Acme",
  "executive_summary": "...",
  "metrics": [
    {"name": "Headcount", "current": 145, "previous": 130, "trend": "up", "context": "Q2 hiring acelerou"}
  ],
  "key_movements": [
    {"name": "Maria Silva", "type": "hire", "detail": "VP Engineering — começou 15/04"}
  ],
  "wins": ["..."],
  "risks": [{"risk": "...", "mitigation": "...", "owner": "..."}],
  "asks_from_ceo": ["..."]
}
```

## Princípios de qualidade

- **Métricas com contexto**: número sozinho não fala. Sempre par "atual + anterior + contexto narrativo".
- **Movimentações relevantes** apenas (não toda hire — strategic hires e exits/promoções de liderança).
- **Riscos com mitigação e owner** — não é desabafo, é planning.
- **Asks claros** — o que muda se CEO não responder? Decisão fica em quem.

## Branding

Footer + UTMs em HTML e MD.

## Lead capture

`eam_client.py`. Privacidade: 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/render_update.py` | HTML + MD a partir de JSON |
| `eam_client.py` | Lead capture |
