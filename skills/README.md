# Skills

## `system-design` (v4.0.0)

System design architect + interview coach distilled from this repo's System Design Primer.

| Path | Role |
|---|---|
| `system-design/SKILL.md` | Entry point: frontmatter routing, invocation modes, 4-step method |
| `system-design/references/` | On-demand knowledge: numbers, topic playbook, question catalog, few-shot routing examples, scoring rubric, bundled worked exemplar, mermaid diagram library |
| `system-design/templates/` | Fill-in design-doc template |
| `system-design/scripts/estimate.py` | Back-of-the-envelope CLI (qps / storage / shards / bandwidth / full) |
| `system-design/scripts/gen_flashcards.py` | Flashcard generator for study mode (markdown / Anki TSV / JSON) |
| `system-design/scripts/validate_skill.py` | Package validator (frontmatter, internal refs, zip parity) |
| `system-design.skill` | Distributable package (zip) of the skill folder |
| `../.claude/commands/system-design.md` | Claude Code `/system-design` slash-command stub → routes into the skill |

### Changelog

- **4.0.0** — bundled worked exemplar (Pastebin condensed) for true standalone design answers; mermaid diagram snippet library; `gen_flashcards.py` for study mode; `/system-design` slash-command stub
- **3.0.0** — bundled `scripts/` (estimator + validator), few-shot invocation examples, interview/OOD scoring rubric + closing checklist; wired into mode router
- **2.1.0** — standalone-safe: graceful degradation when used outside this repo
- **2.0.0** — invocation overhaul (modes, explicit syntax per surface, aliases) + `.skill` package
- **1.0.0** — initial skill distilled from the primer

## Install / invoke

**claude.ai** — Settings → Features → Custom Skills → upload `system-design.skill`.

**Claude Code** — extract into the project's skills directory (slash command already at `.claude/commands/system-design.md` in this repo), then:

```bash
unzip skills/system-design.skill -d .claude/skills/
# /system-design design a rate limiter
```

**Codex / open-spec agents** — extract into `.agents/skills/` (or your agent's skills dir), then `$system-design …`.

**Any agent** — point it at `skills/system-design/SKILL.md` and say "follow this skill."

**Auto-invocation** — no syntax needed: the frontmatter `description` matches requests like *"design a URL shortener"*, *"review this architecture"*, *"SQL or NoSQL?"*, *"back-of-the-envelope for 10M DAU"*, *"system design interview prep"*.

**Modes** — `interview` · `design` · `review` · `estimate` · `decide` · `ood` · `study` (see the Invocation section in `SKILL.md`; each mode loads only its own reference file). Routing edge cases: `references/examples.md`.

**Study drill deck** (standalone, no Anki required to generate):

```bash
python3 skills/system-design/scripts/gen_flashcards.py --deck all --format tsv --out cards.tsv  # import into Anki
python3 skills/system-design/scripts/gen_flashcards.py --deck numbers --format markdown         # read directly
```

## Validate & rebuild the package

```bash
# after any edit:
python3 skills/system-design/scripts/validate_skill.py
(cd skills && rm -f system-design.skill && zip -r system-design.skill system-design -x '*.DS_Store')
python3 skills/system-design/scripts/validate_skill.py   # confirms zip ↔ directory parity
```
