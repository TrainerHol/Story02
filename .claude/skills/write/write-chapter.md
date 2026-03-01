# Chapter Generation Workflow

Write chapters and scenes with full story context - matches your style, maintains character voices, tracks plot threads.

## Overview

This workflow generates chapters that feel like YOUR writing, not generic AI prose. It loads all your story context (style profile, character voices, plot structure, world details) and produces prose that maintains consistency across your entire story.

**Time:** 20-40 minutes per chapter (depending on length)
**Output:** chapter-{NN}.md in your story's chapters/ directory
**When to use:** After story planning (YOLO or In-Depth mode), ready to draft

## How It Works

The system reads your entire story context, prompts you for chapter specifics (which plot beat, POV character, scene breakdown), then generates prose scene-by-scene while matching your style patterns and maintaining continuity.

## The Workflow

### Step 1: Validate Story Project

I'll verify you're in a valid story project by reading `PROJECT.md` from `stories/{slug}/`.

If you haven't initialized a project yet, run `/write:init` first.

### Step 2: Load Story Context

I'll load ALL available story files to ensure full consistency:

**Required files:**
- `PROJECT.md` — title, length, mode, genre, premise
- `CHARACTERS.md` or `yolo-characters.md` — character profiles with voice notes
- `OUTLINE.md` or `yolo-outline.md` — plot structure with beats

**Optional files (if they exist):**
- `STYLE.md` — your writing style profile (from `/write:style`)
- `ARCS.md` — character transformation tracking (In-Depth mode)
- `WORLD.md` — setting and world-building details (In-Depth mode)
- `chapters/*.md` — existing chapters for continuity

**What happens if STYLE.md is missing?**
The workflow still works! I'll use sensible defaults based on your genre and story length. But for best results that truly match YOUR voice, run `/write:style` first.

### Step 3: Prompt for Chapter Information

I'll ask you:

**Chapter Number:**
- Auto-suggest: "This would be Chapter {N}" based on existing chapters
- You can override (e.g., writing Chapter 5 before Chapter 4 is fine)

**Chapter Focus:**
- Which plot beat from OUTLINE.md are we writing?
- Or, describe the chapter's purpose in 1-2 sentences
- Example: "The confrontation at the abandoned mill - Sarah discovers the truth about her mother"

**POV Character:**
- Show you the character list from CHARACTERS.md
- You select who's perspective we're in for this chapter
- First-person stories: usually the protagonist
- Third-person: can vary chapter to chapter

**Scene Breakdown (optional):**
- You can specify scenes: "Scene 1: Arrival at mill, Scene 2: Discovery in basement, Scene 3: Escape"
- Or let me suggest scenes based on the plot beat
- Scenes help structure longer chapters (2000+ words)

### Step 4: Generation Instructions (What I'll Do Internally)

When generating prose, I will:

**Match Your Style (if STYLE.md exists):**
- Target your average sentence length (not just "some short, some long" but actual numbers)
- Match your vocabulary level (won't use "domicile" if your samples show "house")
- Follow your tone markers (formal vs casual, lyrical vs direct, sparse vs descriptive)
- Respect your rhythm patterns (short-short-long, balanced variety, etc.)
- Use your POV, tense, formality level, narrative distance

**Maintain Character Voices:**
- Read character voice notes from CHARACTERS.md
- POV character's internal voice matches their profile
- Dialogue for each character reflects their speech patterns
- Consistent personality across chapters

**Track Plot Threads:**
- Reference the specific plot beat from OUTLINE.md
- Note which threads are advanced in this chapter
- Avoid dropped plot threads (check what's been introduced, ensure continuation)

**Adapt Output Length to Story Type:**
Based on your PROJECT.md story length setting:

| Story Type | Chapter Target | Prose Style |
|------------|----------------|-------------|
| Short story (< 7.5k words) | 500-1000 words | Concise, fewer descriptive passages, tight scenes |
| Novella (7.5k-40k words) | 1000-2500 words | Moderate detail, balanced description and action |
| Novel (40k+ words) | 2000-4000 words | Rich descriptions, deeper scene exploration, layered detail |

**Maintain World Consistency:**
- Reference WORLD.md details when describing setting
- Keep worldbuilding rules consistent (magic systems, technology, society)

**Continue Character Arcs:**
- Reference ARCS.md to track character transformation
- Show character growth appropriate to story position
- Internal conflict development

**Ensure Continuity:**
- Read existing chapters to maintain consistency
- Track what characters know/don't know
- Maintain timeline and geography
- Reference previous events naturally

### Step 5: Scene-by-Scene Generation (if multiple scenes)

For chapters with multiple scenes:

**For each scene:**
1. I generate the scene with full context
2. Show you the prose
3. You can:
   - Approve and move to next scene
   - Request revisions ("make it more tense" / "add more dialogue")
   - Edit manually before continuing

**Why scene-by-scene?**
- Longer chapters (2000+ words) benefit from review points
- You can adjust direction mid-chapter
- Prevents giant blocks of prose that need full rewrites

**For shorter chapters (< 1500 words):**
- Generate as single piece
- Review once at end

### Step 6: Calculate Word Count

After generating the prose, I'll:

1. **Count words** in the chapter content (excluding frontmatter and markdown formatting)
   - Split on whitespace
   - Filter out markdown symbols
   - Count actual prose words

2. **Display chapter stats:**
   ```
   Chapter {N} complete: {word_count} words
   ```

### Step 7: Save Chapter

I'll create `stories/{slug}/chapters/chapter-{NN}.md` using the chapter.md template with:

**Frontmatter:**
```yaml
---
chapter: {number}
title: {optional chapter title}
pov: {character name}
scenes: {count}
word_count: {calculated}
plot_threads: [{threads addressed in this chapter}]
created: {timestamp}
revised: null
---
```

**Content:**
```markdown
# Chapter {N}: {Title}

{Generated prose}

---

## Notes
- Plot threads: {what was advanced}
- Character development: {what changed}
- World details: {what was revealed}
```

### Step 8: Update Story Progress

I'll update PROJECT.md with the new chapter:

1. **Read current word count** from PROJECT.md frontmatter (`current_word_count`)

2. **Calculate new total:**
   ```
   new_total = current_word_count + chapter_word_count
   ```

3. **Update PROJECT.md frontmatter:**
   - Set `current_word_count: {new_total}`

4. **Display progress:**
   ```
   ═══════════════════════════════════════
   STORY PROGRESS
   ═══════════════════════════════════════

   Total: {new_total} / {goal} words ({percentage}%)
   Chapters: {count}
   Average: {avg} words per chapter
   ```

   If `word_count_goal` is null, show count without percentage:
   ```
   Total: {new_total} words ({count} chapters)
   Average: {avg} words per chapter

   (Set word_count_goal in PROJECT.md to track progress percentage)
   ```

5. **Check chapter target** (if set):
   - Read Chapter Targets table from PROJECT.md Progress section
   - If target exists for this chapter number, compare:
     ```
     Chapter {N}: {actual} words (target was {target})
     Status: {under-target / on-target / over-target}
     ```

### Step 9: Suggest Next Chapter

Based on OUTLINE.md, I'll suggest what the next chapter should cover:
- "Ready for Chapter {N+1}: {next plot beat from outline}"
- Or, if outline complete: "Story arc complete - ready for conclusion"

## Style Matching Examples

**Without STYLE.md (generic AI):**
> She delved into the mystery surrounding her mother's disappearance. The tapestry of clues she'd assembled painted a complex picture. It was a testament to her investigative skills that she'd navigated this far into the labyrinth of secrets.

**With STYLE.md (matched to thriller style):**
> She hit the evidence board at midnight. Three years of clues. Her mother's calendar. The burner phone. The warehouse address. The pattern was there. She just couldn't see it yet.

**Without STYLE.md (generic literary):**
> The house stood silent, a monument to memory and loss. Within its walls, the ineffable weight of the past pressed upon her consciousness with unbearable intensity.

**With STYLE.md (matched to sparse literary style):**
> The house remembered her. Not with creaking floorboards—that was ghost story bullshit. It remembered in the way dust settled, in the smell of old wood, in the afternoon light that hadn't changed.

## Word Count Adaptation Examples

**Same scene, different story lengths:**

**Short story (concise):**
> Martinez took the stairs. Two floors, maybe three. The shooter would check the elevator first. Everyone checked the elevator. She hit the landing, pushed through the door, scanned the parking garage. Empty. She ran.

**Novella (moderate detail):**
> Martinez hit the stairwell at a run, taking the steps two at a time. The echo of her footsteps bounced off concrete walls. Two floors down, maybe three—enough to reach the parking garage. The shooter would expect the elevator. Everyone expected the elevator. She burst through the door at P3, her Glock sweeping the dim space. Rows of cars, support pillars, the exit ramp beyond. Empty. She sprinted for her car.

**Novel (rich description):**
> Martinez slammed into the stairwell with her shoulder, the metal door clanging against the wall. The fluorescent lights flickered overhead, casting harsh shadows down the concrete shaft. She grabbed the railing and vaulted down the first flight, her boots hitting every third step, the impact jarring through her knees. Two floors, maybe three—just enough to reach the parking level before the shooter could cut her off. The elevator would be his first guess. Everyone went for the elevator. It was human nature, that split-second choice for convenience even when death was seconds behind. She knew better. At P3 she hit the door hard, emerging into the underground garage with her Glock already tracking across the space. The air was thick with exhaust and motor oil. Rows of parked cars stretched into shadow under the low ceiling. Support pillars marked intervals like a concrete forest. The exit ramp glowed in the distance, a slope of freedom or a fatal funnel. No movement. She ran.

## Notes

- **Chapter generation adapts to context** — same workflow for 500-word short story chapters or 4000-word novel chapters
- **Style matching is automatic** — if STYLE.md exists, it's referenced; if not, genre-appropriate defaults apply
- **You control the pace** — scene-by-scene generation for long chapters, single-pass for short ones
- **Manual editing is fine** — generated chapters are starting points; edit freely
- **Consistency is priority** — character voices, plot threads, world rules all tracked automatically
- **Re-generation is supported** — unhappy with a chapter? Delete it and run `/write:chapter` again

## Common Questions

**Q: Can I write chapters out of order?**
A: Yes, but for best continuity, write sequentially. Out-of-order chapters won't have context from later chapters.

**Q: What if I haven't created a STYLE.md profile?**
A: The workflow still works with sensible defaults based on your genre and story length. But style matching is most effective with an actual profile.

**Q: How detailed should my scene breakdown be?**
A: Brief is fine. "Scene 1: Confrontation, Scene 2: Revelation, Scene 3: Escape" is enough. I'll handle the prose.

**Q: Can I revise a generated chapter later?**
A: Absolutely. Edit the markdown file directly. The frontmatter tracks revisions (update `revised:` timestamp manually).

**Q: Will character dialogue sound the same across chapters?**
A: No—each character's voice from CHARACTERS.md is maintained. The detective talks differently than the witness.

**Q: What if I want a different POV mid-chapter?**
A: Currently one POV per chapter. For multiple POVs, create separate chapters or manually edit after generation.

**Q: How does word count tracking work?**
A: The workflow automatically calculates word count for each chapter and updates PROJECT.md `current_word_count` field. If you've set `word_count_goal`, you'll see progress percentage. If you've defined chapter targets in the Progress section table, you'll see status (under/on/over target).

**Q: Can I generate a chapter without an outline?**
A: The workflow expects OUTLINE.md or yolo-outline.md. If you skipped planning, create a minimal outline with 3-5 plot beats first.

---

Ready? Let's write a chapter.

## Usage

In your story project directory:
```
/write:chapter
```

I'll load your story context, prompt for chapter details, and generate prose that matches your voice and maintains consistency with everything you've built.
