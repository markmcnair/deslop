# Changelog

All notable changes to deslop. Dates are YYYY-MM-DD.

## 1.1.0 (2026-10-20)

### Added
- Voice layer. `voice/README.md` explains how to build a personal voice profile from your own writing. `voice/voice-profile.template.md` is a blank template. The rewrite and soul check steps read `voice/voice-profile.md` when it exists and match it.
- `.gitignore` entries for `voice/voice-profile.md` and `voice/samples/` so private writing never gets committed.
- Audit mode ("deslop audit") that shows the full proof of work.
- Message mode for emails, Slack, and texts.
- Email and message tells in phrases.md (openers, closers, over-thanking, filler) and structures.md patterns 21 to 26 (bulleted recaps, bold headers in short emails, the same three-part reply, recap closing paragraphs, formal register in casual channels, restated questions).
- Allowed -ly whitelist in vocabulary.md.
- Email reply and audience scaling examples in examples.md.
- Self-flagging: the agent notes recurring tells it catches that aren't listed yet, as suggested additions at the end of its output.
- A quarterly review of the lists.

### Changed
- Quiet by default. The agent runs every step internally and outputs only the final text and a one-line summary of changes.
- The soul check scales looseness to the audience and channel. Professional writing stays clean and direct. "Let some mess in" now applies only to casual registers.
- The fifth soul dimension is now Fit (register matches the audience) instead of Directness, which moved under Density and Authenticity.
- -ly adverbs are allowed when whitelisted and used sparingly. Intensifiers stay banned.
- Passive voice is allowed when the actor is unknown or doesn't matter.
- Checklist items updated to match.

### Unchanged
- Hard zeros on em dashes, emojis, and curly quotes.

## 1.0.0

- Initial release: six-step pipeline, scoring gates, 12-item checklist, vocabulary, phrase, and structure ban lists, and before/after examples.
