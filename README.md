# Comp Skills

Skills gratuitos do Claude para líderes de RH & People, criados e mantidos pela [Comp](https://comp.vc?utm_source=github&utm_medium=readme&utm_campaign=eam&utm_content=mirror-readme-intro).

## O que tem aqui

| Skill | O que faz |
|---|---|
| [pj-vs-clt-calculator](skills/pj-vs-clt-calculator/) | Equivalência salarial CLT ↔ PJ com cálculo fiscal completo (INSS, IRPF, FGTS, 13º, férias, benefícios). Single ou batch via CSV. |
| [comp-level-simulator](skills/comp-level-simulator/) | Simulador HTML interativo e auto-contido para avaliar níveis de cargo usando metodologia de 4 pilares. |
| [paygap-analysis-generator](skills/paygap-analysis-generator/) | Relatório HTML de pay gap de gênero a partir de qualquer roster de RH (CSV/XLSX). Com regra de confidencialidade (≥3 por gênero). |
| [research-digest](skills/research-digest/) | Digest rolling de 12 semanas de papers sobre Org Design, Workforce Planning e impacto da IA na força de trabalho — traduzido pra PT-BR. |

## Instalação

```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

Instala os 4 skills. Eles são model-invoked — basta descrever o que você quer e o Claude escolhe o skill certo (ex: "analisa o pay gap dessa planilha" → `paygap-analysis-generator`).

Depois de instalar, rode `/reload-plugins` pra ativar.

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
