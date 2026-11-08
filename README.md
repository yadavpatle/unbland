# Unbland

Anti-AI-slop design skill for Flutter™ apps. Works with
[Claude Code](https://docs.claude.com/en/docs/claude-code/skills) and [Kiro](https://kiro.dev).

Unbland audits screens, store screenshots and promo assets for the defaults AI generators
reach for, and for the accessibility gaps they leave behind. Then it fixes them inside your
app's own design system instead of swapping one cliché for another.

- **AI design tells:** decorative gradients, glow, glass, emoji icons, tracked-caps eyebrows,
  card-in-card, template copy
- **Mobile UX defects:** contrast, 48dp targets, text scaling, missing loading/empty/error
  states, reduce motion, safe areas
- **Design-system drift:** raw colours, inline font sizes, off-scale spacing
- **Product truth:** no invented stats, testimonials or features; no "free"/"best"/"#1" on
  store preview assets

## Modes

| Mode | What it does |
| --- | --- |
| `audit <path>` | Report only, edits nothing |
| `fix <path>` | Smallest edits that clear the findings, inside your existing theme |
| `build <screen>` | New screen with all states, critiqued before code |
| `promo` | Store screenshots, feature graphic, promo video |

Findings are tiered: **Floor** (F1–F12, never waivable), **Reflex** (R1–R18, fix or waive on
the record) and **Polish** (P1–P10, advisory). See
[`skills/unbland/references/gates.md`](skills/unbland/references/gates.md).

## Install

Copy `skills/unbland` into your project's skills folder:

| Agent | Path |
| --- | --- |
| Claude Code, one project | `.claude/skills/unbland/` |
| Claude Code, all projects | `~/.claude/skills/unbland/` |
| Kiro, one project | `.kiro/skills/unbland/` |

macOS / Linux:

```sh
git clone https://github.com/yadavpatle/unbland /tmp/unbland
mkdir -p .claude/skills            # or .kiro/skills
cp -r /tmp/unbland/skills/unbland .claude/skills/
```

Windows (PowerShell):

```powershell
git clone https://github.com/yadavpatle/unbland $env:TEMP\unbland
New-Item -ItemType Directory -Force .claude\skills | Out-Null   # or .kiro\skills
Copy-Item -Recurse $env:TEMP\unbland\skills\unbland .claude\skills\
```

## Use

Ask in plain words ("audit the home screen", "does this look AI-generated", "polish
lib/features/profile") or invoke `/unbland audit lib`.

## craftlint

Unbland ships a zero-dependency linter (Node 18+) for the code-certain checks. Run it from
your project root:

```sh
node .claude/skills/unbland/scripts/craftlint.mjs lib --summary
node .claude/skills/unbland/scripts/craftlint.mjs lib --gate F1,F6
node .claude/skills/unbland/scripts/craftlint.mjs contrast "#FFFFFF" "#C6F432"
node .claude/skills/unbland/scripts/craftlint.mjs tokens
```

Optional project settings go in `craft.config.json` at the project root; see
[`references/config.md`](skills/unbland/references/config.md). A design contract
(`DESIGN.md`) can be started from
[`references/contract-template.md`](skills/unbland/references/contract-template.md).

## License

[MIT](LICENSE)

---

Flutter and the related logo are trademarks of Google LLC. Unbland is not endorsed by or
affiliated with Google LLC.
