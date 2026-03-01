---
phase: 01-project-foundation-adaptive-story-setup
plan: 03
status: complete
completed: 2026-02-26
---

# Plan 01-03 Summary: In-Depth Planning Mode

## Objective
Implemented In-Depth planning mode with comprehensive story development templates and length-aware sections, enabling detailed preparation for complex narratives.

## What Was Built

### In-Depth Planning Workflow
- Created `indepth-plan.md` with complete guided planning (610+ lines)
- Validates In-Depth mode from PROJECT.md frontmatter
- Reads story length for template depth adaptation
- Comprehensive prompting through all planning areas:
  - Character Development (STORY-01)
  - Plot Structure (STORY-02)
  - Character Arcs (STORY-03)
  - World-Building (STORY-04)
  - Themes and Motifs (STORY-05)

### Length-Aware Template System
Enhanced all five full templates with `<!--LENGTH:novel-->` markers:

**story-project.md:**
- Development Notes section (novel only)
- Detailed Notes section (novel only)

**characters.md:**
- Character Relationships section (novel only)
- Detailed Notes and consistency tracking (novel only)

**outline.md:**
- Subplots section (novel only)
- Pacing Notes (novel only)
- Detailed Scene List (novel only)

**arcs.md:**
- 4th and 5th growth moments (novel only - short stories use 3)
- Detailed Tracking checklist (novel only)

**world.md:**
- History timeline and backstory (novel only)
- Religion/Language culture details (novel only)
- Consistency Tracking section (novel only)

### Skill Registration
- Updated SKILL.md with `/write:plan` command
- Description emphasizes comprehensive planning
- Links to indepth-plan.md

## Requirements Fulfilled

- STORY-01: ✓ Detailed character profiles (name, role, personality, background, voice)
- STORY-02: ✓ Plot structure with major beats and subplots
- STORY-03: ✓ Character arc definition and transformation tracking
- STORY-04: ✓ World-building documentation (setting, rules, culture, geography)
- STORY-05: ✓ Themes and motifs captured in PROJECT.md
- LENGTH-02: ✓ Novel-length projects use extensive planning depth with all template sections

## Key Files Created

### .claude/skills/write/indepth-plan.md
Comprehensive guided planning workflow with conversational prompting.
Lines: 614

### Enhanced Templates (with LENGTH markers)
All five templates now adapt depth based on story length:
- story-project.md: Enhanced with length-aware development tracking
- characters.md: Relationships and detailed notes for novels
- outline.md: Subplots, pacing, detailed scenes for novels
- arcs.md: 5+ growth moments and tracking for novels
- world.md: History, culture details, consistency tracking for novels

## Technical Approach

### Length-Aware Processing
```
if LENGTH=novel:
  Include all sections (full template)
else if LENGTH=novella:
  Skip LENGTH:novel sections (moderate depth)
else if LENGTH=short-story:
  Skip LENGTH:novel sections (core only)
```

### Template Depth by Length

**Short story (< 7,500 words):**
- 2-3 characters, core sections only
- Simple 3-act structure
- 3 growth moments
- Basic setting
- No subplots, history, or detailed tracking

**Novella (7,500-40,000 words):**
- 3-4 characters, moderate detail
- Three acts with moderate scenes
- 4-5 growth moments
- Moderate world-building
- 1-2 subplots if relevant

**Novel (40,000+ words):**
- 4+ characters, full detail
- Comprehensive structure with scenes
- 5-7 growth moments
- Full world-building with history
- Multiple subplots
- All tracking sections

### Conversational Prompting Style
- Shows examples for each question
- Allows "skip" for optional sections
- Confirms understanding
- Encourages depth where appropriate
- 30-60 minute estimated time investment

## Commits

```
f016bae feat(01-03): implement In-Depth planning with length-aware templates
```

## Self-Check: PASSED

Verification:
- [x] indepth-plan.md contains character development prompting (STORY-01)
- [x] indepth-plan.md contains plot structure prompting (STORY-02)
- [x] indepth-plan.md contains character arc prompting (STORY-03)
- [x] indepth-plan.md contains world-building prompting (STORY-04)
- [x] indepth-plan.md contains themes/motifs in PROJECT.md (STORY-05)
- [x] indepth-plan.md has LENGTH-aware template selection logic (LENGTH-02)
- [x] All five templates have LENGTH:novel markers
- [x] story-project.md contains LENGTH_MARKER
- [x] characters.md contains LENGTH_MARKER
- [x] SKILL.md updated with write:plan command
- [x] Git commit created

## Length-Aware Sections Summary

| Template | Novel-Only Sections | Core Sections |
|----------|---------------------|---------------|
| story-project.md | Development Notes, Notes | Metadata, Premise, Themes, Progress |
| characters.md | Relationships, Detailed Notes | Character profiles, Traits, Goals |
| outline.md | Subplots, Pacing, Scene List | 3-act structure, Major beats |
| arcs.md | Growth moments 4-5, Tracking | Arc type, 3 core moments, Endpoints |
| world.md | History, Religion/Language, Consistency | Setting, World rules, Geography |

## Integration

- Workflows read PROJECT.md `mode` and `length` fields
- In-Depth plan validates mode before proceeding
- Templates conditionally include sections based on length
- Consistent with initialization from Plan 01-01
- Complementary to YOLO mode from Plan 01-02

## Next Steps

Phase 2 will add chapter drafting that leverages these planning documents for consistency and voice.

## Issues Encountered

None

## Deviations from Plan

None - implementation follows plan exactly. LENGTH markers implemented as specified for adaptive template depth.
