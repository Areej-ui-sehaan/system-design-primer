# Skills

## `system-design` (v3.0.0)

System design architect + interview coach distilled from this repo's System Design Primer.

| Path | Role |
|---|---|
| `system-design/SKILL.md` | Entry point: frontmatter routing, invocation modes, 4-step method |
| `system-design/references/` | On-demand knowledge: numbers, topic playbook, question catalog, few-shot routing examples, scoring rubric |
| `system-design/templates/` | Fill-in design-doc template |
| `system-design/scripts/estimate.py` | Back-of-the-envelope CLI (qps / storage / shards / bandwidth / full) |
| `system-design/scripts/validate_skill.py` | Package validator (frontmatter, internal refs, zip parity) |
| `system-design.skill` | Distributable package (zip) of the skill folder |

### Changelog

- **3.0.0** — bundled `scripts/` (estimator + validator), few-shot invocation examples, interview/OOD scoring rubric + closing checklist; wired into mode router
- **2.1.0** — standalone-safe: graceful degradation when used outside this repo
- **2.0.0** — invocation overhaul (modes, explicit syntax per surface, aliases) + `.skill` package
- **1.0.0** — initial skill distilled from the primer

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

**Modes** — `interview` · `design` · `review` · `estimate` · `decide` · `ood` · `study` (see the Invocation section in `SKILL.md`; each mode loads only its own reference file). Routing edge cases: `references/examples.md`.

## Validate & rebuild the package

```bash
# after any edit:
python3 skills/system-design/scripts/validate_skill.py
(cd skills && rm -f system-design.skill && zip -r system-design.skill system-design -x '*.DS_Store')
python3 skills/system-design/scripts/validate_skill.py   # confirms zip ↔ directory parity
```
