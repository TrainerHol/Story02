---
name: write
description: Commands for creative writing workflow - story development from initialization through drafting and revision. Supports both quick-start (YOLO) and detailed planning (In-Depth) modes, with adaptive templates for different story lengths. Includes phase-based workflow orchestration with adaptive discussions before planning, writing, and revision phases. Tracks full story context across chapters with style matching, consistency checking, pacing guidance, and manuscript export features.
---

# Write - Story Development Skill

Commands for structured creative writing workflow with context-aware chapter generation.

## Commands

### `/write:new-project`
Initialize new story project with guided setup

Comprehensive project initialization with clarifying questions and option presentation. Asks about story length (short story, novella, novel), workflow mode (YOLO vs In-Depth), genre, premise, and optional goals. Creates project directory with all necessary template files. Provides clear next steps based on your choices.

This is the recommended starting point for new users. Experience similar to GSD's new-project workflow with clear option presentation, validation, and guidance.

See: new-project.md

### `/write:init`
Initialize new story project (quick setup)

Direct project initialization for advanced users who know their preferences. Creates project directory structure and captures foundational story information (title, genre, premise, story length, workflow mode) with minimal prompting.

See: init-project.md

### `/write:discuss-phase N`
Discuss and plan upcoming writing phase

Adaptive discussion workflow that asks clarifying questions based on phase goals. For planning phases: asks about story elements to develop. For writing phases: asks which chapters to write, plot beats to cover, and consistency concerns. Creates PHASE-N-CONTEXT.md capturing decisions and provides clear next-step guidance. Run before starting each new phase of work.

See: discuss-phase.md

### `/write:expand`
Expand YOLO project from vague idea to structured premise

For YOLO mode projects: transforms fuzzy concepts into workable premises with basic character sketches and simple plot structure. Enables rapid transition to writing.

See: yolo-expand.md

### `/write:plan`
Create detailed story planning (In-Depth mode)

For In-Depth mode projects: comprehensive story planning with detailed character profiles, complete plot outline with beats, character arcs, world-building documentation, and theme definition. Creates CHARACTERS.md, OUTLINE.md, ARCS.md, WORLD.md, and THEMES.md. Provides structured framework before writing begins.

See: indepth-plan.md

### `/write:style-seed`
Analyze writing samples and define voice (STYLE.md)

Define your writing style through sample analysis and voice configuration. Analyzes 2-3 sample paragraphs for measurable patterns (sentence length, vocabulary level, tone markers) and combines with explicit voice preferences (POV, tense, formality, narrative distance). Creates STYLE.md profile for use in chapter generation.

See: style-seed.md

### `/write:chapter`
Generate chapters and scenes with story context (chapters/*.md)

Write chapters with full story awareness - matches your style seed, maintains character voices, tracks plot threads, and adapts output length to story type. Loads STYLE.md, CHARACTERS.md, OUTLINE.md, ARCS.md, WORLD.md, and existing chapters for consistency. Generates prose scene-by-scene for long chapters or single-pass for short chapters.

See: write-chapter.md

### `/write:detect`
Scan prose for AI language patterns (AI-DETECTION-REPORT.md)

Analyze your chapters for 24+ common AI language patterns including 'delve', 'tapestry', 'navigate', 'testament to', 'juxtaposition', overly formal academic language, "it's worth noting" phrases, purple prose excess, and many more. Get concrete replacement suggestions (3-5 alternatives per match) with context. Add custom phrases to watch for via AI-PATTERNS.md customization.

See: ai-detect.md

### `/write:check-consistency`
Scan story for consistency violations (CONSISTENCY-REPORT.md)

Scan your story for consistency violations across all chapters. Checks character details (appearance, voice, personality), timeline continuity, world rule adherence, and POV consistency. Loads CHARACTERS.md, WORLD.md, and all chapters to detect contradictions. Generates CONSISTENCY-REPORT.md with flagged issues, locations, and suggestions. Run after writing 3-5 chapters or before major revisions to catch plot holes and continuity errors.

See: check-consistency.md

### `/write:pacing`
Get length-adapted pacing guidance (PACING-GUIDE.md)

Get story-specific pacing recommendations based on your word count goal and story type. Suggests appropriate chapter count (short story: 1-3, novella: 5-15, novel: 15-30, epic: 30+), provides act-based pacing breakdown adapted to your story length, and offers chapter length targets. Analyzes your OUTLINE.md structure and genre to provide tailored guidance. Updates PROJECT.md with recommended structure.

See: pacing-guide.md

### `/write:export`
Export manuscript in professional formats

Export individual chapters or compile full manuscript in submission-ready formats. Supports markdown (.md), plain text (.txt), and standard manuscript format (.txt with industry conventions). Compiles chapters in sequence, generates professional title pages, applies proper formatting (headers, scene breaks, page structure). Choose single chapter export, chapter range, or full manuscript. Output to exports/ directory with automatic timestamping.

See: export.md

## Character Management

### `/write:character <name>`
View character profile from persistent bank

Query the character bank to view full profile for any character. Character bank lives in `.writing/characters/` and persists across all chapters. If character not in bank yet, offers to populate from CHARACTERS.md or create new entry. Use this to reference character details before writing scenes to ensure consistency. Essential for maintaining consistent voice, appearance, and behavior across chapters.

**Retrieves:** Full character profile with appearance locks, voice markers, behavior patterns, goals, arc, and chapter references
**When to use:** Before writing chapters, when referencing character details, to check consistency
**Duration:** < 1 minute

See: character-bank.md

### `/write:update-character <name>`
Update character details in bank

Modify character profile in the bank: appearance, personality, voice markers, consistency locks, background, goals, arc. Updates timestamp and preserves existing information. Use after chapters where character develops or new details are revealed. Maintains single source of truth for character consistency.

**Updates:** Any section of character profile (appearance, personality, background, goals, arc, chapter references)
**When to use:** After character development moments, when new details revealed, to add chapter references
**Duration:** 3-8 minutes depending on scope

See: character-bank.md

### `/write:populate-bank`
Auto-populate character bank from CHARACTERS.md

Create character bank entries automatically from existing CHARACTERS.md or yolo-characters.md file. Runs during project initialization or on-demand. Extracts character information and creates `.writing/characters/{slug}.md` files with comprehensive format. Initializes empty sections for consistency notes and chapter references.

**Creates:** Character bank files in `.writing/characters/` directory
**When to use:** During project setup, after planning phase, before writing first chapter
**Duration:** 5-15 minutes depending on character count

See: character-bank.md

## Version Control

### `/write:revisions <chapter-name>`
View chapter revision history

Display all saved versions of a chapter with timestamps, word counts, and notes. Shows version number, date, time, word count, change summary, and revision notes. Use this to track chapter development and decide if rollback is needed. Revisions are saved automatically every time a chapter is updated.

**Shows:** Version history table with metadata, current version indicator, change summaries
**When to use:** After multiple chapter revisions, before restoring version, to track chapter evolution
**Duration:** < 1 minute

See: chapter-versions.md

### `/write:restore <chapter-name> <version>`
Restore previous chapter version

Roll back a chapter to a previous version. Shows preview before restoring. Current version is automatically saved as a new revision so no work is lost. Use when a revision didn't work out and you want to return to an earlier draft. Safe experimentation—all versions preserved.

**Restores:** Any previous chapter version to current
**Safety:** Current version saved before restore, no data lost
**When to use:** After unsuccessful revision, to compare different approaches, to recover earlier draft
**Duration:** 1-2 minutes

See: chapter-versions.md

### `/write:diff <chapter-name> <v1> <v2>`
Compare two chapter versions

View differences between two versions of a chapter. Shows word count changes and paragraph-level additions/deletions in human-readable format. Use to understand what changed between revisions. Helps identify improvement patterns and revision effectiveness.

**Shows:** Word count delta, paragraph-level changes (added/removed/modified), change summaries
**When to use:** To see evolution from first draft to current, to compare recent revisions, to learn revision patterns
**Duration:** 2-5 minutes

See: chapter-versions.md

### Future Commands

<!-- Placeholder for future commands -->
<!-- `/write:plan` - Complete In-Depth story planning (Phase 1 Plan 03) -->
<!-- `/write:chapter` - Draft new chapter -->
<!-- `/write:revise` - Revision workflow -->
<!-- `/write:detect-ai` - Detect and highlight AI language patterns -->

## When to use this skill

- Starting a new story project (short story, novella, or novel)
- Developing characters, plot, and world-building
- Managing persistent character database for consistency across chapters
- Defining your unique writing style through sample analysis
- Drafting chapters with consistent voice and style matching
- Tracking chapter revisions with automatic version control
- Detecting and removing AI-generated language patterns
- Checking story consistency (character details, timeline, world rules, POV)
- Getting length-adapted pacing guidance and chapter recommendations
- Comparing chapter versions and restoring previous drafts
- Exporting finished manuscripts in professional formats
- Revising to ensure authentic human voice
- Maintaining story consistency across chapters

## Complete Workflow

**New Project:** `/write:new-project` → discuss → plan → write → revise → export

**Typical Flow:**
1. `/write:new-project` - Initialize with guided setup
2. `/write:discuss-phase 1` - Clarify planning approach
3. `/write:expand` (YOLO) or `/write:plan` (In-Depth) - Develop story foundation
4. `/write:style-seed` - Define writing voice (optional but recommended)
5. `/write:populate-bank` - Create character bank from CHARACTERS.md (optional but recommended)
6. `/write:discuss-phase 2` - Plan writing phase (which chapters, focus areas)
7. `/write:chapter N` - Draft chapters (automatically references character bank, saves revisions)
8. `/write:character <name>` - Query character details as needed during writing
9. `/write:revisions <chapter>` - View chapter history if needed
10. `/write:detect` - Check for AI language patterns
11. `/write:check-consistency` - Validate consistency
12. `/write:discuss-phase 3` - Plan revisions if needed
13. `/write:restore <chapter> <version>` - Roll back if needed during revisions
14. `/write:export` - Compile finished manuscript

Repeat steps 5-8 for additional writing phases as story develops.

**Starting point:** Run `/write:new-project` for guided setup with clear options, or `/write:init` for quick direct setup.

## Workflow modes

**YOLO mode:** Quick start from vague ideas, minimal upfront planning, discover story through writing
**In-Depth mode:** Comprehensive planning before drafting, detailed character/plot/world development
