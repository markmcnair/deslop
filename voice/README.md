# Voice layer

deslop removes AI tells. That gets you clean text, not your text. The voice layer closes the gap: build a profile of how you write once, and the rewrite and soul check steps will match it every time.

Your profile and your samples stay on your machine. `.gitignore` excludes `voice/voice-profile.md` and `voice/samples/`, so neither gets committed. Only the blank template lives in this repo.

## How it works

1. Collect a corpus of your own writing.
2. Study it once and distill it into `voice/voice-profile.md`.
3. deslop reads the profile whenever it exists and matches it during Step 2 (rewrite) and Step 3 (soul check).

No profile, no problem. deslop falls back to its default rules.

## Step 1: Collect samples

Aim for 150 or more messages you wrote yourself. More is better, and variety matters more than volume.

- Sent email from every account you use (work and personal)
- Slack or Teams messages
- Texts, if you can export them
- Anything long you wrote without help: posts, docs, proposals

Keep only your own words. Strip quoted replies, signatures, forwarded content, auto-generated mail, and calendar invites. Note who each message went to (client, vendor, team, friend or family) because the profile needs to show how you change by audience.

Save the raw samples in `voice/samples/` (for example `voice/samples/emails.jsonl` with fields for account, date, recipient type, and body). That folder is git-ignored.

## Step 2: Distill the profile

Give your agent the samples and this instruction:

```
Read every sample in voice/samples/. Fill in voice/voice-profile.template.md
and save it as voice/voice-profile.md. Base every claim on evidence: give real
frequencies ("signs off with X in 88 of 150 messages") and quote real phrases.
Do not invent traits. Note where the sample is thin.
```

A good profile covers:

- **Sentence length.** Typical words per sentence and per message. How often you send one-liners.
- **Greetings and sign-offs.** What you open and close with, and how often, by audience.
- **Punctuation habits.** Exclamation points, dashes, ellipses, semicolons, all caps, emoji, "lol".
- **Recurring phrases.** The handful of phrases you use over and over.
- **Formality by audience.** How you write to clients, vendors, your team, and friends or family.
- **Things you never do.** Just as useful as what you do.
- **About 15 short example lines** in your real voice, covering a range of audiences.

Keep it under two pages. The agent reads it on every run.

## Step 3: Keep it current

Re-run the study every six months or after a big change in your work. Voices drift.

## Privacy

- Never commit `voice/voice-profile.md` or anything in `voice/samples/`.
- Review your profile before sharing it. The example lines can include names and details.
- If you fork this repo publicly, check `git status` before every push.
