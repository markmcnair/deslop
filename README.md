# deslop

Deterministic AI writing pattern removal for Claude Code.

Most "humanizer" skills tell the model to "watch for" AI patterns. The model skims, does a surface pass, and claims it's done. deslop doesn't ask. It forces a mandatory 6-step pipeline with scoring gates, binary checklists, and zero-tolerance rules. Every sentence gets checked against every rule. Every run shows proof of work.

## Why this exists

The built-in humanizer skill and similar tools fail because their processes are advisory, not mandatory. In real usage, the model:

- Skips steps (admitted to skipping 4 of 9 process steps)
- Does "surface passes" instead of line-by-line analysis
- Flags patterns like em dashes in the audit, then leaves them in the output
- Claims completion on unfinished work

deslop fixes this by replacing "watch for" language with "ZERO allowed" rules, adding quantifiable gates, and requiring the model to show its work.

## What it catches

- **79 banned vocabulary words** across 3 tiers (always replace, context-dependent, density flags)
- **100+ banned phrases** across 10 categories (throat-clearing, filler, performative candor, sycophantic artifacts, business jargon, etc.)
- **20 structural pattern bans** (em dashes, rule of three, anaphora, binary contrasts, false agency, passive voice, etc.)
- **12 before/after examples** for calibration

## The pipeline

Six mandatory steps. No skipping. Must show work.

1. **SCAN** — Process every sentence against all ban lists. Output pattern counts with specific instances.
2. **REWRITE** — Apply all fixes. Zero-tolerance enforcement on em dashes, adverbs, emojis, bold, title case.
3. **SOUL CHECK** — Score across 5 dimensions (rhythm, voice, density, authenticity, directness). Must pass 35/50 gate.
4. **ADVERSARIAL AUDIT** — "What makes this obviously AI?" List remaining tells with line references.
5. **FINAL REWRITE** — Fix audit findings. Run 12-item binary checklist. All must pass.
6. **OUTPUT** — Present final text with scan count, score, and checklist as proof of work.

## Install

### Claude Code

```bash
claude mcp add-skill ~/.claude/skills/deslop
```

Or copy the files manually:

```bash
git clone https://github.com/markmcnair/deslop.git ~/.claude/skills/deslop
```

### Manual / Other agents

Copy `SKILL.md` and the `references/` directory into your agent's skill or knowledge folder.

## Usage

Give it text to process:

```
deslop this: [your text here]
```

### Modes

- **Full pipeline** (default): All 6 steps with scoring and checklists
- **Quick mode** (`quick deslop`): Scan, rewrite, checklist. Skips scoring and adversarial audit. For text under 3 sentences.
- **Detect mode** (`deslop check`): Scan only. Shows pattern counts without rewriting.

## Zero-tolerance rules

These are hard bans, not suggestions:

| Pattern | Tolerance |
|---|---|
| Em dashes (—) | Zero. Commas or periods. |
| Adverbs (-ly) | Zero. Stronger verb or cut. |
| Emojis | Zero. |
| Curly quotes | Zero. Straight quotes only. |
| Bold in body text | Zero. Headings only. |
| Title case headings | Zero. Sentence case. |
| "Serves as" / "stands as" | Zero. Use "is". |
| Performative candor | Zero. Just be direct. |

## Built from

This skill merges the best parts of several approaches:

- Pattern catalog depth from [avoid-ai-writing](https://github.com/conorbronsdon/avoid-ai-writing) (36 patterns)
- Scoring system and zero-tolerance rules from [stop-slop](https://github.com/hardikpandya/stop-slop)
- "Add Soul" methodology from [blader/humanizer](https://github.com/blader/humanizer)
- All rooted in Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide

## File structure

```
deslop/
  SKILL.md              — Process pipeline and rules
  references/
    vocabulary.md       — Tiered word ban list (79 Tier 1 + 20 Tier 2 + 15 Tier 3)
    phrases.md          — Banned phrases by category (100+)
    structures.md       — Structural pattern bans (20)
    examples.md         — Before/after transformations (12)
```

## License

MIT
