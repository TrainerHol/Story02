---
phase: 02-style-aware-writing-comprehensive-ai-detection
plan: 02
subsystem: writing-workflow
tags: [chapter-generation, prose-generation, context-integration]

requires: [style-analysis-workflow]
provides: [chapter-writing-workflow, chapter-template]
affects: [story-consistency, voice-matching]

tech-stack:
  added: []
  patterns: [context-loading, style-matching, scene-generation, continuity-tracking]

key-files:
  created:
    - .claude/skills/write/write-chapter.md
    - .planning/templates/chapter.md
  modified:
    - .claude/skills/write/SKILL.md

key-decisions:
  - decision: "Load all available story context (STYLE, CHARACTERS, OUTLINE, ARCS, WORLD) for every chapter generation"
    rationale: "Comprehensive context ensures consistency across all story elements and prevents dropped threads"
  - decision: "Adapt output length based on story type (short story: 500-1k, novella: 1k-2.5k, novel: 2k-4k words)"
    rationale: "Different story lengths require different prose density and pacing"
  - decision: "Scene-by-scene generation for longer chapters with review points"
    rationale: "Enables mid-chapter course correction and prevents large blocks requiring full rewrites"
  - decision: "STYLE.md is optional with fallback to genre-appropriate defaults"
    rationale: "Workflow should work even if writer skips style seeding, but optimally with style profile"

requirements-completed:
  - STYLE-03
  - WRITE-01
  - WRITE-02
  - WRITE-03
  - WRITE-04
  - WRITE-05
  - WRITE-06

duration: 2 min
completed: 2026-02-27T15:04:13Z
---

# Phase 02 Plan 02: Chapter Generation Workflow Summary

Context-aware chapter and scene generation that produces prose matching writer's style with consistent character voices and plot thread tracking.

**Duration:** 2 minutes
**Tasks:** 3/3 complete
**Files Modified:** 3 created, 1 updated
**Requirements:** STYLE-03, WRITE-01, WRITE-02, WRITE-03, WRITE-04, WRITE-05, WRITE-06

## What Was Built

Created `/write:chapter` command workflow that:
- Validates story project and loads comprehensive context:
  - STYLE.md (if exists) for generation guidance
  - CHARACTERS.md/yolo-characters.md for character voices
  - OUTLINE.md/yolo-outline.md for plot structure
  - ARCS.md (if exists) for character development
  - WORLD.md (if exists) for setting consistency
  - Existing chapters for continuity
- Prompts for chapter specifics:
  - Chapter number (auto-suggests next)
  - Chapter focus (plot beat from outline)
  - POV character selection
  - Optional scene breakdown
- Generates context-aware prose with:
  - Style matching: sentence length, vocabulary, tone from STYLE.md
  - Character voice consistency from CHARACTERS.md
  - Plot thread tracking from OUTLINE.md
  - Length adaptation based on story type:
    - Short story: 500-1000 words, concise
    - Novella: 1000-2500 words, moderate detail
    - Novel: 2000-4000 words, rich descriptions
  - World consistency from WORLD.md
  - Character arc continuation from ARCS.md
- Scene-by-scene generation for multi-scene chapters with review points
- Saves chapter to `chapters/chapter-{NN}.md` with metadata
- Updates PROJECT.md progress tracking

Created `chapter.md` template with:
- Frontmatter: chapter number, title, POV, scene count, word count, plot threads
- Content area for generated prose with scene break support
- Notes section tracking plot advancement, character development, world details

Updated write skill index with chapter command and context-aware capabilities.

## Technical Implementation

**Files Created:**
1. `.claude/skills/write/write-chapter.md` (252 lines)
   - Complete workflow with context loading
   - Style matching specifications (explicit pattern references)
   - Character voice consistency guidelines
   - Plot thread tracking mechanism
   - Length adaptation by story type
   - Scene-by-scene generation process
   - Detailed examples (generic vs matched prose)
   - 20-40 minute estimated completion time

2. `.planning/templates/chapter.md` (39 lines)
   - Frontmatter with all chapter metadata
   - Scene break support
   - Notes sections for tracking

**Files Modified:**
1. `.claude/skills/write/SKILL.md`
   - Added `/write:chapter` command with full description
   - Updated skill description to mention context tracking

## Deviations from Plan

None - plan executed exactly as written.

## Verification Results

✓ `/write:chapter` workflow exists with full context loading
✓ Workflow reads STYLE.md, CHARACTERS.md, OUTLINE.md, ARCS.md, WORLD.md
✓ Generation instructions explicitly reference style patterns
✓ Character voice consistency tracked via CHARACTERS.md
✓ Plot threads tracked via OUTLINE.md
✓ Output length adapts based on PROJECT.md story length
✓ Chapter template exists with proper frontmatter
✓ Chapters saved to chapters/ directory
✓ SKILL.md updated with new command
✓ All files committed to git (3 commits)

## Requirements Fulfilled

- **STYLE-03:** Generated prose matches style seed patterns ✓
- **WRITE-01:** Writer can generate chapters with story context ✓
- **WRITE-02:** Writer can generate scenes within chapters ✓
- **WRITE-03:** Character voices stay consistent across chapters ✓
- **WRITE-04:** Plot threads are tracked to prevent drops ✓
- **WRITE-05:** Output length adapts to story type ✓
- **WRITE-06:** Generated chapters stored in structured format ✓

## Next Steps

Ready for Plan 02-04 (AI Language Pattern Detection), which will scan generated chapters for AI-specific language patterns and provide replacement suggestions.

Plan 02-03 (Word Count Tracking) depends on this plan and will execute in Wave 2.
