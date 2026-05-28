# Comp Skills

Skills gratuitos do Claude para líderes de RH & People, criados e mantidos pela [Comp](https://comp.vc?utm_source=github&utm_medium=readme&utm_campaign=eam&utm_content=mirror-readme-intro).

**Versão atual: v0.3.0** — 26 skills, 8 deles funcionam em Claude Code + Claude Cowork. [Ver release →](https://github.com/cleiton-comp/comp-skills/releases/latest)

## Instalação

```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

Instala os 26 skills de uma vez. Eles são model-invoked — basta descrever o que você quer e o Claude escolhe o skill certo (ex: "analisa o pay gap dessa planilha" → `paygap-analysis-generator`).

Depois de instalar, rode `/reload-plugins` pra ativar.

## O que tem aqui (26 skills)

### Calculadoras (7)

| Skill | O que faz | Dual-platform |
|---|---|---|
| [pj-vs-clt-calculator](skills/pj-vs-clt-calculator/) | Equivalência salarial CLT ↔ PJ com cálculo fiscal completo (INSS, IRPF, FGTS, 13º, férias, benefícios). Single ou batch via CSV. | ✅ |
| [total-comp-calculator](skills/total-comp-calculator/) | Pacote completo de Total Compensation: cash (base + variável) + benefícios + equity (SOP/ILP com cenários). 2 headlines + visão visual. | ✅ |
| [custo-demissao-calculator](skills/custo-demissao-calculator/) | Custo de rescisão CLT decomposto (saldo, aviso, 13º, férias, FGTS, INSS, IRPF) nos 4 tipos de demissão. | ✅ |
| [custo-turnover-calculator](skills/custo-turnover-calculator/) | Custo real (oculto) de turnover em 8 componentes. Quick mode (multiplicadores) ou detailed. Baseado no artigo Cajuína. | ✅ |
| [custo-folha-simulator](skills/custo-folha-simulator/) | Custo total empregador (salários + encargos + provisões). Estimate ou CSV roster. | ✅ |
| [reajuste-impact-calculator](skills/reajuste-impact-calculator/) | Impacto financeiro de reajuste salarial (flat, por nível ou por área) com × 1,555 full load. | ✅ |
| [stock-options-calculator](skills/stock-options-calculator/) | Modela vesting, diluição, cenários de exit em empresas de capital fechado. Baseado no artigo Cajuína. | ✅ |

### Assessments HTML interativos (4)

| Skill | O que faz |
|---|---|
| [comp-level-simulator](skills/comp-level-simulator/) | Simulador HTML interativo de nível de cargo usando metodologia de 4 pilares. |
| [hr-data-maturity-assessment](skills/hr-data-maturity-assessment/) | Assessment HTML de maturidade de dados de RH (5 níveis × 5 dimensões). |
| [ai-native-hr](skills/ai-native-hr/) | Assessment de prontidão pra IA em RH baseado no [AI Maturity Map da Comp](https://comp.vc/ai-maturity-map) (N1-N5 por área). |
| [org-design-assessment](skills/org-design-assessment/) | Maturidade de design organizacional (4 pilares × 3 perguntas, score 0-100). Baseado em artigo Cajuína. |

### CSV Analyzers (6)

| Skill | O que faz |
|---|---|
| [paygap-analysis-generator](skills/paygap-analysis-generator/) | Relatório HTML de pay gap de gênero a partir de qualquer roster (CSV/XLSX). Confidencialidade ≥3 por gênero. |
| [regretted-attrition-analyzer](skills/regretted-attrition-analyzer/) | Padrões em desligamentos regretted (gestor, área, tenure, performance). |
| [comp-ratio-analyzer](skills/comp-ratio-analyzer/) | Compa-ratio do roster vs bandas salariais. Outliers + custo pra equalizar. |
| [promotion-equity-analyzer](skills/promotion-equity-analyzer/) | Equidade de promoções por gênero. Gap F vs M, disparidade por área. |
| [engagement-deep-dive](skills/engagement-deep-dive/) | Segmentação de pesquisa de engajamento (eNPS) por área/tenure/manager/nível. |
| [span-of-control-diagnostic](skills/span-of-control-diagnostic/) | Diagnóstico Span of Intelligence (org chart → classificação). Baseado em artigo Cajuína. |

### Generators conversacionais (7)

| Skill | O que faz | Dual-platform |
|---|---|---|
| [onboarding-kit-generator](skills/onboarding-kit-generator/) | Plano 30/60/90 + checklist IT + 1:1s + welcome email + buddy script. HTML + MD. |  |
| [job-profile-builder](skills/job-profile-builder/) | Entrevista o hiring manager → JD completa + scorecard + roteiro de entrevistas. |  |
| [candidate-screening](skills/candidate-screening/) | Ranking de candidatos contra scorecard com justificativa por critério. |  |
| [decision-memo-generator](skills/decision-memo-generator/) | Memo estruturado (problema → opções → recomendação → ask). | ✅ |
| [ceo-people-update-drafter](skills/ceo-people-update-drafter/) | Update CHRO → CEO em formato 1-pager. |  |
| [board-people-slide-builder](skills/board-people-slide-builder/) | Slide People & Culture pra board (HTML 16:9 printable). |  |
| [comp-budget-defense-pack](skills/comp-budget-defense-pack/) | Pacote pra defender comp/headcount budget ao CFO/CEO. |  |

### Research (1)

| Skill | O que faz |
|---|---|
| [research-digest](skills/research-digest/) | Digest rolling de 12 semanas de papers (Org Design, Workforce Planning, IA na força de trabalho) traduzido pra PT-BR. |

### Orchestrator (1)

| Skill | O que faz |
|---|---|
| [chro-chief-of-staff](skills/chro-chief-of-staff/) | Chief of Staff conversacional do CHRO. Contexto persistente, pré-meeting briefs, drafts de comunicação, open loops tracker. Orquestra os outros 25 skills. |

## Dual-platform (Code + Cowork)

8 skills funcionam tanto em **Claude Code** quanto em **Claude Cowork**: pj-vs-clt, total-comp, custo-demissao, custo-turnover, custo-folha, reajuste-impact, stock-options, decision-memo. Os outros 18 são Claude Code only (dependem de filesystem, HTML interativo standalone, ou config persistente).

Matriz completa de compatibilidade em [MARKETPLACE.md no monorepo](https://github.com/trycomp-io/growth/blob/main/eam/distribution/MARKETPLACE.md).

## Instalação só de um skill específico

Pra puxar só um (em vez do plugin inteiro), baixe o `.zip` da [release mais recente](https://github.com/cleiton-comp/comp-skills/releases/latest) e descompacte em `~/.claude/skills/`.

## Privacidade

Esses skills rodam **localmente** no seu Claude. Dados de salário, rosters e qualquer análise ficam na sua máquina — nada disso é enviado pra fora.

Na primeira execução, cada skill pergunta uma única vez se você quer:
1. **Atualizações por email** (opcional) — apenas para notificar melhorias dos skills.
2. **Telemetria anônima de uso** (default: **off**) — se ativada, envia apenas o nome do skill + timestamp por execução. **Nunca** seus inputs, outputs ou dados de roster.

Ambos os opt-ins ficam em `~/.comp-skills/config.json`. Apague o arquivo a qualquer momento para revogar.

## Issues e feedback

Abra uma [issue](https://github.com/cleiton-comp/comp-skills/issues) — lemos todas.

## Licença

[MIT](LICENSE) — livre para usar, forkar e redistribuir. Atribuição apreciada.

## Sobre a Comp

A Comp é um serviço de RH AI-native para empresas em crescimento rápido. Embarcamos executivos de RH e engenheiros de IA nos times dos nossos clientes. Esses skills são uma pequena fatia do que construímos internamente — liberados gratuitamente porque ferramentas de RH melhores são boas pra todo mundo.

[comp.vc](https://comp.vc?utm_source=github&utm_medium=readme&utm_campaign=eam&utm_content=mirror-readme-footer)
