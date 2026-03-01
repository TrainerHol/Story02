---
phase: 02-style-aware-writing-comprehensive-ai-detection
plan: 03
subsystem: writing-workflow
tags: [word-count, progress-tracking, goal-setting]

requires: [chapter-writing-workflow]
provides: [word-count-tracking]
affects: [project-progress, chapter-planning]

tech-stack:
  added: []
  patterns: [automatic-counting, progress-calculation, target-comparison]

key-files:
  created: []
  modified:
    - .planning/templates/story-project.md
    - .claude/skills/write/write-chapter.md

key-decisions:
  - decision: "Automatic word count updates in PROJECT.md after each chapter generation"
    rationale: "Eliminates manual tracking, ensures accuracy, provides immediate progress feedback"
  - decision: "Optional goal setting with graceful handling of null goals"
    rationale: "Writers who skip goal-setting still get word counts; those who set goals get progress tracking"
  - decision: "Chapter-level target tracking via Progress section table"
    rationale: "Enables pacing control for writers who want granular chapter length management"
  - decision: "Story length guidelines in template (short: 1k-7.5k, novella: 7.5k-40k, novel: 40k+)"
    rationale: "Helps writers set realistic goals based on story type"

requirements-completed:
  - WRITE-07
  - WRITE-08
  - WRITE-09
  - WRITE-10

duration: 1 min
completed: 2026-02-27T15:11:35Z
---

# Phase 02 Plan 03: Word Count Tracking System Summary

Word count tracking system for story projects, enabling progress monitoring toward length goals with automatic updates.

**Duration:** 1 minute
**Tasks:** 2/2 complete
**Files Modified:** 2 updated
**Requirements:** WRITE-07, WRITE-08, WRITE-09, WRITE-10

## What Was Built

Enhanced PROJECT.md template with word count fields:
- Added frontmatter fields:
  - `word_count_goal`: Writer-defined target (e.g., 50000 for novel)
  - `current_word_count`: Auto-updated running total (starts at 0)
  - `target_chapters`: Optional estimated chapter count
- Added Word Count section in Progress with:
  - Goal display (or "Not set")
  - Current total display
  - Progress percentage (if goal is set)
  - Average words per chapter
  - Story length guidelines (short story, novella, novel ranges)
- Added Chapter Targets table for per-chapter word count goals:
  - Chapter number, target, actual, status columns
  - Optional feature for pacing control

Enhanced write-chapter.md workflow with automatic tracking:
- Calculate word count after prose generation:
  - Count words in chapter content
  - Exclude frontmatter and markdown formatting
  - Use whitespace splitting with symbol filtering
- Update chapter frontmatter `word_count` field
- Read PROJECT.md `current_word_count`
- Calculate new total (current + chapter)
- Update PROJECT.md `current_word_count` field
- Display progress after each chapter:
  - Total words / goal (percentage) if goal set
  - Total words with chapter count if no goal
  - Chapter count and average per chapter
- Check chapter targets (if defined):
  - Compare actual vs target
  - Display status: under-target / on-target / over-target
- Handle null goals gracefully (show counts without percentages)

## Technical Implementation

**Files Modified:**
1. `.planning/templates/story-project.md`
   - Added 3 frontmatter fields
   - Added Word Count subsection in Progress (8 lines)
   - Added Chapter Targets table structure
   - Added story length guidelines

2. `.claude/skills/write/write-chapter.md`
   - Added Step 6: Calculate Word Count
   - Enhanced Step 8: Update Story Progress (replaces Step 7)
   - Added progress display formatting
   - Added chapter target checking
   - Updated FAQ about word count tracking

## Deviations from Plan

None - plan executed exactly as written.

## Verification Results

✓ PROJECT.md template has word_count_goal, current_word_count, target_chapters fields
✓ PROJECT.md template has Progress section with word count tracking display
✓ write-chapter.md calculates word count for generated chapters
✓ write-chapter.md updates PROJECT.md current_word_count after each chapter
✓ write-chapter.md displays progress toward goal
✓ write-chapter.md checks and displays chapter targets if set
✓ Word count calculation excludes frontmatter and markdown formatting
✓ All files committed to git (2 commits)

## Requirements Fulfilled

- **WRITE-07:** Writer can set project word count goals ✓
- **WRITE-08:** System tracks current word count across chapters ✓
- **WRITE-09:** Writer can see progress toward goal ✓
- **WRITE-10:** Writer can set chapter target word counts ✓

## Next Steps

Phase 02 complete! All 4 plans executed:
- 02-01: Style Seeding System ✓
- 02-02: Chapter Generation Workflow ✓
- 02-03: Word Count Tracking ✓
- 02-04: AI Pattern Detection ✓

Ready for phase verification to confirm all requirements (STYLE-01 through STYLE-04, WRITE-01 through WRITE-10, AI-01 through AI-10) are fulfilled.
