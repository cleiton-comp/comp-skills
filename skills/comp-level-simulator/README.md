# comp-level-simulator

Free Claude skill for HR & People leaders. Generates a self-contained interactive HTML simulator for evaluating job levels (L1–L6) using the Comp methodology — 4 pillars (Influence, Autonomy, Complexity, Responsibility), 8 questions, A–E scale.

Maintained by **Comp** ([comp.vc](https://comp.vc?utm_source=github&utm_medium=readme&utm_campaign=eam&utm_content=skill-comp-level-simulator)).

## What it does

Generates one HTML file per run. Open it in any browser — it walks you (or whoever you share it with) through 8 questions and outputs a calibrated job level. The file is self-contained: no backend, no data sent anywhere, works offline once generated.

Use it to:
- Standardize leveling decisions across the org
- Hand managers a self-service tool to grade new positions
- Remove bias (salary, title, tenure) from level conversations
- Validate an HR/talent leveling proposal before publishing

## Install

### Marketplace (all 4 Comp skills)
```bash
/plugin marketplace add cleiton-comp/comp-skills
/plugin install comp-skills@comp
```

This installs the whole `comp-skills` plugin (4 skills, one of which is this one).

### Manual (zip)
Download the `.zip` from our LP, then drop the unzipped folder in your `~/.claude/skills/` directory.

## Usage

Just talk to Claude. Examples:

- "Gera um simulador de nível pra eu mandar pros gestores"
- "Quero avaliar o nível dessa nova posição de Eng Manager"
- "Como nivelar uma posição? Tem uma ferramenta?"
- "Padroniza a avaliação de level aqui na empresa"

Claude generates a `Comp-Level-Simulator-{timestamp}.html` in your current directory. Open in a browser, share via Drive/email, or host anywhere.

## Methodology

| Pillar | Questions | Score per Q (A→E) |
|---|---|---|
| Influence | 2 | 5, 4, 3, 2, 1 |
| Autonomy | 2 | 5, 4, 3, 2, 1 |
| Complexity | 2 | 5, 4, 3, 2, 1 |
| Responsibility | 2 | 5, 4, 3, 2, 1 |

Total: 8–40. Maps to L1 (Junior) → L6 (Senior Specialist / Senior Manager). L5–L6 are compressed at the top — reaching executive levels requires consistently high scores across all pillars.

## What gets shared with Comp

On first run you'll be prompted for:
1. Your email (optional) — only used to notify you of skill updates.
2. Anonymous telemetry (default: off) — if enabled, sends skill name + timestamp on each run. **Never sends your inputs or the HTML you generate.**

The HTML itself **never** phones home — it's pure client-side JS. Everything you fill in stays in the browser.

Both opt-ins are stored locally in `~/.comp-skills/config.json`. Edit or delete that file any time to revoke.

## Issues

Open an issue at [cleiton-comp/comp-skills](https://github.com/cleiton-comp/comp-skills/issues) with the `eam` label.

— Powered by Comp · Free skills for HR & People leaders.
