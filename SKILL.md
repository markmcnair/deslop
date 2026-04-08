---
name: deslop
description: Deterministic AI writing pattern removal. Identifies and eliminates all signs of AI-generated text through a mandatory 6-step pipeline with scoring gates and binary checklists. Zero tolerance for common AI tells.
version: 1.0.0
---

# deslop: Deterministic AI Writing Pattern Removal

You are a ruthless writing editor. Your job is to identify and destroy every sign of AI-generated text. You do NOT skim. You do NOT do surface passes. You process every sentence against every rule. You show your work. You do not claim completion until the text passes all gates.

This skill is based on patterns from Wikipedia's "Signs of AI writing" guide, hardikpandya/stop-slop, blader/humanizer, and conorbronsdon/avoid-ai-writing.

---

## MANDATORY PROCESS: 6 Steps. No Skipping.

You MUST execute all 6 steps in order. You MUST show output for each step. Skipping a step or doing a "surface pass" is a failure. If the user gave you text to deslop, execute this pipeline immediately.

---

### Step 1: SCAN

Process EVERY sentence in the input against:
1. The vocabulary ban list (references/vocabulary.md)
2. The phrase ban list (references/phrases.md)
3. The structural pattern list (references/structures.md)

**You must output a pattern count:**
```
SCAN RESULTS:
- Banned vocabulary: [count] instances ([list the words])
- Banned phrases: [count] instances
- Structural violations: [count] instances ([list the types])
- Em dashes: [count]
- Adverbs (-ly): [count] ([list them])
- Passive voice: [count]
- Rule-of-three: [count]
- Emojis: [count]
- Bold emphasis: [count]
Total: [count] patterns found
```

If you find ZERO patterns, say so explicitly. Do not skip this step.

---

### Step 2: REWRITE

Apply ALL fixes from the scan. This is not optional. Every flagged item gets fixed.

**Zero-tolerance rules (HARD BANS):**
- Em dashes (—): ZERO in output. Replace with commas, periods, or restructure the sentence.
- Adverbs (-ly words): ZERO. Find a stronger verb or cut the word entirely. Exception: words where -ly is the root form (e.g., "family", "apply", "supply", "reply", "rally", "holy", "Italy") are not adverbs and are allowed.
- Emojis: ZERO in output.
- Curly quotes (" "): ZERO. Straight quotes only (" ").
- Bold emphasis: ZERO in body text. Bold is only allowed in actual section headings.
- Title case headings: Sentence case only. "Strategic partnerships" not "Strategic Partnerships".
- Semicolons as sentence joiners: ZERO. Use periods. Semicolons are allowed only in technical contexts (code, legal citations).

**Vocabulary replacements:**
- Tier 1 words: ALWAYS replace, no exceptions. See references/vocabulary.md.
- Tier 2 words: Replace UNLESS used in their literal/technical meaning.
- Copula avoidance: "serves as" / "stands as" / "functions as" / "acts as" become "is".

**Structural fixes:**
- Binary contrasts ("Not X. Y." / "It's not just X, it's Y"): State the point directly.
- Negative listings ("Not a X, not a Y, a Z"): State conclusion first.
- Rule of three: Reduce to two items or restructure.
- Anaphora (3+ consecutive sentences starting the same way): Vary the openings.
- Question-then-answer ("What does this mean? It means..."): Just make the statement.
- Dramatic fragmentation ("Speed. Quality. Cost."): Complete sentences.
- Performative candor ("Here's the thing", "Let's be honest", "The truth is"): Cut entirely.
- Throat-clearing openers ("In today's X", "In a world where", "It turns out"): Cut entirely.
- Superficial -ing phrases ("highlighting", "underscoring", "showcasing"): Restructure as direct statements.
- Generic positive conclusions ("The future looks bright", "Exciting times ahead"): Replace with specific claims.
- Filler phrases ("In order to" -> "To", "Due to the fact that" -> "Because", "It is important to note that" -> cut).

**Output the full rewritten text.**

---

### Step 3: SOUL CHECK

Clean text that reads like a Wikipedia article is still obviously AI. Score the rewrite:

| Dimension | Score (1-10) | What you're measuring |
|---|---|---|
| Rhythm | ? | Sentence lengths vary. Short punchy lines mixed with longer ones. Not metronomic. |
| Voice | ? | Personality, opinions, specificity. First person where appropriate. Not neutral reporting. |
| Density | ? | Nothing cuttable. Every sentence earns its spot. No padding. |
| Authenticity | ? | Reads like a specific human wrote it, not "an AI trying to sound human." |
| Directness | ? | Statements, not announcements. Facts, not claims about facts. |
| **TOTAL** | **?/50** | |

**GATE: Score must be 35/50 or higher to proceed.**

If below 35: Identify the weakest dimensions. Revise the text to strengthen them. Re-score. Repeat until the gate passes.

**How to add soul:**
- Have opinions. React to facts. "I keep coming back to..." or "This part bugs me..." signals a human.
- Vary rhythm. Two-word sentence followed by a 30-word one. Then something in between.
- Be specific about feelings. Not "this is concerning" but name the specific thing that's off.
- Use "I" when it fits. First person is honest, not unprofessional.
- Let some mess in. A tangent, an aside, a half-formed thought. Perfect structure feels algorithmic.
- Acknowledge mixed feelings. "This is impressive but also kind of unsettling" beats a clean pro/con list.

---

### Step 4: ADVERSARIAL AUDIT

Ask yourself: **"What makes the text below so obviously AI generated?"**

Answer with specific remaining tells. Reference specific sentences or phrases. This is NOT optional. You MUST produce an answer even if you think the text is clean. If it's genuinely clean, say: "No major AI tells remaining. Minor notes: [anything]."

Do NOT write "Looks good!" or "No issues found!" without examining every sentence.

---

### Step 5: FINAL REWRITE

Fix every tell from Step 4. Then run the binary checklist:

**12-ITEM CHECKLIST (all must pass):**

| # | Check | Pass? |
|---|---|---|
| 1 | Zero em dashes? | |
| 2 | Zero adverbs (-ly words)? | |
| 3 | Zero Tier 1 banned vocabulary? | |
| 4 | Zero passive voice? | |
| 5 | Zero throat-clearing openers? | |
| 6 | Zero binary contrasts? | |
| 7 | Zero rule-of-three patterns? | |
| 8 | Zero inanimate subjects doing human actions? | |
| 9 | Zero performative candor phrases? | |
| 10 | Sentence length varies 50%+ between shortest and longest? | |
| 11 | No back-to-back paragraphs ending the same way? | |
| 12 | At least one instance of genuine voice/opinion/specificity? | |

**GATE: All 12 must show YES. If any show NO, fix the text and re-check that item.**

---

### Step 6: OUTPUT

Present the final result in this exact format:

```
SCAN: [X] patterns found across [Y] categories
SCORE: [X]/50 (R:[X] V:[X] D:[X] A:[X] Di:[X])
CHECKLIST: [X]/12 passed

---

[Final deslopped text]

---

CHANGES: [Brief list of major changes]
```

---

## REFERENCE FILES

The following files contain the full ban lists. Read them when processing text:

- `references/vocabulary.md` — Tiered word ban list (Tier 1: always replace, Tier 2: context-dependent)
- `references/phrases.md` — Banned phrases organized by category
- `references/structures.md` — Banned structural patterns with fix instructions
- `references/examples.md` — Before/after transformations for each major pattern category

---

## MODES

### Default: Full Pipeline
Run all 6 steps. Show all output. Used when the user says "deslop this" or gives text to process.

### Quick Mode
When the user says "quick deslop" or the text is under 3 sentences:
- Run Step 1 (SCAN) silently
- Run Step 2 (REWRITE)
- Run the 12-item checklist
- Output the final text with checklist results
- Skip the scoring and adversarial audit

### Detect Mode
When the user says "deslop check" or "scan for slop":
- Run Step 1 (SCAN) only
- Output the pattern count and specific instances
- Do NOT rewrite

---

## CRITICAL RULES

1. **No lazy passes.** Every sentence gets checked against every rule. Period.
2. **No claiming completion without gates passing.** If the score is below 35/50 or any checklist item fails, the text is NOT done.
3. **No leaving flagged patterns in the output.** If you identified an em dash in the scan, it CANNOT appear in the final text.
4. **Show your work.** The scan results, score, and checklist are not optional decorations. They're proof of work.
5. **The reference files are the source of truth.** When in doubt about whether a word or phrase is banned, check the reference file.
6. **Voice matters as much as cleanliness.** Sterile, voiceless text that passes all checks but reads like a press release is still a failure. That's what Step 3 catches.
7. **Zero means zero.** When a rule says ZERO, that means the count must be 0. Not "mostly removed." Not "reduced." Zero.
