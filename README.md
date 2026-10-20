# deslop

Deterministic AI writing pattern removal for Claude Code.

Most "humanizer" skills tell the model to "watch for" AI patterns. The model skims, does a surface pass, and claims it's done. deslop doesn't ask. It forces a mandatory 6-step pipeline with scoring gates, binary checklists, and hard zeros. Every sentence gets checked against every rule.

Version 1.1 adds three things on top: it runs quietly, it can learn your voice, and it adjusts to who you're writing to.

## Why this exists

The built-in humanizer skill and similar tools fail because their processes are advisory, not mandatory. In real usage, the model:

- Skips steps (admitted to skipping 4 of 9 process steps)
- Does "surface passes" instead of line-by-line analysis
- Flags patterns like em dashes in the audit, then leaves them in the output
- Claims completion on unfinished work

deslop fixes this with required steps, quantifiable gates, and a checklist that must fully pass. Clean text still isn't enough, though. It has to sound like you, at the right level of formality for the reader.

## What's new in 1.1

- **Quiet by default.** deslop does the scan, scoring, audit, and checklist internally, then shows you the final text and a one-line summary. Say "deslop audit" to see all the work.
- **Voice profiles.** Build a private profile of how you write and deslop will match it. See [voice/README.md](voice/README.md).
- **Audience scaling.** A note to your accountant comes out clean and direct. A text to a friend comes out loose. No forced casualness in professional writing.
- **Message mode.** Catches email, Slack, and text tells: "I hope this finds you well", "Just wanted to", "Happy to help with anything", over-thanking, bulleted recaps of simple things, bold headers in short emails, and recap closing paragraphs.
- **Whitelist instead of blanket bans.** Purposeful -ly words (only, likely, early, nearly) and passive voice with an unknown actor are allowed. Em dashes, emojis, and curly quotes are still zero.
- **Self-flagging.** When deslop catches a recurring tell that isn't on a list yet, it suggests adding it.

See [CHANGELOG.md](CHANGELOG.md) for details.

## What it catches

- **Banned vocabulary** across 3 tiers (always replace, context-dependent, density flags), plus a whitelist of -ly words that are fine in moderation
- **100+ banned phrases** across 11 categories, including email and message tells
- **26 structural patterns** (rule of three, anaphora, binary contrasts, false agency, bulleted recaps, bold headers in short emails, and more)
- **Before/after examples** for calibration, including an email reply and audience scaling

## The pipeline

Six mandatory steps. In the default mode they run silently. In audit mode you see each one.

1. **Scan.** Check every sentence against all lists and count the patterns.
2. **Rewrite.** Fix everything flagged. Match your voice profile if you have one.
3. **Soul check.** Score rhythm, voice, density, authenticity, and fit for the audience. Must reach 35/50.
4. **Adversarial audit.** "What makes this obviously AI?" and "Would the sender actually write this?"
5. **Final rewrite.** Fix what the audit found. Run the 12-item checklist. All items must pass.
6. **Output.** The final text and a one-line summary, or the full proof of work in audit mode.

## Install

### Claude Code

```bash
git clone https://github.com/markmcnair/deslop.git ~/.claude/skills/deslop
```

### Manual / other agents

Copy `SKILL.md`, the `references/` directory, and the `voice/` directory into your agent's skill or knowledge folder.

## Usage

```
deslop this: [your text here]
```

### Modes

| Trigger | Mode | What you get |
|---|---|---|
| `deslop this` | Quiet (default) | Final text and a one-line summary of changes |
| `deslop audit` | Audit | Scan counts, scores, audit, checklist, and the final text |
| `deslop email`, `deslop message`, or any email, Slack, or text input | Message | Email and message tells removed, answer first, no headers or bold |
| `quick deslop` | Quick | Scan, rewrite, checklist. For text under 3 sentences |
| `deslop check` | Detect | Pattern counts only, no rewrite |

Message mode combines with quiet or audit mode.

## Your voice

deslop can match the way you write. Collect your own sent emails and messages, have your agent distill them into `voice/voice-profile.md` using the template, and deslop will read it on every run.

Your profile and samples are listed in `.gitignore`. They never leave your machine through this repo. Full instructions are in [voice/README.md](voice/README.md).

## Rules at a glance

| Pattern | Rule |
|---|---|
| Em dashes | Zero. Commas or periods. |
| Emojis | Zero. |
| Curly quotes | Zero. Straight quotes only. |
| Adverbs (-ly) | Intensifiers banned. Whitelisted words allowed, one per paragraph at most in formal writing. |
| Passive voice | Fine when the actor is unknown or irrelevant. Rewrite when it hides a known actor. |
| Bold in body text | None. Headings only, and never in short emails. |
| Title case headings | None. Sentence case. |
| "Serves as" / "stands as" | Use "is". |
| Performative candor | Cut. Be direct. |
| Casual asides | Only in casual registers. Never forced into professional writing. |

## Keeping the lists current

deslop flags new tells it keeps seeing as suggested additions at the end of its output. Review the lists about once a quarter: add what keeps coming up, remove anything causing false positives, and note it in the changelog.

## Built from

- Pattern catalog depth from [avoid-ai-writing](https://github.com/conorbronsdon/avoid-ai-writing)
- Scoring system and zero-tolerance rules from [stop-slop](https://github.com/hardikpandya/stop-slop)
- "Add soul" methodology from [blader/humanizer](https://github.com/blader/humanizer)
- All rooted in Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide

## File structure

```
deslop/
  SKILL.md                         Process pipeline and rules
  CHANGELOG.md                     Version history
  references/
    vocabulary.md                  Tiered word ban list and -ly whitelist
    phrases.md                     Banned phrases, including email and message tells
    structures.md                  Structural patterns (26)
    examples.md                    Before/after transformations
  voice/
    README.md                      How to build a voice profile
    voice-profile.template.md      Blank template
    voice-profile.md               Your profile (git-ignored, you create it)
    samples/                       Your raw samples (git-ignored)
```

## License

MIT
