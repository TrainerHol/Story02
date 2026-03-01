# /write:pacing - Story Pacing Guidance

Get story-specific pacing recommendations based on your word count goal and story type. Suggests appropriate chapter count and provides act-based pacing breakdown adapted to your story length.

## Overview

**What it does:**
- Analyzes story length, genre, and structure to provide tailored pacing recommendations
- Categorizes story type: short story, novella, novel, or epic novel
- Suggests optimal chapter count for target word count (LENGTH-03)
- Provides act-by-act pacing breakdown adapted to story length (LENGTH-04)
- Offers chapter length targets and story beat distribution
- Accounts for genre-specific pacing conventions
- **Execution time:** 5-10 minutes

## Prerequisites

Before requesting pacing guidance:
- Valid story project must exist (PROJECT.md)
- `word_count_goal` should be set in PROJECT.md (or you'll be prompted for target length)
- OUTLINE.md recommended but not required (system provides generic structure if missing)

If word count goal not set, the system will prompt you to specify target length before generating recommendations.

## Workflow

### Step 1: Analyze story parameters

Read and extract key project data:

**From PROJECT.md:**
- **word_count_goal:** Target story length (e.g., 5000, 25000, 75000)
- **genre:** Story genre (fantasy, thriller, romance, literary, etc.)
- **current_word_count:** Progress so far (if chapters written)
- **Existing chapters:** Count of chapters already drafted

**Categorize story type based on word count goal:**

| Word Count Range | Category | Typical Structure |
|------------------|----------|-------------------|
| 1,000 - 7,500 | Short story | Tight, focused narrative |
| 7,500 - 40,000 | Novella | Moderate complexity |
| 40,000 - 100,000 | Novel | Full subplot development |
| 100,000+ | Epic novel | Complex multi-thread narrative |

**From OUTLINE.md (if exists):**
- Count major plot beats
- Identify act structure (2-act, 3-act, 5-act)
- Note subplot count
- Check for major set pieces or climax events

If no OUTLINE.md exists, default to standard 3-act structure with genre conventions.

### Step 2: Calculate recommended chapter count (LENGTH-03)

Based on story type and word count goal, suggest chapter count using these guidelines:

#### Short Story (1,000-7,500 words)

**Recommended chapters:** 1-3 chapters (or single continuous piece)

**Rationale:**
- Short stories benefit from tight structure and minimal chapter breaks
- Most short stories work best as single continuous narratives
- If breaking into chapters, use natural dramatic pauses (perspective shifts, time jumps)

**Chapter length targets:**
- 1-chapter story: entire word count
- 2-chapter story: ~1,500-3,500 words per chapter
- 3-chapter story: ~1,000-2,500 words per chapter

**Pacing note:** Every scene must advance plot or character. No room for filler or extensive world-building. Get in, deliver impact, get out.

#### Novella (7,500-40,000 words)

**Recommended chapters:** 5-15 chapters

**Calculation:** `word_count_goal / 2500` (average chapter length)

**Examples:**
- 10,000 words → 4-6 chapters
- 25,000 words → 10-12 chapters
- 35,000 words → 14-16 chapters

**Chapter length targets:** 1,500-3,000 words per chapter

**Rationale:**
- Balance between story length and scene segmentation
- Enough chapters to build tension and develop limited subplots
- Not so many that pacing drags

**Pacing note:** Moderate scene development. Focus on core plot with 1-2 limited subplots. Character development possible but streamlined.

#### Novel (40,000-100,000 words)

**Recommended chapters:** 15-30 chapters

**Calculation:** `word_count_goal / 3000` (average chapter length)

**Examples:**
- 50,000 words → 16-18 chapters
- 75,000 words → 22-25 chapters
- 90,000 words → 27-30 chapters

**Chapter length targets:** 2,000-4,000 words per chapter

**Rationale:**
- Standard novel structure with room for subplots and pacing variation
- Allows for multiple POV characters if desired
- Sufficient chapters for proper three-act structure development

**Pacing note:** Room for slower character moments, detailed world-building, subplot development. Can vary chapter length for pacing effect (faster chapters near climax).

#### Epic Novel (100,000+ words)

**Recommended chapters:** 30-50+ chapters (consider part/section divisions)

**Calculation:** `word_count_goal / 3500` (average chapter length)

**Examples:**
- 120,000 words → 32-35 chapters
- 150,000 words → 40-45 chapters
- 200,000 words → Consider 3-5 parts of 10-15 chapters each

**Chapter length targets:** 2,500-5,000 words per chapter

**Structure consideration:**
- For 120k+: Consider dividing into Parts (Part I, Part II, Part III)
- Each part can follow mini three-act structure
- Part breaks at major story transitions (time jump, location shift, perspective change)

**Pacing note:** Complex stories need more segmentation. Multiple POVs expected. Extensive subplots justified. Can afford slower world-building sections.

**Adjustments based on OUTLINE.md:**

If outline analysis reveals:
- **More plot beats than typical:** Add 2-5 chapters
- **Multiple subplots (3+):** Add 3-7 chapters
- **Complex character arcs (4+ characters):** Slightly longer chapters (upper range)
- **Single-thread narrative:** Fewer chapters (lower range)

### Step 3: Provide act-based pacing breakdown (LENGTH-04)

Generate pacing guidance adapted to story length:

#### For Short Stories

**Structure:** Modified single-arc structure

**Act I (Setup) - 20-25% of word count:**
- Establish character and conflict immediately
- No lengthy exposition — drop reader into action
- Inciting incident within first 10-20% of story

**Act II (Confrontation) - 50-60% of word count:**
- Rising tension and complications
- Single core conflict (no time for subplot complexity)
- Steady escalation to crisis point

**Act III (Resolution) - 20-25% of word count:**
- Climax and denouement tightly compressed
- Quick resolution after climax
- Resonant ending without drawn-out wrap-up

**Chapter distribution:** If using chapters, typically equal length OR single continuous narrative

**Pacing characteristics:**
- No slow starts — immediate engagement
- Every paragraph must earn its place
- Tighter scene construction than novels
- Resolution comes quickly after climax

#### For Novellas

**Structure:** Standard three-act structure, streamlined

**Act I (Setup) - 25% of word count (~3-5 chapters):**
- Introduce protagonist in normal world
- Establish character motivation quickly
- Inciting incident (the event that launches the story)
- First plot point / point of no return

**Target word count:** `0.25 * word_count_goal`
**Example (25k novella):** ~6,250 words, ~3-4 chapters

**Act II (Confrontation) - 50% of word count (~6-10 chapters):**
- Rising action with complications
- Midpoint: major twist or revelation that shifts the story
- Pinch points: increasing pressure on protagonist
- Darkest moment / all is lost
- Builds to second plot point

**Target word count:** `0.50 * word_count_goal`
**Example (25k novella):** ~12,500 words, ~6-7 chapters

**Act III (Resolution) - 25% of word count (~3-5 chapters):**
- Final confrontation setup
- Climax: the big showdown or revelation
- Falling action: immediate aftermath
- Resolution: tie up plot threads

**Target word count:** `0.25 * word_count_goal`
**Example (25k novella):** ~6,250 words, ~3-4 chapters

**Pacing characteristics:**
- Faster than novels, more development than short stories
- Can support 1-2 moderate subplots
- Character development focused on protagonist + 1-2 key supporting characters
- World-building present but efficient

#### For Novels

**Structure:** Full three-act structure with subplots

**Act I (Setup) - 25% of word count (~5-8 chapters):**
- Establish world, introduce full cast
- Multiple character POVs if applicable
- Inciting incident establishes stakes
- Character introductions with room for personality
- First plot point propels into main conflict

**Target word count:** `0.25 * word_count_goal`
**Example (75k novel):** ~18,750 words, ~6-7 chapters

**Act II (Confrontation) - 50% of word count (~10-15 chapters):**
- Multiple subplot threads introduced and developed
- Character development arcs for protagonist + 2-4 key characters
- Midpoint reversal: major shift in story direction or revelation
- Pinch points: escalating obstacles and complications
- Subplot complications interweave with main plot
- Try/fail cycles for protagonist
- Darkest moment: lowest point before final act

**Target word count:** `0.50 * word_count_goal`
**Example (75k novel):** ~37,500 words, ~12-13 chapters

**Act III (Resolution) - 25% of word count (~5-8 chapters):**
- Converge subplot threads
- Final confrontation setup
- Climax: culmination of all threads
- Falling action with emotional beats
- Denouement: resolution with character reflection
- Tie up all major plot threads

**Target word count:** `0.25 * word_count_goal`
**Example (75k novel):** ~18,750 words, ~6-7 chapters

**Pacing characteristics:**
- Room for slower character moments and introspection
- Detailed world-building integrated naturally
- Subplot development alongside main plot
- Can vary chapter length for effect (short intense chapters, long development chapters)
- Multiple POV characters supported

#### For Epic Novels

**Structure:** Multi-part three-act structure

**Recommended approach:** Divide into 3-5 parts, each with mini three-act structure

**Part I (30% of novel):**
- World establishment and character introduction
- Part climax: first major event or revelation
- Internal structure: Setup → Complication → Part Resolution

**Part II (40% of novel):**
- Main complications and subplot development
- Major midpoint for entire novel
- Part climax: significant reversal or darkest moment

**Part III (30% of novel):**
- Convergence of all threads
- Final confrontations and climax
- Extended denouement for complex story resolution

**Chapter distribution example (150k epic):**
- Part I: 12-15 chapters (~45k words)
- Part II: 16-20 chapters (~60k words)
- Part III: 12-15 chapters (~45k words)

**Pacing characteristics:**
- Multiple POV characters expected (4-8+ POVs)
- Extensive world-building justified
- Complex subplot network (4-6+ subplots)
- Room for political intrigue, romance arcs, character backstories
- Can afford slower sections if balanced with high-tension sequences

### Step 4: Generate chapter length targets

Provide granular chapter targets based on act positioning:

**Act-based variation approach:**

**Act I chapters (Setup):**
- Slightly longer to establish world and characters
- More description and context-setting
- Example ranges:
  - Short story: N/A (often no chapters in Act I)
  - Novella: 2,500-3,000 words
  - Novel: 3,000-3,500 words
  - Epic: 3,500-4,500 words

**Act II chapters (Confrontation):**
- Variable length to maintain interest
- Mix of action-heavy (shorter) and development (longer) chapters
- Example ranges:
  - Short story: 1,000-2,000 words (if chaptered)
  - Novella: 2,000-3,000 words
  - Novel: 2,500-4,000 words (high variance for pacing)
  - Epic: 2,500-5,000 words

**Act III chapters (Resolution):**
- Shorter chapters as pace accelerates toward climax
- Faster reading experience creates urgency
- Example ranges:
  - Short story: 800-1,500 words
  - Novella: 1,800-2,500 words
  - Novel: 2,000-3,000 words
  - Epic: 2,500-3,500 words

**Recommendation:** Avoid making all chapters exactly the same length. Natural variation (2k, 3.5k, 2.8k, 4k) maintains reader interest better than rigid uniformity (3k, 3k, 3k, 3k).

### Step 5: Provide genre-specific recommendations

Based on genre from PROJECT.md:

**Fantasy / Science Fiction:**
- Allow longer chapters in Act I for world-building (readers expect immersion)
- Can support extensive world detail if core narrative maintains momentum
- Epic fantasy: justify 4-5k word chapters with rich detail
- Urban fantasy: faster pacing, shorter chapters (2-3k)

**Mystery / Thriller:**
- Shorter chapters in Act II and III for page-turner effect (1.5-2.5k)
- Cliffhanger chapter endings encouraged
- Fast pacing: scenes end on questions or tension
- Reveal information gradually across many chapters

**Romance:**
- Balance pacing with relationship development
- Allow slower emotional moments (introspection scenes)
- Chapter length can vary widely (2-4k) based on emotional vs action content
- Subplot romantic tension can justify longer middle act

**Literary Fiction:**
- Flexible pacing based on theme and style
- Character introspection chapters can be longer
- Not bound to rigid structure if thematic purpose justifies
- Short story length (under 10k) very common in literary

**Horror:**
- Build tension gradually in Act I and II
- Shorter chapters near climax (1.5-2k) for urgency and fear pacing
- Atmosphere-building can justify longer early chapters
- Accelerate pace in final act

**Young Adult:**
- Slightly faster pacing than adult fiction
- Shorter chapters overall (2-3k typical)
- Quick hooks at chapter starts
- Strong chapter-ending hooks to encourage page-turning

### Step 6: Display recommendations

Generate comprehensive output for writer:

```
═══════════════════════════════════════════════════════
        PACING RECOMMENDATIONS
═══════════════════════════════════════════════════════

Story: {Title}
Target Word Count: {word_count_goal} words
Current Progress: {current_word_count} / {word_count_goal} ({percentage}%)
Genre: {genre}

───────────────────────────────────────────────────────
STORY TYPE: {Short Story | Novella | Novel | Epic Novel}
───────────────────────────────────────────────────────

RECOMMENDED CHAPTER COUNT: {N} chapters
Rationale: {Explanation based on word count and structure}

Average chapter length: ~{calculated} words
Range: {min}-{max} words per chapter

───────────────────────────────────────────────────────
ACT BREAKDOWN
───────────────────────────────────────────────────────

ACT I (Setup) — {percentage}%
Target word count: {calculated} words
Chapter range: Chapters {1-N}
Estimated chapters: {count}

Key story beats:
• Establish protagonist and normal world
• Inciting incident
• First plot point / point of no return

Pacing notes: {Story-type-specific guidance}

ACT II (Confrontation) — {percentage}%
Target word count: {calculated} words
Chapter range: Chapters {N-M}
Estimated chapters: {count}

Key story beats:
• Rising action and complications
• Midpoint twist or revelation
• Escalating obstacles
• Darkest moment / all is lost

Pacing notes: {Story-type-specific guidance}

ACT III (Resolution) — {percentage}%
Target word count: {calculated} words
Chapter range: Chapters {M-end}
Estimated chapters: {count}

Key story beats:
• Final confrontation
• Climax
• Falling action
• Resolution

Pacing notes: {Story-type-specific guidance}

───────────────────────────────────────────────────────
CHAPTER LENGTH TARGETS
───────────────────────────────────────────────────────

Act I chapters: {range} words (world-building focus)
Act II chapters: {range} words (variable for pacing)
Act III chapters: {range} words (faster pacing)

Recommendation: Vary chapter length to maintain interest

───────────────────────────────────────────────────────
GENRE-SPECIFIC NOTES
───────────────────────────────────────────────────────

{Genre}: {Specific pacing recommendations for this genre}

───────────────────────────────────────────────────────
CURRENT PROGRESS ASSESSMENT
───────────────────────────────────────────────────────

Chapters written: {count}
Words so far: {current_word_count}
On pace for: {projected chapter count based on current average}

Status: {On track | Ahead of pace | Behind pace | Needs adjustment}

{If adjustment needed: specific recommendation}

───────────────────────────────────────────────────────
NEXT STEPS
───────────────────────────────────────────────────────

1. Update PROJECT.md `target_chapters` field to {recommended}
2. Review OUTLINE.md and distribute plot beats across acts
3. Use chapter targets as guidelines (not rigid requirements)
4. Start writing and adjust pacing based on story needs

═══════════════════════════════════════════════════════
```

Optionally write recommendations to PROJECT.md "Pacing Guidance" section.

## Examples

### Example 1: Short Story (5,000 words)

**Analysis:**
- Word count goal: 5,000
- Type: Short story
- Genre: Literary fiction

**Recommendations:**
- **Chapters:** 2-3 chapters OR single continuous narrative
- **Structure:**
  - Setup: 1,000-1,250 words (20-25%)
  - Confrontation: 2,500-3,000 words (50-60%)
  - Resolution: 1,000-1,250 words (20-25%)
- **Chapter targets:** 1,500-2,500 words if using chapters
- **Pacing:** Tight focus, every scene advances plot, immediate engagement

### Example 2: Novella (25,000 words)

**Analysis:**
- Word count goal: 25,000
- Type: Novella
- Genre: Mystery

**Recommendations:**
- **Chapters:** 10-12 chapters
- **Average:** ~2,200 words per chapter
- **Act I (6,250 words):** Chapters 1-3
  - Introduce detective, establish murder, first clues
- **Act II (12,500 words):** Chapters 4-9
  - Investigation, red herrings, midpoint revelation, complications
- **Act III (6,250 words):** Chapters 10-12
  - Final clues, confrontation, resolution
- **Genre note:** Shorter chapters (1,800-2,500 words) with cliffhangers for page-turning effect

### Example 3: Novel (75,000 words)

**Analysis:**
- Word count goal: 75,000
- Type: Novel
- Genre: Fantasy

**Recommendations:**
- **Chapters:** 22-25 chapters
- **Average:** ~3,200 words per chapter
- **Act I (18,750 words):** Chapters 1-6
  - World-building, magic system intro, protagonist in normal life
  - Inciting incident, stakes established, first plot point
  - Chapter targets: 3,000-3,500 words (world immersion)
- **Act II (37,500 words):** Chapters 7-18
  - Quest/journey begins, complications, secondary characters
  - Midpoint: major revelation about magic or antagonist
  - Subplots: romantic tension, political intrigue
  - Chapter targets: 2,500-4,000 words (varied for pacing)
- **Act III (18,750 words):** Chapters 19-25
  - Convergence of plot threads, final battle preparation
  - Climax: magical confrontation
  - Denouement: new world order, character reflection
  - Chapter targets: 2,000-3,000 words (faster pace)
- **Genre note:** Fantasy readers expect world detail; longer Act I chapters justified for immersion

## FAQ

**Q: Can I have more or fewer chapters than recommended?**
A: Absolutely. These are guidelines based on typical story structures. If your story naturally breaks into 18 chapters instead of 22, that's fine. Follow your story's natural scene divisions.

**Q: What if I'm pantsing (writing without an outline)?**
A: Use the genre conventions and basic three-act structure as a loose roadmap. You can course-correct as you discover your story. Check pacing again at 25%, 50%, and 75% completion.

**Q: Should all my chapters be the same length?**
A: No! Varying chapter length creates better pacing. Fast action chapters can be short (1,500-2,000 words), character development chapters can be longer (3,500-4,000 words). Monotonous uniformity can be predictable.

**Q: What if my word count is between categories?**
A: Interpolate. For example, 45,000 words is upper novella / lower novel territory. You might use 15-18 chapters (between novella's 5-15 and novel's 15-30). Use the approach that feels right for your story complexity.

**Q: How strictly should I follow act percentages?**
A: They're guidelines, not laws. The 25/50/25 split is a proven structure, but 20/60/20 or 30/50/20 can work too. The key principle: setup is shorter than complication, resolution is concise after climax.

**Q: What about 4-act or 5-act structures?**
A: This tool focuses on three-act (most common in modern fiction). If you're using Save the Cat (15-beat), Hero's Journey (12-stage), or other structures, map those beats to the three-act framework for pacing purposes.

**Q: Can I change pacing recommendations mid-project?**
A: Yes. If you're 30 chapters into what you thought would be a 25-chapter novel, adjust your expectations. The story tells you its natural length. Re-run `/write:pacing` at milestones to reassess.

**Q: What about prologue and epilogue?**
A: Count them in your chapter total. A prologue is typically Act I (or pre-Act I). Epilogue is post-Act III resolution. Factor them into word count but they don't need to match standard chapter lengths.

**Q: My genre isn't listed. What should I do?**
A: Use the closest match:
- Historical fiction → Literary or Fantasy pacing (depending on detail level)
- Paranormal romance → Romance + Fantasy world-building
- Cozy mystery → Mystery (but can be slightly slower than thriller)
- Dystopian → Science Fiction structure

**Q: How often should I check my pacing?**
A: Run pacing check:
- Before starting (planning phase)
- At 25% completion (end of Act I)
- At 50% completion (midpoint)
- At 75% completion (entering Act III)
- After draft completion (assess if revision needed)

**Q: What if I'm significantly over or under my target?**
A: Common during drafting. Options:
- **Over target:** Tighten prose, cut subplots, remove filler scenes
- **Under target:** Deepen character moments, add subplot complexity, expand world-building (but only if it serves the story)
- **Accept new target:** If the story wants to be 90k instead of 75k, let it
