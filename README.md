# flutter-craft

An agent skill for Flutter apps that makes screens look designed, not generated, and keeps an
accessibility floor. Works with [Claude Code](https://docs.claude.com/en/docs/claude-code/skills)
and [Kiro](https://kiro.dev).

It audits for AI design tells (decorative gradients, glow, glass, emoji icons, tracked-caps
eyebrows, card-in-card, template copy), mobile UX defects (contrast, 48dp targets, text
scaling, missing loading/empty/error states, reduce motion) and drift from your project's own
design system. It also covers store screenshots, feature graphics and promo videos.

## Modes

| Mode | What it does |
| --- | --- |
| `audit <path>` | Report only, edits nothing |
| `fix <path>` | Smallest edits that clear the findings, inside your existing theme |
| `build <screen>` | New screen with all states, critiqued before code |
| `promo` | Store screenshots, feature graphic, promo video |

Findings are tiered: **Floor** (F1–F12, never waivable), **Reflex** (R1–R18, fix or waive on
the record) and **Polish** (P1–P10, advisory). See
[`skills/flutter-craft/references/gates.md`](skills/flutter-craft/references/gates.md).

## Install

Copy `skills/flutter-craft` into your Flutter project.

**Claude Code** (project): `.claude/skills/flutter-craft/`
**Claude Code** (all projects): `~/.claude/skills/flutter-craft/`
**Kiro** (project): `.kiro/skills/flutter-craft/`

macOS / Linux:

```sh
git clone https://github.com/<you>/flutter-craft /tmp/flutter-craft
mkdir -p .claude/skills            # or .kiro/skills
cp -r /tmp/flutter-craft/skills/flutter-craft .claude/skills/
```

Windows (PowerShell):

```powershell
git clone https://github.com/<you>/flutter-craft $env:TEMP\flutter-craft
New-Item -ItemType Directory -Force .claude\skills | Out-Null   # or .kiro\skills
Copy-Item -Recurse $env:TEMP\flutter-craft\skills\flutter-craft .claude\skills\
```

## Use

Ask the agent in plain words ("audit the home screen", "does this look AI-generated",
"polish lib/features/profile") or invoke `/flutter-craft audit lib`.

## craftlint

The skill ships a zero-dependency linter (Node 18+) for the code-certain checks. Run it from
your project root:

```sh
node .claude/skills/flutter-craft/scripts/craftlint.mjs lib --summary
node .claude/skills/flutter-craft/scripts/craftlint.mjs lib --gate F1,F6
node .claude/skills/flutter-craft/scripts/craftlint.mjs contrast "#FFFFFF" "#C6F432"
node .claude/skills/flutter-craft/scripts/craftlint.mjs tokens
```

Optional project settings go in `craft.config.json` at the project root; see
[`references/config.md`](skills/flutter-craft/references/config.md). A design contract
(`DESIGN.md`) can be started from
[`references/contract-template.md`](skills/flutter-craft/references/contract-template.md).

## License

[MIT](LICENSE)
