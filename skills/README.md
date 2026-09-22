# Skills

## `system-design` (v5.0.0)

System design architect + interview coach distilled from **the entire** System Design Primer repo.

| Path | Role |
|---|---|
| `system-design/SKILL.md` | Entry point: frontmatter routing, invocation modes, 4-step method |
| `system-design/references/` | On-demand knowledge: numbers, topic playbook, question catalog, few-shot examples, scoring rubric, worked exemplar, **all-8 solutions index**, **all-6 OOD class designs**, diagram library, study extras |
| `system-design/data/anki_cards.json` | Primer's 3 Anki decks extracted (56 cards: system / exercises / oo) |
| `system-design/templates/` | Fill-in design-doc template |
| `system-design/scripts/estimate.py` | Back-of-the-envelope CLI (qps / storage / shards / bandwidth / full) |
| `system-design/scripts/gen_flashcards.py` | Flashcard generator: built-in decks + extracted primer Anki decks (markdown / Anki TSV / JSON) |
| `system-design/scripts/validate_skill.py` | Package validator (frontmatter, internal refs, zip parity) |
| `system-design.skill` | Distributable package (zip) of the skill folder |
| `../.claude/commands/system-design.md` | Claude Code `/system-design` slash-command stub → routes into the skill |

### Changelog

- **5.0.0** — full-repo learning pass: distilled all 8 system design solutions + all 6 OOD solutions into the package; extracted primer Anki decks to `data/anki_cards.json` (wireable via `--deck anki*`); company blogs/architectures + stretch topics reference; standard "Additional talking points" output section; RPC vs REST table + security basics completed in playbook
- **4.0.0** — bundled worked exemplar (Pastebin condensed); mermaid diagram snippet library; `gen_flashcards.py`; `/system-design` slash-command stub
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

**Study drill decks** (standalone):

```bash
python3 skills/system-design/scripts/gen_flashcards.py --deck anki --format tsv --out anki.tsv   # primer's 56 extracted cards
python3 skills/system-design/scripts/gen_flashcards.py --deck all --format markdown              # built-in + primer cards
```

## Validate & rebuild the package

```bash
# after any edit:
python3 skills/system-design/scripts/validate_skill.py
(cd skills && rm -f system-design.skill && zip -r system-design.skill system-design -x '*.DS_Store')
python3 skills/system-design/scripts/validate_skill.py   # confirms zip ↔ directory parity
```
