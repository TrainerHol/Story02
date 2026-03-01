# Discuss and Plan Writing Phase

Adaptive discussion workflow that asks clarifying questions before each writing phase, captures the writer's vision and decisions, and provides workflow orchestration guidance.

## What this does

This workflow conducts a guided discussion before starting a new phase of work (planning, writing, revision). It:
1. Validates the story project exists and phase number is valid
2. Detects phase type based on context (planning, writing, or revision)
3. Asks adaptive questions tailored to the phase goals
4. Captures decisions in PHASE-{N}-CONTEXT.md for reference
5. Provides clear next-step guidance for workflow progression

**Purpose:** Enable writers to clarify their goals and make decisions before diving into implementation. This reduces mid-phase confusion and ensures the writing aligns with the writer's vision.

**Similar to:** GSD's discuss-phase workflow - structured questioning that captures intent before execution.

## When to use this

Run `/write:discuss-phase N` before starting work on a new phase:

- **Phase 1 (Planning):** Before expanding YOLO premise or creating In-Depth plans
- **Phase 2+ (Writing):** Before drafting a new batch of chapters
- **Revision phases:** Before tackling consistency fixes or major revisions

**Frequency:** Use whenever you're ready to begin a distinct phase of work. For novel writing, you might run this 3-5 times: once for planning, 2-3 times for writing phases (batches of chapters), and once for final revision.

## Workflow

### Step 1: Validate Context

**Check project exists:**
```bash
# From working directory, verify story project structure
[ -f "PROJECT.md" ] || echo "Error: No PROJECT.md found. Run /write:new-project or /write:init first."
```

**Validate phase number:**
- Phase number should be 1-10 (typical range for most projects)
- Phase 1 is always planning/setup
- Phase 2+ depends on project progression

**Load existing context (if resuming):**
```bash
# Check if PHASE-{N}-CONTEXT.md already exists
[ -f "PHASE-${N}-CONTEXT.md" ] && echo "Found existing context - will offer to review and update"
```

**Read project metadata:**
```bash
# Load PROJECT.md to understand:
# - Story title and genre
# - Story length (short story, novella, novel)
# - Workflow mode (YOLO vs In-Depth)
# - Current word count and progress
```

**Display project context:**
```
[Discussion for: {STORY_TITLE}]
Genre: {GENRE} | Length: {LENGTH} | Mode: {WORKFLOW_MODE}
Current Progress: {WORD_COUNT} words | Phase {N} Discussion
```

### Step 2: Phase Detection

Based on phase number and project state, determine phase type:

**Phase 1: Planning/Setup**
- Occurs at project start
- Focus: story elements (characters, plot, world, arcs)
- Outputs: expanded premise, character profiles, outline, world-building

**Phase 2+: Writing/Drafting**
- Occurs after planning phase
- Focus: drafting chapters, scenes, narrative prose
- Outputs: chapter markdown files with story content

**Revision Phase Detection:**
- Check if CONSISTENCY-REPORT.md or AI-DETECTION-REPORT.md exists
- If writer mentions "revision", "fixing", "consistency", or "editing"
- Focus: addressing issues identified in reports
- Outputs: updated chapter files, resolved inconsistencies

**Auto-detection logic:**
```
if phase_number == 1:
    phase_type = "planning"
elif consistency_report_exists or ai_report_exists or "revision" in user_context:
    phase_type = "revision"
else:
    phase_type = "writing"
```

### Step 3: Adaptive Questions

Ask questions tailored to the detected phase type. Present numbered questions for clear flow.

#### For Planning Phases (Phase 1)

**Context setting:**
```
Phase 1: Planning & Story Foundation

Before we dive into development, let's clarify your approach for this phase.
This helps ensure we create the right planning depth for your workflow style.
```

**Questions:**

**Q1: What's your planning approach for this phase?**
```
Choose your approach:

A. YOLO Expand (Quick Start)
   - Start from vague premise and expand as you write
   - Minimal upfront planning
   - Discover story through drafting
   - Run /write:expand to develop premise
   - Best for: Discovery writers, experimental projects

B. In-Depth Planning (Comprehensive)
   - Detailed planning before drafting
   - Complete character profiles, outline, world-building
   - Full story blueprint before writing
   - Run /write:plan to create comprehensive foundation
   - Best for: Plotters, complex narratives, series

Which approach fits your style? (A or B)
```

**Q2: Which story elements will you develop in this phase?**
```
Select the areas you want to focus on (you can choose multiple):

1. Characters - Protagonists, antagonists, supporting cast
2. Plot Structure - Three-act outline, major beats, key scenes
3. Character Arcs - Transformation tracking from start to end
4. World Building - Setting, rules, culture, magic systems
5. Style & Voice - POV, tense, tone, narrative distance

Which elements are priorities? (e.g., "1, 2, 4" or "All")
```

**Q3: How much detail do you want?**
```
Planning depth:

- Light Sketches: Basic notes, room to improvise
- Moderate Detail: Clear direction with flexibility
- Comprehensive: Thorough development before drafting

Your preference?
```

**Q4: Any specific concerns or things to explore?**
```
Optional: Share any specific challenges, themes, or questions you want to address
during planning. For example:
- "Need to nail down the magic system rules"
- "Want to explore the mentor betrayal theme deeply"
- "Concerned about pacing for middle chapters"

(Leave blank if none)
```

#### For Writing Phases (Phase 2+)

**Context setting:**
```
Phase {N}: Chapter Drafting

Let's plan this writing phase. We'll identify which chapters to write, what plot
beats they'll cover, and any consistency concerns to watch for.
```

**Questions:**

**Q1: Which chapters will you write in this phase?**
```
Specify the chapters you plan to draft:

Examples:
- "Chapters 1-3" (range)
- "Chapter 5" (single)
- "Chapters 7, 8, 10" (specific set)

Which chapters?
```

**Q2: What plot beats from your outline will these chapters cover?**
```
Review your OUTLINE.md and identify the major story beats these chapters will include.

Examples:
- "Inciting incident and first plot point (Act 1)"
- "Midpoint reversal and rising action"
- "Climax and resolution"

Which beats?
```

**Q3: Are there any character arcs to focus on?**
```
Which characters undergo significant development in these chapters?

Examples:
- "Protagonist's journey from naive to determined"
- "Antagonist reveal and backstory"
- "Supporting character's betrayal arc"

Focus characters: (leave blank if no specific focus)
```

**Q4: Do you want to adjust pacing or style for these chapters?**
```
Any pacing or style considerations for this batch?

Examples:
- "Slower pacing for world-building in chapter 1"
- "Action-heavy for chapters 2-3"
- "Switch to villain POV for chapter 4"

Notes: (leave blank if following standard style)
```

**Q5: Any consistency concerns from previous chapters?**
```
If you've written chapters already, are there any continuity details to watch for?

Examples:
- "Make sure timeline matches - chapter 2 is Tuesday, not Monday"
- "Character X's eye color established as green in chapter 1"
- "Magic system rules from chapter 3 need to stay consistent"

Concerns: (leave blank if starting fresh or no concerns)
```

**Q6: Will you run /write:detect for AI language after writing?**
```
AI language detection helps identify and replace common AI patterns
(delve, tapestry, navigate, etc.) to maintain authentic human voice.

Plan to run /write:detect after this phase? (Yes/No/Maybe later)
```

#### For Revision Phases

**Context setting:**
```
Phase {N}: Revision & Refinement

Let's plan your revision work. We'll identify what needs fixing and which tools
to use for validation.
```

**Questions:**

**Q1: Which chapters need revision?**
```
Specify chapters to revise:

Examples:
- "All chapters" (full manuscript revision)
- "Chapters 1-5" (range)
- "Chapters 3, 7, 9" (specific chapters with issues)

Which chapters?
```

**Q2: What issues did you identify?**
```
What problems are you addressing in this revision?

Common issues:
- Plot holes or logical inconsistencies
- Character continuity errors (appearance, voice, personality)
- Timeline problems or event order confusion
- Pacing issues (too slow, too rushed)
- World rule violations
- POV inconsistencies
- AI language patterns that need replacement

Your issues:
```

**Q3: Will you use /write:check for consistency validation?**
```
The consistency checker scans all chapters for:
- Character detail contradictions
- Timeline continuity errors
- World rule violations
- POV shifts

Run /write:check to generate validation report? (Yes/No/Already ran it)
```

**Q4: Are you ready for export, or more drafting needed?**
```
After this revision phase:

A. Ready for /write:export - Compile finished manuscript
B. More drafting needed - Continue with additional writing phases

Which applies?
```

### Step 4: Capture Decisions

Create `PHASE-{N}-CONTEXT.md` in the story project directory with all captured information.

**File structure:**

```markdown
---
phase: {N}
phase_type: {planning|writing|revision}
created: {ISO timestamp}
updated: {ISO timestamp if resuming}
---

# Phase {N} Context

## Goals

{Bulleted list of what writer wants to accomplish this phase}

Example:
- Develop protagonist and antagonist character profiles
- Create three-act outline with major plot beats
- Establish magic system rules in WORLD.md

## Decisions

{Bulleted list of explicit decisions made during discussion}

Example:
- Planning approach: In-Depth (comprehensive)
- Focus areas: Characters, Plot Structure, World Building
- Detail level: Comprehensive development before drafting

## Focus Areas

{What to prioritize - specifics based on phase type}

**For Planning:**
- Story elements to develop: {list}
- Detail depth: {light|moderate|comprehensive}

**For Writing:**
- Chapters to draft: {range or list}
- Plot beats covered: {description}
- Character arcs: {focus characters}
- Pacing notes: {any adjustments}
- Consistency watch: {concerns from previous chapters}

**For Revision:**
- Chapters to revise: {range or list}
- Issues to address: {specific problems}
- Validation tools: {which commands to run}

## Concerns

{Optional - anything to watch for or address}

Example:
- Need to ensure magic system rules are consistent from chapter 1
- Timeline needs careful tracking - story spans 3 weeks
- Watch for POV slips in villain chapters

## Next Steps

{Specific actionable steps based on discussion and phase type}

Example:
1. Run /write:expand to develop YOLO premise into structured outline
2. Run /write:style to define writing voice from sample paragraphs
3. Run /write:discuss-phase 2 when ready to start chapter drafting
```

**Resume support:**

If PHASE-{N}-CONTEXT.md already exists:
1. Display existing context at start of discussion
2. Ask: "Would you like to review and update your decisions, or start fresh?"
3. If updating: preserve previous decisions with "Updated:" timestamps
4. If fresh: archive old context to PHASE-{N}-CONTEXT.archive.md

### Step 5: Workflow Orchestration Guidance

After capturing decisions, provide clear next-step guidance based on phase type.

**For Planning Phases (Phase 1):**

**If YOLO mode selected:**
```
Next Steps for YOLO Planning:

1. Run /write:expand
   - This will transform your premise into a workable story foundation
   - Creates basic character sketches and simple plot structure
   - Enables rapid transition to writing

2. (Optional) Run /write:style
   - Define your writing voice through sample analysis
   - Helps chapters match your authentic style
   - Recommended before drafting

3. When ready to write: Run /write:discuss-phase 2
   - This will help you plan which chapters to draft first
   - Ensures smooth transition from planning to writing

Estimated time for YOLO expand: 15-30 minutes
```

**If In-Depth mode selected:**
```
Next Steps for In-Depth Planning:

1. Run /write:plan
   - This will guide you through comprehensive story development
   - Creates detailed CHARACTERS.md, OUTLINE.md, ARCS.md, WORLD.md
   - Provides complete story blueprint before drafting

2. Run /write:style (recommended)
   - Define your writing voice through sample analysis
   - Ensures chapters match your authentic style

3. (Optional) Run /write:pacing
   - Get story-length adapted pacing recommendations
   - Learn optimal chapter count and act breakdown

4. When ready to write: Run /write:discuss-phase 2
   - Plan your first batch of chapters
   - Transition smoothly from planning to drafting

Estimated time for In-Depth planning: 1-3 hours depending on detail depth
```

**For Writing Phases (Phase 2+):**

```
Next Steps for Chapter Drafting:

1. Start drafting: Run /write:chapter {first_chapter_number}
   - This will generate your first chapter with full story context
   - Matches your STYLE.md, maintains character voices
   - Adapts length to your story type

2. Continue drafting: Run /write:chapter {N} for each subsequent chapter
   - Work through your planned chapter list
   - Take breaks as needed - context is preserved

3. After 2-3 chapters: Consider running /write:detect
   - Scans for AI language patterns (delve, tapestry, etc.)
   - Provides concrete replacement suggestions
   - Helps maintain authentic human voice

4. After 5+ chapters: Run /write:check
   - Validates consistency across chapters
   - Catches character detail contradictions
   - Identifies timeline continuity errors
   - Flags world rule violations

5. When this phase complete: Run /write:discuss-phase {N+1}
   - Plan your next batch of chapters
   - Or transition to revision if drafting complete

Estimated time per chapter: 20-45 minutes depending on length
```

**For Revision Phases:**

```
Next Steps for Revision:

1. Generate validation report: Run /write:check
   - Scans all chapters for consistency violations
   - Identifies character, timeline, world, and POV issues
   - Creates CONSISTENCY-REPORT.md with detailed findings

2. Address identified issues:
   - Review CONSISTENCY-REPORT.md findings
   - Update affected chapter files
   - Resolve contradictions and continuity errors

3. (Optional) Run /write:detect for AI language
   - Scan for common AI patterns if not done yet
   - Get replacement suggestions for flagged phrases
   - Ensure authentic human voice throughout

4. Re-validate: Run /write:check again
   - Confirm fixes resolved the issues
   - Ensure no new problems introduced

5. When satisfied: Run /write:export
   - Compile finished manuscript in submission format
   - Choose markdown, plain text, or standard manuscript format
   - Generate professional title page

Estimated time for revision: 1-4 hours depending on issue count
```

### Step 6: Confirmation and Summary

After providing next steps, display a summary for writer confirmation:

```
Phase {N} Discussion Summary:

Phase Type: {planning|writing|revision}
Goals: {concise list}
Next Command: /write:{command}
Context File: PHASE-{N}-CONTEXT.md created ✓

Ready to proceed with these plans? (The context has been saved for reference)
```

## Presentation Style

**Use clear, encouraging language:**
- Numbered questions for logical flow
- Show current project context at start (title, genre, progress)
- Format options clearly with bullets and examples
- Use **bold** for emphasis on key choices
- Provide concrete examples where helpful
- Keep tone supportive and judgment-free

**Avoid:**
- Overwhelming with too many questions at once
- Jargon without explanation
- Prescriptive language ("you should")
- Making assumptions about writer's process

## Error Handling

**Project not found:**
```
Error: No story project found in current directory.

You need to initialize a project first. Run one of these commands:

- /write:new-project (Recommended: Guided setup with clear options)
- /write:init (Advanced: Quick direct setup)

Then run /write:discuss-phase 1 to begin planning.
```

**Invalid phase number:**
```
Warning: Phase {N} seems unusual for this project.

Current state: {describe based on what files exist}
Typical flow: Phase 1 (planning) → Phase 2+ (writing) → Revision

Is Phase {N} correct? Or did you mean a different phase number?
```

**Missing planning files for writing phase:**
```
Notice: Starting Phase {N} writing, but planning files are minimal.

Missing: {list - CHARACTERS.md, OUTLINE.md, etc.}

Recommendations:
- Consider running /write:expand (YOLO) or /write:plan (In-Depth) first
- Or proceed with discovery writing if that's your style

Continue anyway? (Yes/No)
```

## Resume Support

If `PHASE-{N}-CONTEXT.md` already exists:

**Display existing context:**
```
Found Existing Phase {N} Context:

Created: {original timestamp}
Goals: {bulleted list from file}
Decisions: {bulleted list from file}

Would you like to:
A. Review and update these decisions
B. Start fresh (archives previous context)
C. Cancel and continue with existing plan

Your choice? (A, B, or C)
```

**If updating (A):**
- Load existing context as defaults
- Allow writer to modify any section
- Add "Updated: {timestamp}" markers to changed sections
- Preserve original decisions in "Previous Decisions" section

**If starting fresh (B):**
- Move PHASE-{N}-CONTEXT.md to PHASE-{N}-CONTEXT.archive.{timestamp}.md
- Create new context from scratch
- Include note: "Previous context archived to {filename}"

**If canceling (C):**
- Exit without changes
- Remind writer they can continue with existing plan

## Integration with Other Commands

**Reads from:**
- `PROJECT.md` - Story metadata, progress, goals
- `PHASE-{N}-CONTEXT.md` - Existing context if resuming
- `CONSISTENCY-REPORT.md` - Detect revision phase
- `AI-DETECTION-REPORT.md` - Detect revision phase
- `chapters/*.md` - Understand current chapter progress

**Creates:**
- `PHASE-{N}-CONTEXT.md` - Captured decisions and next steps

**References in guidance:**
- `/write:expand` - YOLO planning
- `/write:plan` - In-Depth planning
- `/write:style` - Voice definition
- `/write:chapter` - Chapter drafting
- `/write:detect` - AI language detection
- `/write:check` - Consistency validation
- `/write:pacing` - Length-adapted pacing guidance
- `/write:export` - Manuscript compilation

## Duration

**Typical discussion time:** 10-20 minutes depending on phase complexity

- Planning phases: 15-20 minutes (more decisions to make)
- Writing phases: 10-15 minutes (straightforward chapter planning)
- Revision phases: 10-12 minutes (focused on specific fixes)

## Example Output

### Example: Planning Phase Discussion

```
[Discussion for: The Crimson Prophecy]
Genre: Fantasy | Length: Novel | Mode: Not set
Current Progress: 0 words | Phase 1 Discussion

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Phase 1: Planning & Story Foundation

Before we dive into development, let's clarify your approach for this phase.
This helps ensure we create the right planning depth for your workflow style.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q1: What's your planning approach for this phase?

Choose your approach:

A. YOLO Expand (Quick Start)
   - Start from vague premise and expand as you write
   - Minimal upfront planning
   - Discover story through drafting
   - Run /write:expand to develop premise
   - Best for: Discovery writers, experimental projects

B. In-Depth Planning (Comprehensive)
   - Detailed planning before drafting
   - Complete character profiles, outline, world-building
   - Full story blueprint before writing
   - Run /write:plan to create comprehensive foundation
   - Best for: Plotters, complex narratives, series

Which approach fits your style? (A or B)

> User: B

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q2: Which story elements will you develop in this phase?

Select the areas you want to focus on (you can choose multiple):

1. Characters - Protagonists, antagonists, supporting cast
2. Plot Structure - Three-act outline, major beats, key scenes
3. Character Arcs - Transformation tracking from start to end
4. World Building - Setting, rules, culture, magic systems
5. Style & Voice - POV, tense, tone, narrative distance

Which elements are priorities? (e.g., "1, 2, 4" or "All")

> User: All

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q3: How much detail do you want?

Planning depth:

- Light Sketches: Basic notes, room to improvise
- Moderate Detail: Clear direction with flexibility
- Comprehensive: Thorough development before drafting

Your preference?

> User: Comprehensive

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q4: Any specific concerns or things to explore?

Optional: Share any specific challenges, themes, or questions you want to address
during planning. For example:
- "Need to nail down the magic system rules"
- "Want to explore the mentor betrayal theme deeply"
- "Concerned about pacing for middle chapters"

> User: Need to nail down the magic system rules and ensure they're consistent

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Phase 1 Discussion Summary:

Phase Type: Planning
Goals:
  - Comprehensive In-Depth planning before drafting
  - Develop all story elements (characters, plot, arcs, world, style)
  - Thorough detail depth across all areas
  - Special focus on magic system consistency

Next Command: /write:plan
Context File: PHASE-1-CONTEXT.md created ✓

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Next Steps for In-Depth Planning:

1. Run /write:plan
   - This will guide you through comprehensive story development
   - Creates detailed CHARACTERS.md, OUTLINE.md, ARCS.md, WORLD.md
   - Provides complete story blueprint before drafting

2. Run /write:style (recommended)
   - Define your writing voice through sample analysis
   - Ensures chapters match your authentic style

3. (Optional) Run /write:pacing
   - Get story-length adapted pacing recommendations
   - Learn optimal chapter count and act breakdown

4. When ready to write: Run /write:discuss-phase 2
   - Plan your first batch of chapters
   - Transition smoothly from planning to drafting

Estimated time for In-Depth planning: 1-3 hours depending on detail depth

Ready to proceed with these plans?
```

### Example: Writing Phase Discussion

```
[Discussion for: The Crimson Prophecy]
Genre: Fantasy | Length: Novel | Mode: In-Depth
Current Progress: 0 words | Phase 2 Discussion

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Phase 2: Chapter Drafting

Let's plan this writing phase. We'll identify which chapters to write, what plot
beats they'll cover, and any consistency concerns to watch for.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q1: Which chapters will you write in this phase?

Specify the chapters you plan to draft:

Examples:
- "Chapters 1-3" (range)
- "Chapter 5" (single)
- "Chapters 7, 8, 10" (specific set)

> User: Chapters 1-5

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q2: What plot beats from your outline will these chapters cover?

Review your OUTLINE.md and identify the major story beats these chapters will include.

Examples:
- "Inciting incident and first plot point (Act 1)"
- "Midpoint reversal and rising action"
- "Climax and resolution"

> User: Full Act 1 - ordinary world, inciting incident, first plot point

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q3: Are there any character arcs to focus on?

Which characters undergo significant development in these chapters?

Examples:
- "Protagonist's journey from naive to determined"
- "Antagonist reveal and backstory"
- "Supporting character's betrayal arc"

> User: Protagonist discovers her powers and begins training

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q4: Do you want to adjust pacing or style for these chapters?

Any pacing or style considerations for this batch?

Examples:
- "Slower pacing for world-building in chapter 1"
- "Action-heavy for chapters 2-3"
- "Switch to villain POV for chapter 4"

> User: Slower pacing for chapter 1 world-building, pick up pace by chapter 3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q5: Any consistency concerns from previous chapters?

> User: (blank - starting fresh)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Q6: Will you run /write:detect for AI language after writing?

AI language detection helps identify and replace common AI patterns
(delve, tapestry, navigate, etc.) to maintain authentic human voice.

> User: Yes

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Phase 2 Discussion Summary:

Phase Type: Writing
Goals:
  - Draft chapters 1-5 (Act 1 completion)
  - Cover plot beats: ordinary world, inciting incident, first plot point
  - Focus on protagonist's power discovery and training arc
  - Pacing: slower chapter 1, accelerate by chapter 3
  - Plan to run /write:detect after drafting

Next Command: /write:chapter 1
Context File: PHASE-2-CONTEXT.md created ✓

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Next Steps for Chapter Drafting:

1. Start drafting: Run /write:chapter 1
   - This will generate your first chapter with full story context
   - Matches your STYLE.md, maintains character voices
   - Adapts length to your story type

2. Continue drafting: Run /write:chapter {N} for each subsequent chapter
   - Work through chapters 2-5
   - Take breaks as needed - context is preserved

3. After chapters complete: Run /write:detect
   - Scans for AI language patterns (delve, tapestry, etc.)
   - Provides concrete replacement suggestions
   - Helps maintain authentic human voice

4. After 5 chapters: Run /write:check
   - Validates consistency across chapters
   - Catches character detail contradictions
   - Identifies timeline continuity errors

5. When Act 1 complete: Run /write:discuss-phase 3
   - Plan your next batch of chapters (Act 2)
   - Continue your story progression

Estimated time per chapter: 20-45 minutes depending on length

Ready to start chapter 1?
```
