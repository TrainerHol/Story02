# Plan 03-02: Length-Adapted Pacing Guidance - SUMMARY

**Completed:** 2026-02-27
**Duration:** ~18 minutes
**Result:** Success - All requirements met

## What Was Built

Implemented length-adapted pacing guidance system that analyzes story word count goals and provides tailored recommendations for chapter counts and act-based pacing structure:

1. **Story type categorization (LENGTH-03)**
   - Short story: 1,000-7,500 words → 1-3 chapters
   - Novella: 7,500-40,000 words → 5-15 chapters
   - Novel: 40,000-100,000 words → 15-30 chapters
   - Epic novel: 100,000+ words → 30-50+ chapters (with part divisions)

2. **Chapter count recommendations (LENGTH-03)**
   - Calculation formulas per story type:
     - Novella: `word_count_goal / 2500`
     - Novel: `word_count_goal / 3000`
     - Epic: `word_count_goal / 3500`
   - Adjustments based on OUTLINE.md complexity (plot beats, subplots)
   - Rationale provided for each recommendation

3. **Act-based pacing breakdown (LENGTH-04)**
   - Adapted structure for each story type:
     - Short story: 20-25% / 50-60% / 20-25% (tight, focused)
     - Novella: 25% / 50% / 25% (standard 3-act, streamlined)
     - Novel: 25% / 50% / 25% (full 3-act with subplots)
     - Epic: Multi-part structure with mini arcs per part
   - Chapter distribution across acts
   - Key story beats mapped to each act
   - Pacing characteristics per story length

4. **Chapter length targets**
   - Act-specific targets (setup longer, resolution faster)
   - Variable ranges to maintain reader interest
   - Examples for each story type

5. **Genre-specific recommendations**
   - Fantasy/Sci-Fi: Longer Act I for world-building
   - Mystery/Thriller: Shorter chapters, cliffhanger endings
   - Romance: Balanced pacing with emotional moments
   - Literary: Flexible structure
   - Horror: Build tension, accelerate in Act III
   - YA: Faster pacing, shorter chapters overall

## Key Files Created

### .claude/skills/write/pacing-guide.md (634 lines)
Complete `/write:pacing` workflow command with:
- Prerequisites validation
- 6-step workflow:
  1. Analyze story parameters (word count, genre, outline)
  2. Calculate recommended chapter count
  3. Provide act-based pacing breakdown
  4. Generate chapter length targets
  5. Provide genre-specific recommendations
  6. Display comprehensive recommendations
- Detailed breakdowns for 4 story types
- Examples for 5,000-word short story, 25k novella, 75k novel
- FAQ section with 13 common questions

**Chapter count examples:**
- 5k short story → 2-3 chapters OR continuous
- 25k novella → 10-12 chapters (~2,200 words/chapter)
- 75k novel → 22-25 chapters (~3,200 words/chapter)
- 150k epic → 40-45 chapters with 3-5 part divisions

**Pacing guidance examples:**
- Novella Act II: 50% (12,500 words, 6-7 chapters) - midpoint twist, complications
- Novel Act I: 25% (18,750 words, 6-7 chapters) - world-building, inciting incident
- Epic Part structure: 30% / 40% / 30% with mini three-act per part

### .planning/templates/story-project.md (updated)
Added "Pacing Guidance" section with:
- Recommended structure summary
- Act breakdown template:
  - Word count targets per act
  - Chapter ranges per act
  - Key story beats
- Chapter length targets by act
- Genre-specific notes
- Placeholder variables for `/write:pacing` to populate

Updated Metadata section:
- Target Chapters field note: "run /write:pacing for recommendations"

### .claude/skills/write/SKILL.md (updated)
- Added `/write:pacing` command entry with detailed description
- Lists what it analyzes, provides, input/output
- 5-10 minute execution time noted

## Technical Approach

**Story type determination:**
```
Read word_count_goal from PROJECT.md
if 1k-7.5k: short story
else if 7.5k-40k: novella
else if 40k-100k: novel
else: epic novel
```

**Chapter count calculation:**
- Base formula per type
- Adjustment factors:
  - +2-5 chapters for complex OUTLINE.md (many plot beats)
  - +3-7 chapters for multiple subplots
  - Longer chapters (upper range) for complex character arcs

**Act percentage distribution:**
- Short story: Modified single-arc (20-25 / 50-60 / 20-25)
- Standard fiction: Classic 3-act (25 / 50 / 25)
- Epic: Multi-part with 30 / 40 / 30 per part

**Genre adaptation:**
- Read genre from PROJECT.md
- Apply genre-specific pacing notes
- Adjust chapter length recommendations
- Provide structure notes (e.g., thriller uses cliffhangers)

## Deviations from Plan

None. All tasks completed as specified:
- ✓ Task 1: pacing-guide.md workflow created (150+ lines, actual: 634)
- ✓ Task 2: story-project.md updated with Pacing Guidance section
- ✓ Task 3: SKILL.md updated with /write:pacing entry

## Verification

**Requirements coverage:**
- LENGTH-03: Chapter count suggestions for story types ✓
- LENGTH-04: Pacing guidance adapted to story length ✓

**Must-haves validation:**
- System suggests chapter count based on story type ✓
- Pacing guidance adapted to story type ✓
- Writer can request pacing recommendations ✓
- Suggestions account for structure and word count goals ✓

**Artifact checks:**
- pacing-guide.md: 634 lines (exceeds 150 min) ✓
- story-project.md contains "## Pacing Guidance" ✓
- SKILL.md exports pacing-guide ✓
- Key links documented ✓

## Impact

Writers can now:
- Get appropriate chapter count recommendations for any story length
- Understand act structure adapted to their specific word count goal
- Plan pacing before writing (avoid structural issues mid-draft)
- Balance chapter lengths across acts for optimal reader experience
- Apply genre-specific pacing conventions
- Adjust expectations based on story complexity (outline analysis)
- Re-run pacing analysis at 25%, 50%, 75% milestones to course-correct

**Example use cases:**
- Novice writer with 60k goal: "I should aim for ~20 chapters, not 10 or 40"
- Epic fantasy writer: "My 150k story justifies 40+ chapters with part divisions"
- Short story writer: "I can use 2-3 chapters OR keep it continuous"
- Mystery writer: "Shorter chapters (1.8-2.5k) suit thriller pacing"

This prevents common pacing mistakes:
- Too many chapters for short stories (drags pace)
- Too few chapters for novels (each chapter too dense)
- Unbalanced act structure (45% Act I, 30% Act II - imbalanced)

## Commits

```
9416323 feat(03-02): implement length-adapted pacing guidance
- Created /write:pacing workflow with story type categorization
- Chapter count recommendations for all story lengths
- Act-based pacing breakdown adapted to length
- Genre-specific pacing notes
- Updated PROJECT template with Pacing Guidance section
```

**Files modified:** 2 created, 1 updated
**Lines added:** 665+
**Lines removed:** 1 (updated skill description)

## Self-Check

- [x] All requirements implemented
- [x] All must-haves deliverable
- [x] All artifacts meet minimum line requirements
- [x] Workflow documented with 3 complete examples
- [x] FAQ section with 13 questions
- [x] Genre-specific guidance for 6 genres
- [x] Committed to git with proper message format
- [x] No blockers or issues

**Status:** PASSED ✓
