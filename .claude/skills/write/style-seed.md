# Style Seeding Workflow

Define your writing style through sample analysis and voice configuration.

## Overview

This workflow helps you capture your unique writing voice so that generated chapters match your personal style rather than sounding like generic AI output.

**Time:** 10-15 minutes
**Output:** STYLE.md profile in your story project
**When to use:** After project initialization, before writing chapters

## How It Works

We'll analyze sample paragraphs of your writing to identify measurable patterns (sentence length, vocabulary, tone), then combine that with your explicit voice preferences (POV, tense, formality) to create a style profile that guides chapter generation.

## The Workflow

### Step 1: Validate Story Project

First, I'll check that you're in a valid story project by reading `PROJECT.md` from `stories/{slug}/`.

If you haven't initialized a project yet, run `/write:init` first.

### Step 2: Collect Writing Samples

I'll ask you to provide 2-3 sample paragraphs that represent the style you want for this story.

**What makes a good sample:**
- **Your own writing** (not quotes from published works - we want YOUR voice)
- **Recent work** you're proud of (represents your current style)
- **Similar genre/tone** to this story (literary fiction samples for a thriller won't help)
- **At least 100-150 words total** across the paragraphs (more data = better analysis)

**Examples:**

*Good sample (literary fiction):*
> The house remembered her footsteps. Not the way houses in ghost stories remember—with creaking floorboards and groaning timbers—but quietly, in the way dust settles differently in walked-upon rooms. She'd been gone three years. The dust had forgotten her by now, or learned new patterns in her absence.

*Good sample (thriller):*
> Martinez hit the stairwell at a dead run. Two floors down, maybe three. The shooter would expect the elevator. Everyone expected the elevator. She took the steps three at a time, one hand on the rail, the other keeping her Glock steady. Footsteps echoed above her—too close, too fast.

*Not helpful (too short):*
> She walked into the room.

*Not helpful (not your voice):*
> "It was the best of times, it was the worst of times..." [Dickens quote]

### Step 3: Analyze Samples for Patterns

I'll analyze your samples for these quantifiable patterns:

**Sentence Length:**
- Average words per sentence (e.g., 12 words, 18 words, 25 words)
- Variety (Do you mix short punchy sentences with longer flowing ones? Or maintain consistency?)
- Rhythm patterns (e.g., "short-short-long" patterns, "long-medium-short" patterns)

**Vocabulary Level:**
- Simple: common words, direct language ("walked," "house," "night")
- Moderate: varied vocabulary with some literary choices ("strode," "dwelling," "twilight")
- Literary: rich vocabulary, layered meaning ("sauntered," "domicile," "gloaming")

**Tone Markers:**
- Formal vs. Casual (academic distance vs. conversational intimacy)
- Lyrical vs. Direct (poetic flourishes vs. straightforward prose)
- Descriptive vs. Sparse (rich sensory detail vs. minimal scene-setting)
- Internal vs. External (character thoughts vs. observable actions)

**Dialogue vs. Description Ratio:**
- Heavy dialogue (60%+ of prose is conversation)
- Balanced (mix of dialogue and narration)
- Description-focused (rich prose with occasional dialogue)

**Paragraph Structure:**
- Typical length (short paragraphs: 2-4 sentences, medium: 5-8, long: 9+)
- Pacing (paragraphs as beats, paragraphs as scenes)

I'll calculate these metrics and show you the results so you can confirm they feel accurate.

### Step 4: Define Voice Characteristics

Next, I'll ask you to explicitly define your narrative voice for this story:

**Point of View:**
- First-person ("I walked into the room")
- Third-person limited ("She walked into the room, wondering...")
- Third-person omniscient ("She walked into the room. What she didn't know was...")
- Second-person ("You walk into the room") — rare but valid

**Tense:**
- Past tense ("She walked") — most common in fiction
- Present tense ("She walks") — increasingly popular, immediate feel

**Formality Level:**
- Casual (conversational, relaxed, intimate)
- Moderate (literary but accessible)
- Formal (elevated language, careful distance)

**Narrative Distance:**
- Close (tight POV, deep in character's head, limited perspective)
- Moderate (some distance, balanced internal/external)
- Distant (observational, minimal interiority, more external focus)

### Step 5: Create STYLE.md Profile

I'll create `stories/{slug}/STYLE.md` using the style-profile.md template, filled with:
- Your sample analysis results (sentence patterns, vocabulary, tone)
- Your voice configuration (POV, tense, formality, distance)
- 1-2 preserved sample paragraphs for reference
- Synthesized generation guidelines (specific instructions for prose generation)

### Step 6: Confirmation

I'll show you a summary of your style profile and confirm it's saved. This profile will automatically be referenced when you run `/write:chapter` to generate prose.

**You can manually edit STYLE.md anytime** to adjust the patterns or add notes.

## What Happens Next

When you generate chapters with `/write:chapter`, the system will:
- Read your STYLE.md profile
- Match your sentence length patterns (not just "some are short, some are long" but actual target lengths)
- Match your vocabulary level (won't use "domicile" if your samples show "house")
- Match your tone markers (formal vs. casual, lyrical vs. direct)
- Respect your voice configuration (POV, tense, narrative distance)

**Example impact:**

*Without style seed (generic AI):*
> She delved into the mystery, navigating the complex web of clues. It was a testament to her detective skills that she'd made it this far.

*With style seed (matched to thriller sample above):*
> She hit the case files at midnight. Three victims, maybe four. The pattern would be there somewhere. Everyone missed patterns. She found them.

## Notes

- **Style seeding is optional** — you can skip this and `/write:chapter` will work with sensible defaults
- **One style profile per story** — different stories can have different styles
- **You can regenerate** the style profile anytime by running `/write:style` again
- **Analysis is guidance, not rules** — generated prose won't be robotic; it'll use your patterns as a foundation while staying natural
- **More samples = better analysis** — if you have 4-5 paragraphs instead of 2-3, even better

## Common Questions

**Q: Can I use published authors' writing as samples?**
A: Better not to. We want YOUR voice, not an imitation of someone else's. If you love Hemingway's sparse style, write a few paragraphs in that style yourself, then use those.

**Q: What if my writing style varies widely?**
A: Choose samples that match the style you want for THIS specific story. You can create different style profiles for different projects.

**Q: Can I have multiple style profiles in one story (e.g., different chapters)?**
A: Currently one STYLE.md per story, but you can manually edit it between chapters if you want variation.

**Q: Will the generated prose be exactly like my samples?**
A: No—it'll be original prose that *feels similar* in sentence rhythm, vocabulary choice, and tone. Think "matching your voice" not "copying your samples."

**Q: What if I don't have samples of my own writing?**
A: Write 2-3 paragraphs in the style you want for this story, treating it as a writing exercise. Those count as samples.

---

Ready? Let's define your writing style.

## Usage

In your story project directory:
```
/write:style
```

I'll guide you through the sample collection, analysis, and voice definition, then create your STYLE.md profile.
