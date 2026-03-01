# AI Language Pattern Detection

Scan your prose for AI-specific language patterns and get concrete replacement suggestions.

## Overview

This workflow helps you identify and remove common AI language patterns from your writing, ensuring your prose maintains an authentic human voice. It scans for 10 specific pattern types (from overused words like "delve" to purple prose excess) and provides 3-5 concrete replacement options for every match.

**Time:** 5-15 minutes (depending on text volume)
**Output:** AI-DETECTION-REPORT.md in your story project
**When to use:** After generating chapters, during revision, or on any prose you want to check

## How It Works

The system loads a pattern database (10 built-in patterns + your custom additions), scans your text, flags every match with context, and generates a detailed report showing where AI patterns appear and how to replace them.

## The Workflow

### Step 1: Validate Story Project

I'll check that you're in a valid story project by reading `PROJECT.md` from `stories/{slug}/`.

If you're checking prose outside a project, you can paste text directly (Option C in Step 2).

### Step 2: Choose Detection Scope

I'll ask what you want to scan:

**Option A: Single Chapter**
- Enter chapter number (e.g., "3" for chapter-03.md)
- Scans only that chapter
- Fast, focused check

**Option B: All Chapters**
- Scans every chapter in `chapters/` directory
- Comprehensive story-wide analysis
- Shows patterns across your entire draft

**Option C: Specific Text**
- Paste prose directly (no file required)
- One-time scan for testing or non-project text
- Great for checking before you save

### Step 3: Load Pattern Database

I'll load the AI pattern definitions:

**Default source:** `.planning/templates/ai-patterns.md` (10 built-in patterns + custom section)

**Project-specific override:** If `stories/{slug}/AI-PATTERNS.md` exists, I'll use that instead. This lets you customize patterns per-story or add project-specific phrases to watch for.

**Patterns loaded:**
1. Delve/Delved/Delving
2. Tapestry (metaphorical)
3. Navigate/Navigated (metaphorical)
4. Testament to
5. Juxtaposition
6. Overly formal academic language (multiple sub-patterns)
7. "It's worth noting" phrases (multiple sub-patterns)
8. Purple prose patterns (multiple sub-patterns)
9. *(Concrete replacements for all patterns)*
10. Custom patterns (from `custom_patterns` YAML section)

### Step 4: Scan Prose for Patterns

I'll scan your text looking for each pattern:

**Pattern 1-5, 7:** Simple keyword/phrase matching
- Case-insensitive
- Word boundary detection (won't match "delve" inside "undelved")
- Full-word matches only

**Pattern 6:** Multi-pattern check (academic language)
- Scans for: "Furthermore," "Moreover," "Additionally," "Nevertheless," etc.
- Checks for: "One might observe," "It can be seen that," etc.
- Flags: Latin phrases (per se, vis-à-vis)
- Flags: Archaic formal words (aforementioned, heretofore)

**Pattern 8:** Complex pattern detection (purple prose)
- Adjective stacking: 3+ adjectives before a noun
- Melodramatic adverbs: ineffably, unutterably, indescribably, etc.
- Overwrought metaphor keywords (when overused)
- Pretentious vocabulary in place of simple words
- Enhanced dialogue tags (breathed, purred, intoned - when overused)

**Custom Patterns:** Keyword matching from your `custom_patterns` YAML list

### Step 5: Record Matches

For each pattern match found, I record:
- **Location:** Chapter number, approximate paragraph or line number
- **Matched text:** The flagged phrase with surrounding context (full sentence)
- **Pattern info:** Category and why it's AI-ish
- **Replacement suggestions:** 3-5 concrete alternatives from pattern database

### Step 6: Generate Detection Report

I create a comprehensive report at `stories/{slug}/AI-DETECTION-REPORT.md`:

```markdown
# AI Pattern Detection Report

**Story:** {Story Title}
**Scanned:** {Single chapter / All chapters / Pasted text}
**Run Date:** {Timestamp}
**Patterns found:** {Total count}

---

## Summary

**Total flags:** {N}
**Most common pattern:** {Pattern name} ({count} instances)
**Chapters affected:** {List of chapter numbers}

**Pattern breakdown:**
- Pattern 1 (Delve): {count} instances
- Pattern 2 (Tapestry): {count} instances
- Pattern 6 (Formal Language): {count} instances
- ...

---

## Findings by Pattern

### Pattern 1: Delve/Delved/Delving ({X} instances)

**Chapter 2, paragraph 5:**
> "She delved into the mystery surrounding the murder, uncovering clues that had been hidden for years."

**Why flagged:** Overly common in AI-generated text, rarely used in natural contemporary prose

**Suggestions:**
- "She investigated the mystery surrounding the murder..."
- "She dug into the mystery surrounding the murder..."
- "She explored the mystery surrounding the murder..."
- Simply: "She looked into the murder, finding hidden clues."

---

**Chapter 5, paragraph 12:**
> "He delved deeper into the ancient texts."

**Why flagged:** Overly common in AI-generated text, rarely used in natural contemporary prose

**Suggestions:**
- "He studied the ancient texts more closely."
- "He examined the ancient texts in detail."
- "He pored over the ancient texts."

---

### Pattern 2: Tapestry ({X} instances)

**Chapter 3, paragraph 8:**
> "The city was a tapestry of cultures and traditions."

**Why flagged:** AI loves "tapestry" for any complex interconnection

**Suggestions:**
- "The city mixed dozens of cultures and traditions."
- "The city was a blend of cultures and traditions."
- Be specific: "Korean shops next to Mexican restaurants next to Russian bakeries."
- Simply: "Every culture lived in that city."

---

### Pattern 6: Overly Formal Academic Language ({X} instances)

**Chapter 1, paragraph 3:**
> "Moreover, one might observe that the protagonist's behavior was, per se, indicative of her determination."

**Why flagged:** Academic formality doesn't fit creative narrative prose

**Suggestions:**
- "And her behavior showed determination."
- "Her actions proved she was determined."
- Simply: "She kept going. Stubborn as hell."

---

**Chapter 4, paragraph 15:**
> "Furthermore, the aforementioned evidence suggested a clear pattern."

**Why flagged:** Overly formal; "Furthermore" and "aforementioned" are academic markers

**Suggestions:**
- "And the evidence showed a clear pattern."
- "The earlier evidence pointed to a pattern."
- Simply: "The pattern was obvious."

---

### Pattern 8: Purple Prose ({X} instances)

**Chapter 6, paragraph 2:**
> "The dark, cold, forbidding, menacing castle loomed before them."

**Why flagged:** Adjective stacking (4 adjectives) - excessive

**Suggestions:**
- Pick strongest one: "The forbidding castle loomed before them."
- Combine: "The dark castle loomed, menacing."
- Show through action: "The castle loomed. They stopped. None of them wanted to go in."

---

**Chapter 7, paragraph 19:**
> "She was ineffably, unutterably sad."

**Why flagged:** Melodramatic adverbs add no value

**Suggestions:**
- "She was devastated."
- "She was heartbroken."
- Show it: "She couldn't stop crying."
- Show it: "She sat there. Empty. Nothing left."

---

## Next Steps

1. **Review flagged passages in context**
   - Not all instances need changing
   - Some patterns might fit your genre or style
   - Trust your judgment

2. **Consider your STYLE.md preferences**
   - Formal style might keep some academic language
   - Sparse style might already avoid purple prose
   - Your voice guide helps choose replacements

3. **Make changes selectively**
   - Fix obvious AI-isms (delve, tapestry, testament to)
   - Evaluate context-dependent patterns (formal language okay in academic character's POV)
   - Keep what works for your voice

4. **Re-run detection after revisions**
   - Run `/write:detect` again to verify cleanup
   - Track improvement over multiple drafts

5. **Add custom patterns**
   - Notice words YOU personally overuse
   - Add to custom_patterns in AI-PATTERNS.md
   - Future scans will catch them

---

**Report saved:** `stories/{slug}/AI-DETECTION-REPORT-{timestamp}.md`

To create a project-specific pattern database: Run this command again and select "Yes" when offered.
```

### Step 7: Offer Project-Specific Pattern Database

After generating the report, I'll ask:

> "Would you like to create a project-specific AI-PATTERNS.md file?"
>
> This copies the template to `stories/{slug}/AI-PATTERNS.md`, allowing you to:
> - Customize pattern definitions for this story
> - Add more custom phrases you overuse
> - Adjust replacements to match your style
>
> Future detections for this story will use the project copy instead of the global template.

If you say yes:
- Copy `.planning/templates/ai-patterns.md` to `stories/{slug}/AI-PATTERNS.md`
- Future `/write:detect` runs in this project will read from project file
- You can edit freely without affecting the global template

### Step 8: Display Summary

I'll show you quick stats:

```
╔══════════════════════════════════════════╗
║  AI PATTERN DETECTION COMPLETE           ║
╚══════════════════════════════════════════╝

Story: [Title]
Scanned: [Scope]
Total flags: [N]
Most common: [Pattern] ([count] times)

Report: stories/{slug}/AI-DETECTION-REPORT-{timestamp}.md

Next: Review flagged passages and make selective changes.
```

## Pattern Scanning Details

### Pattern 1-5: Simple Keywords

**Delve/Delved/Delving:**
- Regex: `\b(delve|delves|delved|delving)\b` (case-insensitive)
- Matches: "delve into the mystery" ✓
- Ignores: "undelved territory" (word boundary)

**Tapestry:**
- Regex: `\btapestry\b` (case-insensitive, metaphorical context)
- Matches: "a tapestry of cultures" ✓
- Note: Literal tapestries (fabric) might false-positive - review in context

**Navigate:**
- Regex: `\b(navigate|navigates|navigated|navigating)\b` (case-insensitive, non-literal)
- Matches: "navigate the complex situation" ✓
- May false-positive on actual navigation ("navigate the streets") - review context

**Testament to:**
- Regex: `\ba testament to\b` (case-insensitive)
- Matches: "a testament to her skill" ✓

**Juxtaposition:**
- Regex: `\bjuxtaposition\b` (case-insensitive)
- Matches: "the juxtaposition of wealth and poverty" ✓

### Pattern 6: Formal Academic Language

Scans for multiple sub-patterns:
- Sentence starters: Furthermore, Moreover, Additionally, Nevertheless, Consequently, Hence, Thus, Therefore
- Academic hedging: "one might observe," "it can be seen that," "it should be noted," "it is worth noting"
- Latin phrases: per se, vis-à-vis, de facto, ipso facto, ergo
- Archaic: aforementioned, heretofore, wherein, whereby, therein

Each match flagged separately with location.

### Pattern 7: "Worth Noting" Phrases

Scans for:
- "it's worth noting that" / "it is worth noting that"
- "it should be noted that"
- "notably,"
- "of note,"
- "interestingly,"
- "it is interesting to note"

### Pattern 8: Purple Prose

More complex detection:

**Adjective stacking:**
- Count adjectives before nouns
- Flag if 3+ adjectives in a row ("the dark, cold, forbidding, ancient castle")

**Melodramatic adverbs:**
- List: ineffably, unutterably, indescribably, impossibly, unbearably, infinitely, eternally (when modifying emotions)

**Pretentious vocabulary:**
- Detect: domicile (vs house), masticate (vs chew), utilize (vs use), commence (vs start), terminate (vs end)

**Enhanced dialogue tags (if frequent):**
- Track: breathed, purred, intoned, murmured huskily, whispered seductively
- Flag if used in >30% of dialogue tags (some is fine, but overuse is AI-ish)

### Pattern 10: Custom Patterns

Load from YAML:
```yaml
custom_patterns:
  - phrase: "suddenly"
    reason: "Overused"
    alternatives: [...]
```

Simple keyword match on each `phrase` entry.

## Notes

- **Detection is awareness, not prescription** — you decide what to change
- **Some false positives are normal** — review in context before changing
- **Genre matters** — literary fiction vs thriller have different tolerances
- **STYLE.md integration** — use your style profile to guide replacement choices
- **Iterative process** — run after each draft to track improvement
- **Custom patterns** — add your personal overuse words as you notice them

## Common Questions

**Q: Will this catch EVERY AI pattern?**
A: No—these are 10 common patterns. There are more subtle AI-isms, but these are the most flagrant.

**Q: Should I change every flagged instance?**
A: No. Review in context. Some might fit your voice or genre. The goal is awareness.

**Q: Can I add more built-in patterns?**
A: Edit `.planning/templates/ai-patterns.md` (global) or create project-specific `AI-PATTERNS.md` and add patterns there.

**Q: What if I'm using "delve" intentionally in fantasy genre?**
A: Keep it if it fits your world/voice. Detection raises awareness; you make the final call.

**Q: How do I know which replacement to use?**
A: Check your STYLE.md (if you have one) for tone/formality guidance. Pick the option that fits your voice.

**Q: Can I scan non-chapter text?**
A: Yes—Option C lets you paste any text for one-time scanning.

**Q: Does this work on YOLO vs In-Depth mode stories?**
A: Yes, works on any story project regardless of planning mode.

---

Ready? Let's scan for AI patterns.

## Usage

In your story project directory:
```
/write:detect
```

I'll ask for scope (chapter, all chapters, or paste text), scan for all 10 pattern types plus custom patterns, and generate a detailed report with location, context, and concrete replacement suggestions for every match.
