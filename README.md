# Jahani design skills

Four agent skills for building web dashboards and Persian (RTL) interfaces, distilled from building
[jahanicoaching.ir](https://jahanicoaching.ir). They work with Claude Code and Cursor (standard `SKILL.md` format).

| Skill | What it covers |
|---|---|
| `motion-rules` | 20 motion rules, 12 transitions.dev recipes, per-page skeletons, page transitions, save indicator (+ `tokens.css`) |
| `ux-laws` | Fitts, Hick, Jakob, proximity, Von Restorff, with concrete rules |
| `dashboard-design` | Layout of panels and dashboards, desktop and mobile |
| `persian-rtl-ui` | RTL layout, Persian digits, toman/rial, Jalali dates, Persian copy |

## Install

With the skills CLI:

```bash
npx skills add amirhosseinjahani88-code/jahani-design-skills
```

Or by hand: copy the folders in `skills/` into

- Claude Code: `~/.claude/skills/` (all projects) or `.claude/skills/` (one project)
- Cursor: `~/.cursor/skills/` or `.cursor/skills/`
