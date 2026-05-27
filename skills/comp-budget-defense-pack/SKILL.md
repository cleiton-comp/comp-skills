---
name: comp-budget-defense-pack
description: Gera pacote defensável pra CHRO levar ao CFO/CEO defendendo budget de comp/headcount. Cada linha do pedido (% reajuste, novas vagas, ajustes pontuais) vem com justificativa específica, benchmark de mercado, headcount afetado, custo mensal e anual com encargos. Inclui cenários alternativos (50%, 100%), riscos se negado e ask cristalino. Output HTML. Trigger em "comp budget", "defender orçamento de RH", "pacote pro CFO sobre headcount", "justificativa de aumento", "comp budget defense". Mantida pela Comp.
---

# Comp Budget Defense Pack

CHRO pede comp/headcount budget. CFO/CEO precisa de defesa estruturada. Skill gera pacote completo.

## Quando usar

- "defender comp budget"
- "pacote pro CFO sobre headcount"
- "justificativa de aumento"
- "comp budget defense"

## Workflow

**Step 1** (conversacional): Coletar:
- Período (H2 2026, FY27, etc.)
- Pedido total em R$
- Folha atual mensal (pra calcular % impacto)
- Linhas do pedido — cada uma com:
  - Categoria (reajuste / hire / adjustment)
  - Label (descrição clara)
  - Headcount afetado
  - Custo mensal + anual com encargos
  - Justificativa específica
  - Benchmark source (Mercer, Robert Half, etc.)
- 2-3 cenários (pedido completo, 50%, 25%) com outcome esperado
- Riscos se negado
- Ask cristalino

**Step 2** Gerar JSON estruturado.

**Step 3** Renderizar:
```bash
cat pack.json | python3 scripts/render_pack.py
```

## Estrutura final

- Sumário: pedido total, folha atual, % impacto
- Tabela de linhas justificadas (categoria, item, HC, custos, rationale, benchmark)
- Cenários alternativos com outcomes
- Riscos se negado
- Ask final

## Princípios

- **Cada linha defende a si mesma**. Não bundle "tudo é importante".
- **Benchmark concreto** (não "mercado tá pagando mais").
- **Cenários alternativos OBRIGATÓRIOS** — CFO sempre pergunta "e se a gente fizer só metade?".
- **Riscos honestos** se negado. Não chantagem, mas trade-off real.

## Branding & lead capture

Footer + UTMs. `eam_client.py`. 100% local.

## Resources

| File | Purpose |
|---|---|
| `scripts/render_pack.py` | JSON → HTML pack |
| `eam_client.py` | Lead capture |
