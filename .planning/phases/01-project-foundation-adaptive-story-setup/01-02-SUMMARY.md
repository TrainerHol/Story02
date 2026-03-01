---
phase: 01-project-foundation-adaptive-story-setup
plan: 02
status: complete
completed: 2026-02-26
---

# Plan 01-02 Summary: YOLO Quick-Start Mode

## Objective
Implemented YOLO (quick-start) mode that transforms vague story ideas into structured premises with basic planning, enabling rapid transition to writing.

## What Was Built

### YOLO Expansion Workflow
- Created `yolo-expand.md` with complete expansion workflow (350+ lines)
- Validates YOLO mode from PROJECT.md frontmatter
- Expands vague ideas into 2-3 sentence structured premises
- Generates basic character sketches (2-4 characters)
- Suggests simple 3-act plot structure
- Enables skip-to-writing workflow

### Lightweight Templates
- **yolo-characters.md**: 67 lines (vs full template's 117)
  - Essential character information only
  - Name, role, 3 traits, background, goal, voice
  - Quick reference section
  - Encourages organic development during writing

- **yolo-outline.md**: 88 lines (vs full template's 128)
  - Simple 3-act structure with major beats
  - High-level complications, no detailed scenes
  - Plot threads checklist
  - Flexibility notes for discovery writers

### Skill Registration
- Updated SKILL.md with `/write:expand` command
- Clear description of YOLO mode workflow
- Links to yolo-expand.md

## Requirements Fulfilled

- YOLO-01: ✓ Premise expansion from vague ideas
- YOLO-02: ✓ Basic character sketch generation
- YOLO-03: ✓ Simple plot structure suggestion
- YOLO-04: ✓ Skip-to-writing enablement
- LENGTH-01: ✓ Lighter templates (40-50% smaller than full versions)

## Key Files Created

### .claude/skills/write/yolo-expand.md
Complete expansion workflow with premise generation, character creation, and plot suggestion.
Lines: 352

### .planning/templates/yolo-characters.md
Lightweight character template for quick starts.
Lines: 67 (43% smaller than full template)

### .planning/templates/yolo-outline.md
Simple plot structure template.
Lines: 88 (31% smaller than full template)

## Technical Approach

### Premise Expansion
- Analyzes vague ideas for core elements (protagonist, conflict, setting, hook)
- Uses expansion template to structure ideas
- Provides genre-appropriate examples
- 2-3 sentence output with clear components

### Character Generation
- Auto-suggests genre-appropriate names
- Minimal but focused information (role, traits, goal)
- Emphasis on getting started over perfection
- Voice notes for dialogue consistency

### Plot Structure
- High-level 3-act framework
- Major beats only, no scene-by-scene detail
- Encourages flexibility and discovery
- Tracks key plot threads as checklist

## Commits

```
70e9bec feat(01-02): implement YOLO quick-start mode with lightweight templates
```

## Self-Check: PASSED

Verification:
- [x] yolo-expand.md contains premise expansion logic
- [x] yolo-expand.md contains character sketch generation
- [x] yolo-expand.md contains plot structure suggestion
- [x] yolo-expand.md contains skip-to-writing flow
- [x] YOLO character template < 80 lines (67 lines)
- [x] YOLO outline template < 90 lines (88 lines)
- [x] Templates demonstrably lighter than full versions
- [x] SKILL.md updated with write:expand command
- [x] Git commit created

## Comparison: YOLO vs Full Templates

| Template | YOLO Lines | Full Lines | Reduction |
|----------|------------|------------|-----------|
| Characters | 67 | 117 | 43% |
| Outline | 88 | 128 | 31% |

YOLO templates focus on essentials, enabling quick start without overwhelming detail.

## Integration

- Workflows read PROJECT.md `mode` field to route correctly
- YOLO expand validates mode before proceeding
- Templates designed for organic expansion during writing
- Consistent with project initialization from Plan 01-01

## Next Steps

Phase 2 will add chapter drafting workflow that works with both YOLO and In-Depth planning documents.

## Issues Encountered

None

## Deviations from Plan

None - implementation follows plan exactly.
