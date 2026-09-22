# Skills

## `system-design` (v2.0.0)

System design architect + interview coach distilled from this repo's System Design Primer.

| File | Role |
|---|---|
| `system-design/SKILL.md` | Entry point: frontmatter routing, invocation modes, 4-step method |
| `system-design/references/` | On-demand knowledge: numbers, topic playbook, question catalog |
| `system-design/templates/` | Fill-in design-doc template |
| `system-design.skill` | Distributable package (zip) of the skill folder |

## Install / invoke

**claude.ai** — Settings → Features → Custom Skills → upload `system-design.skill`.

**Claude Code** — extract into the project's skills directory, then:

```bash
unzip skills/system-design.skill -d .claude/skills/
# /system-design design a rate limiter
```

**Codex / open-spec agents** — extract into `.agents/skills/` (or your agent's skills dir), then `$system-design …`.

**Any agent** — point it at `skills/system-design/SKILL.md` and say "follow this skill."

**Auto-invocation** — no syntax needed: the frontmatter `description` matches requests like *"design a URL shortener"*, *"review this architecture"*, *"SQL or NoSQL?"*, *"back-of-the-envelope for 10M DAU"*, *"system design interview prep"*.

**Modes** — `interview` · `design` · `review` · `estimate` · `decide` · `ood` · `study` (see the Invocation section in `SKILL.md`; each mode loads only its own reference file).

## Rebuild the package

```bash
(cd skills && rm -f system-design.skill && zip -r system-design.skill system-design -x '*.DS_Store')
```
