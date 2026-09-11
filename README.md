# grok-skills

User-level Grok skills for quant research desks (alpha discovery, lagged signal graphs, strategy UI).

These are **not** bundled xAI skills. They live in the common user store:

```
~/.grok/skills/<name>/SKILL.md
```

Project copies also live in a Grok Build app at `.grok/skills/` — that only affects that app.

## Skills

| Slash | Job |
| --- | --- |
| `/quant-research` | Alpha discovery, lag, costs, IS/OOS verdicts |
| `/stock-signal-charts` | IC series, lag decay, price+z overlay, heatmap, terciles |
| `/stock-strategy-ui` | Monthly grid, rolling OOS windows, weights |
| `/quant-ui-generation` | Tokenized desk chrome / Recharts recipes |

## Install (CLI / Grok Build)

```bash
git clone git@github.com:praveenguptahcl/grok-skills.git
mkdir -p ~/.grok/skills
cp -a grok-skills/.grok/skills/. ~/.grok/skills/
```

Optional `~/.grok/config.toml`:

```toml
[skills]
paths = ["~/.grok/skills"]
```

## grok.com Skills

The grok.com / iOS / Android Skills library is a **separate** cloud store. This repo does not auto-publish there. Paste a skill or attach the folder in Skills if you want it on every Grok chat.

## Honesty

Simulated universes stay labeled. Verdicts are REJECT / WEAK / WATCH. No live-edge claims.
