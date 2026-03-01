---
phase: 02-style-aware-writing-comprehensive-ai-detection
plan: 04
subsystem: writing-workflow
tags: [ai-detection, prose-quality, pattern-scanning]

requires: [chapter-writing-workflow]
provides: [ai-pattern-detection, pattern-database]
affects: [prose-revision, voice-authenticity]

tech-stack:
  added: []
  patterns: [pattern-matching, text-scanning, replacement-suggestion]

key-files:
  created:
    - .planning/templates/ai-patterns.md
    - .claude/skills/write/ai-detect.md
  modified:
    - .claude/skills/write/SKILL.md

key-decisions:
  - decision: "10 specific AI pattern types with concrete replacement suggestions (not generic advice)"
    rationale: "Writers need actionable alternatives, not just awareness; 3-5 replacements per pattern enables choice"
  - decision: "Pattern database as editable markdown template with YAML custom section"
    rationale: "Allows project-specific customization and easy addition of writer's personal overuse patterns"
  - decision: "Comprehensive reporting with location, context, why flagged, and replacements"
    rationale: "Full context enables informed decisions about what to change vs. what to keep"
  - decision: "Support for project-specific AI-PATTERNS.md overrides"
    rationale: "Different stories/genres may need different pattern sensitivity; customization per-project"

requirements-completed:
  - AI-01
  - AI-02
  - AI-03
  - AI-04
  - AI-05
  - AI-06
  - AI-07
  - AI-08
  - AI-09
  - AI-10

duration: 3 min
completed: 2026-02-27T15:08:30Z
---

# Phase 02 Plan 04: AI Language Pattern Detection Summary

Comprehensive AI pattern detection system with 10 built-in patterns, concrete replacement suggestions, and custom phrase management.

**Duration:** 3 minutes
**Tasks:** 3/3 complete
**Files Modified:** 3 created, 1 updated
**Requirements:** AI-01 through AI-10

## What Was Built

Created `/write:detect` command workflow that:
- Validates story project or accepts pasted text
- Prompts for scan scope:
  - Single chapter by number
  - All chapters in project
  - Direct text paste (one-time scan)
- Loads pattern database:
  - Default: `.planning/templates/ai-patterns.md`
  - Override: `stories/{slug}/AI-PATTERNS.md` (if exists)
- Scans for 10 AI pattern types:
  1. Delve/Delved/Delving (keyword)
  2. Tapestry (metaphorical keyword)
  3. Navigate/Navigated (metaphorical keyword)
  4. Testament to (phrase)
  5. Juxtaposition (keyword)
  6. Formal academic language (multi-pattern: Furthermore, Moreover, per se, aforementioned, etc.)
  7. "It's worth noting" phrases (multi-pattern: notably, interestingly, etc.)
  8. Purple prose patterns (complex: adjective stacking 3+, melodramatic adverbs, pretentious vocabulary, enhanced dialogue tags)
  9. *(All patterns include concrete replacements)*
  10. Custom patterns (from YAML custom_patterns section)
- Records every match with:
  - Location (chapter, paragraph/line)
  - Matched text with context
  - Why it's AI-ish
  - 3-5 concrete replacement suggestions
- Generates `AI-DETECTION-REPORT.md` with:
  - Summary stats (total flags, most common, chapters affected)
  - Findings grouped by pattern
  - Context for each match
  - Specific replacement options
  - Next steps guidance
- Offers to create project-specific pattern database for customization

Created `ai-patterns.md` template (256 lines) with:
- 10 fully-defined built-in patterns
- Each pattern includes:
  - Category classification
  - Why AI-ish explanation
  - Detection logic (regex/keywords/complex patterns)
  - 3-5 concrete replacements with examples
- Pattern 6 & 8 with multiple sub-patterns
- Custom patterns YAML section with format examples
- Usage notes (context matters, genre considerations, STYLE.md integration)

Updated write skill index with detection command and voice authenticity features.

## Technical Implementation

**Files Created:**
1. `.planning/templates/ai-patterns.md` (256 lines)
   - Pattern 1-5: Simple keyword patterns with replacements
   - Pattern 6: Academic language (8 sub-patterns)
   - Pattern 7: Meta-commentary phrases (6 sub-patterns)
   - Pattern 8: Purple prose (5 sub-patterns)
   - Custom patterns YAML template
   - Comprehensive examples for each pattern

2. `.claude/skills/write/ai-detect.md` (411 lines)
   - Complete detection workflow
   - 3 scan scope options
   - Pattern loading with override support
   - Detailed scanning logic for each pattern type
   - Report generation format
   - Project-specific database creation
   - Extensive examples and Q&A

**Files Modified:**
1. `.claude/skills/write/SKILL.md`
   - Added `/write:detect` command
   - Updated skill overview to emphasize AI detection

## Deviations from Plan

None - plan executed exactly as written.

## Verification Results

✓ ai-patterns.md template exists with all 10 patterns defined
✓ Each pattern has detection logic, explanation, and 3-5 replacements
✓ Pattern 6 (formal language) includes multiple sub-patterns (Furthermore, Moreover, per se, aforementioned, etc.)
✓ Pattern 8 (purple prose) includes multiple sub-patterns (adjective stacking, melodramatic adverbs, etc.)
✓ Custom phrases section exists with YAML format example
✓ ai-detect.md workflow exists with scanning logic
✓ Detection scans chapters or pasted text
✓ Report includes location, context, why flagged, and suggestions
✓ Workflow offers to create project-specific pattern database
✓ SKILL.md updated with /write:detect command
✓ All files committed to git (3 commits)

## Requirements Fulfilled

- **AI-01:** System flags "delve/delved/delving" ✓
- **AI-02:** System flags "tapestry" (metaphorical) ✓
- **AI-03:** System flags "navigate/navigated" (metaphorical) ✓
- **AI-04:** System flags "testament to" ✓
- **AI-05:** System flags "juxtaposition" ✓
- **AI-06:** System flags overly formal academic language ✓
- **AI-07:** System flags "it's worth noting" and similar phrases ✓
- **AI-08:** System flags purple prose patterns ✓
- **AI-09:** System provides concrete replacement suggestions (3-5 per pattern) ✓
- **AI-10:** Writer can add custom phrases to detection list ✓

## Next Steps

Wave 1 complete (Plans 02-01, 02-02, 02-04).

Ready for Wave 2: Plan 02-03 (Word Count Tracking Enhancement), which depends on 02-02 and adds automatic word count tracking to the writing workflow.
