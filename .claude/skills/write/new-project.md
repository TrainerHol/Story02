# Initialize New Story Project (Comprehensive)

Create a new story project with guided initialization that asks clarifying questions and presents clear options, similar to GSD's new-project experience.

## What this does

This comprehensive workflow:
1. Welcomes writer and explains the initialization process
2. Asks clarifying questions with clear option presentation
3. Validates inputs and checks for conflicts
4. Creates project structure with appropriate templates
5. Provides clear next-step guidance based on selections

This is the recommended entry point for new users. Advanced users can use `/write:init` for direct initialization.

## Workflow

### Step 1: Welcome and Overview

Present welcome message:

```
Welcome to Claudespeare Story Initialization!

Let's set up your new story project. This takes 5-10 minutes and will ask you questions about:
- Your story's title and basic details
- The length you're planning (short story, novella, or novel)
- Your workflow preference (quick start vs detailed planning)
- Genre and premise

At each step, you'll see clear options to choose from. Ready to begin?
```

### Step 2: Gather Story Title

**Question:** "What's your story title?"

**Prompt:**
```
Story Title:
Enter the working title for your story. You can change this later in PROJECT.md if needed.

Examples:
- "The Crimson Prophecy"
- "Lost in Translation"
- "Beneath the Surface"
```

**Validation:**
1. Check title is not empty
2. Create slug from title: lowercase, replace non-alphanumeric with hyphens, collapse multiple hyphens
3. Check if `stories/{slug}/` directory already exists
4. If exists, display error:
   ```
   Error: A project with slug '{slug}' already exists at stories/{slug}/

   Suggestions:
   - Try a different title variation (e.g., "My Story V2", "My Story Revised")
   - Or specify the existing project if you meant to continue working on it
   ```
5. Allow retry without losing context

**Store:** `TITLE` (original), `SLUG` (slugified)

### Step 3: Present Story Length Options

**Question:** "What length are you planning?"

**Option Presentation:**
```
Story Length:

Choose the length that best fits your story vision. This determines template depth and planning guidance.

1. Short Story (1,000-7,500 words)
   - Quick, focused narrative
   - Single plotline with tight pacing
   - Minimal character development
   - Lighter planning templates
   - Best for: Flash fiction, focused scenes, experimental concepts

2. Novella (7,500-40,000 words)
   - Extended single plotline
   - 2-3 core characters with development
   - Room for subplots
   - Moderate planning depth
   - Best for: Extended narratives, character studies, novelettes

3. Novel (40,000-100,000+ words)
   - Full-length with multiple subplots
   - Complex character arcs
   - Rich world-building
   - Comprehensive planning templates
   - Best for: Expansive stories, series foundations, epic narratives

Which length matches your vision? (1, 2, or 3)
```

**Validation:**
- Must select 1, 2, or 3
- If invalid, re-prompt with "Please enter 1, 2, or 3"

**Store:** `LENGTH` (one of: `short-story`, `novella`, `novel`)

### Step 4: Present Workflow Mode Options

**Question:** "Which workflow mode fits your style?"

**Option Presentation:**
```
Workflow Mode:

Choose how you want to develop your story. Both approaches work for any length.

A. YOLO Mode (Quick Start, Discovery Writing)
   - Start from a vague idea
   - Minimal upfront planning
   - Discover your story through writing
   - Lighter templates and faster setup
   - System helps expand fuzzy concepts
   - Best for: Discovery writers, pantsers, experimental projects, time-limited writing
   - Next step: /write:expand to transform your idea into a workable premise

B. In-Depth Mode (Comprehensive Planning)
   - Detailed character development before drafting
   - Full plot structure with major beats
   - Comprehensive world-building
   - Character arc tracking
   - Theme and motif definition
   - Best for: Plotters, complex narratives, novels with multiple storylines
   - Next step: /write:plan to build comprehensive story foundation

Which approach fits you better? (A or B)
```

**Validation:**
- Must select A or B (case insensitive)
- If invalid, re-prompt with "Please enter A for YOLO or B for In-Depth"

**Store:** `MODE` (one of: `yolo`, `indepth`)

### Step 5: Ask for Genre

**Question:** "What genre is your story?"

**Prompt:**
```
Genre:

This helps the system provide genre-appropriate guidance and pacing recommendations.

Common genres:
- Fantasy
- Science Fiction
- Mystery / Thriller
- Romance
- Horror
- Literary Fiction
- Historical Fiction
- Contemporary Fiction
- Young Adult
- Other (please specify)

Enter your story's genre:
```

**Validation:**
- Must not be empty
- Accept any text input (writer may use hybrid genres like "Sci-Fi Romance")

**Store:** `GENRE`

### Step 6: Ask for Premise/Logline

**Question:** "Describe your core story concept in 1-2 sentences."

**Prompt:**
```
Premise/Logline:

Describe the heart of your story. What's the core conflict or situation?

Good examples:
- "A detective with telepathy must solve murders in a city where magic is illegal"
- "Two rival scholars race to decipher an ancient prophecy before war erupts"
- "A spaceship mechanic discovers the station's AI is sentient and planning rebellion"
- "A teenage witch must hide her powers while attending a non-magical boarding school"

Weak examples (too vague):
- "A story about a detective"
- "Magic and adventure"
- "It's about relationships"

For YOLO mode: It's okay if this is still fuzzy - we'll expand it in the next step.
For In-Depth mode: Try to be more specific about the central conflict.

Your premise (1-2 sentences):
```

**Validation:**
- Must be at least 10 words (to ensure it's not just "magic story")
- If too short, prompt:
  ```
  Your premise seems a bit brief. Can you add a bit more detail about the conflict or situation?
  Aim for at least 10-15 words to capture the essence of your story.
  ```

**Store:** `PREMISE`

### Step 7: Optional - Word Count Goal

**Question:** "Would you like to set a word count goal now?"

**Prompt:**
```
Word Count Goal (Optional):

Setting a goal helps track progress, but you can also set this later or skip it entirely.

Typical ranges:
- Short Story: 1,000-7,500 words
- Novella: 7,500-40,000 words
- Novel: 40,000-100,000+ words

Options:
1. Set a specific goal now (enter number of words, e.g., "50000")
2. Skip for now (you can add this later in PROJECT.md)

Enter goal or press Enter to skip:
```

**Validation:**
- If provided, must be a positive number
- If invalid, re-prompt
- If empty/skipped, set to null

**Store:** `WORD_COUNT_GOAL` (number or null)

### Step 8: Optional - Themes

**Question:** "Do you want to define themes now?"

**Prompt:**
```
Core Themes (Optional):

Themes are the deeper ideas your story explores (e.g., "power and corruption", "identity vs duty", "fear of the unknown").

You can:
1. Define 1-3 themes now (enter comma-separated, e.g., "loyalty, sacrifice, redemption")
2. Skip for now (discover themes as you write)

Enter themes or press Enter to skip:
```

**Validation:**
- If provided, split by comma and trim whitespace
- Accept any text
- If empty/skipped, set to empty array

**Store:** `THEMES` (array of strings or empty array)

### Step 9: Confirmation Summary

Display summary of all choices:

```
Project Configuration Summary:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Title: {TITLE}
Slug: {SLUG}
Length: {LENGTH}
Mode: {MODE}
Genre: {GENRE}
Premise: {PREMISE}
Word Count Goal: {WORD_COUNT_GOAL or "Not set"}
Themes: {THEMES or "Not set"}

Is this correct? (yes/no)
```

**If "no":** Ask which field to change and loop back to that step
**If "yes":** Proceed to project creation

### Step 10: Create Project Structure

```bash
# Create project directory
mkdir -p "stories/$SLUG"

# Create subdirectories for chapters
mkdir -p "stories/$SLUG/chapters"

# Create exports directory for manuscript output
mkdir -p "stories/$SLUG/exports"
```

### Step 11: Generate PROJECT.md

Use template at `.planning/templates/story-project.md` and populate:

**Frontmatter:**
```yaml
---
title: "{TITLE}"
genre: {GENRE}
length: {LENGTH}
mode: {MODE}
status: planning
created: {YYYY-MM-DD}
word_count_goal: {WORD_COUNT_GOAL or null}
---
```

**Content replacements:**
- `{STORY_TITLE}` → TITLE
- `{GENRE}` → GENRE
- `{DATE}` → current date in YYYY-MM-DD format
- `{word_count_goal}` → WORD_COUNT_GOAL or "Not set - run /write:pacing for recommendations"
- In Premise section, replace placeholder with PREMISE
- In Core Themes section, replace placeholders with THEMES (if provided) or keep template placeholders

**Handle LENGTH-specific sections:**
- If LENGTH is "short-story": Remove sections marked with `<!--LENGTH:novel-->` to `<!--/LENGTH:novel-->`
- If LENGTH is "novel" or "novella": Keep all sections

Write to `stories/{SLUG}/PROJECT.md`

### Step 12: Create Mode-Specific Template Files

**If MODE is "yolo":**

Create placeholder files using YOLO templates:

1. **stories/{SLUG}/CHARACTERS.md**
   - Copy from `.planning/templates/yolo-characters.md`
   - Replace `{STORY_TITLE}` with TITLE
   - Keep character slots as placeholders

2. **stories/{SLUG}/OUTLINE.md**
   - Copy from `.planning/templates/yolo-outline.md`
   - Replace `{STORY_TITLE}` with TITLE
   - Keep structure as placeholders (to be filled by /write:expand)

**If MODE is "indepth":**

Create placeholder files using In-Depth templates:

1. **stories/{SLUG}/CHARACTERS.md**
   - Copy from `.planning/templates/characters.md`
   - Replace `{STORY_TITLE}` with TITLE
   - Keep character profiles as placeholders

2. **stories/{SLUG}/OUTLINE.md**
   - Copy from `.planning/templates/outline.md`
   - Replace `{STORY_TITLE}` with TITLE
   - Keep plot structure as placeholders

3. **stories/{SLUG}/ARCS.md**
   - Create from scratch with template structure for character transformation tracking

4. **stories/{SLUG}/WORLD.md**
   - Create from scratch with template structure for world-building details

### Step 13: Success Message and Next Steps

**Display completion message:**

```
✓ Project created successfully!

Location: stories/{SLUG}/
Files created:
  - PROJECT.md (story metadata and progress tracking)
  - CHARACTERS.md (character profiles)
  - OUTLINE.md (plot structure)
  {if indepth:}
  - ARCS.md (character development tracking)
  - WORLD.md (world-building documentation)
  {endif}
  - chapters/ (directory for your story chapters)
  - exports/ (directory for manuscript exports)

Current Status: Planning
```

**If MODE is "yolo":**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
YOLO Mode: Quick Start Workflow
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your project is initialized with lightweight planning templates.

Next Step: /write:expand

This will:
  ✓ Transform your premise into a structured story concept
  ✓ Generate basic character sketches (2-4 core characters)
  ✓ Suggest simple plot structure with major beats
  ✓ Get you ready to start writing immediately

After expansion, you can:
  • Run /write:style to define your writing voice
  • Run /write:chapter to start drafting
  • Skip heavy planning and discover your story through writing

Estimated time for expansion: 10-15 minutes

Ready to expand your idea: /write:expand
```

**If MODE is "indepth":**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
In-Depth Mode: Comprehensive Planning
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your project is initialized for detailed story development.

Next Step: /write:plan

This will guide you through:
  ✓ Detailed character profiles with goals, conflicts, and arcs
  ✓ Full plot structure with three-act breakdown and major beats
  ✓ Character transformation tracking from start to finish
  ✓ World-building documentation (rules, culture, consistency)
  ✓ Theme and motif definition

This planning phase takes 30-60 minutes but provides:
  • Solid foundation for complex narratives
  • Clear roadmap before drafting
  • Consistency reference for later chapters
  • Reduced risk of plot holes and character inconsistencies

After planning, you can:
  • Run /write:style to define your writing voice
  • Run /write:chapter to start drafting with full context
  • Refer to your planning docs throughout the writing process

Estimated time for planning: 30-60 minutes

Ready to build your story foundation: /write:plan
```

### Step 14: Display Project Summary

```
Project: {TITLE}
─────────────────────────────

Story Length: {LENGTH}
Workflow Mode: {MODE}
Genre: {GENRE}
Word Count Goal: {WORD_COUNT_GOAL or "Not set (add later with /write:pacing)"}

Status: Ready for {expansion|planning}

Command to continue: /write:{expand|plan}
```

## Implementation Notes

### Title Slugification

Use bash for consistency:

```bash
SLUG=$(echo "$TITLE" | tr '[:upper:]' '[:lower:]' | sed 's/[^a-z0-9]/-/g' | sed 's/--*/-/g' | sed 's/^-//' | sed 's/-$//')
```

This ensures:
- Lowercase only
- Non-alphanumeric characters become hyphens
- Multiple consecutive hyphens collapsed to one
- No leading or trailing hyphens

### Frontmatter Format

The frontmatter must be valid YAML for parsing by later workflows:

```yaml
---
title: "The Story Title"     # Use quotes if title contains: or special chars
genre: fantasy               # Lowercase, single word preferred
length: novel                # One of: short-story, novella, novel
mode: indepth               # One of: yolo, indepth
status: planning            # Will progress to: planning-complete, drafting, revising, complete
created: 2026-02-27         # ISO date format YYYY-MM-DD
word_count_goal: 80000      # Number or null
---
```

### Error Handling

**Duplicate title:**
```
Error: Project 'stories/my-story/' already exists.

The slug 'my-story' is taken. Please choose a different title.

Suggestions:
- "My Story (Revised)"  → my-story-revised
- "My Story V2"         → my-story-v2
- "My New Story"        → my-new-story
```

**Invalid input:**
- Re-prompt with clear error message
- Show valid options again
- Don't lose previous answers

**Template file missing:**
```
Error: Template file not found at .planning/templates/{template-name}.md

Please ensure the template exists or contact support.
```

**Directory creation failure:**
```
Error: Could not create project directory at stories/{slug}/

Check permissions and disk space.
```

### Validation Logic

**Title validation:**
```bash
if [ -z "$TITLE" ]; then
  echo "Error: Title cannot be empty"
  exit 1
fi

if [ -d "stories/$SLUG" ]; then
  echo "Error: Project 'stories/$SLUG' already exists"
  exit 1
fi
```

**Premise validation:**
```bash
WORD_COUNT=$(echo "$PREMISE" | wc -w)
if [ "$WORD_COUNT" -lt 10 ]; then
  echo "Error: Premise is too brief ($WORD_COUNT words). Please add more detail (at least 10 words)."
  exit 1
fi
```

**Word count goal validation:**
```bash
if [ -n "$WORD_COUNT_GOAL" ] && ! [[ "$WORD_COUNT_GOAL" =~ ^[0-9]+$ ]]; then
  echo "Error: Word count goal must be a positive number"
  exit 1
fi
```

### Option Presentation Best Practices

**Clear formatting:**
- Use numbers or letters for options (1, 2, 3 or A, B)
- Bold option names with asterisks: `**YOLO Mode**`
- Use bullet points for details
- Include "Best for:" guidance
- Show what comes next: "Next step: /write:expand"

**Whitespace and structure:**
- Use blank lines between options
- Use separators (━━━) for major sections
- Align text for readability
- Keep descriptions concise (2-3 lines per option)

**Examples over abstractions:**
- Show concrete examples of good premises
- Show examples of weak premises to avoid
- Provide genre examples
- Give word count ranges with context

## Quality Checklist

Before marking task complete, verify:

- [ ] All 7 question steps implemented (title, length, mode, genre, premise, word count, themes)
- [ ] Each question has clear option presentation with formatting
- [ ] Validation logic present for all inputs
- [ ] Error messages are helpful with suggestions
- [ ] Duplicate title checking implemented
- [ ] Premise word count validation (minimum 10 words)
- [ ] Confirmation summary shows all choices
- [ ] Project directory creation includes chapters/ and exports/ subdirs
- [ ] PROJECT.md generated with correct frontmatter and content
- [ ] Mode-specific templates created (YOLO vs In-Depth)
- [ ] Success message shows files created
- [ ] Next-step guidance is clear and actionable for both modes
- [ ] Estimated time provided for next command
- [ ] Final project summary displayed with all metadata

## Integration Points

**Extends existing init-project.md:**
- Builds on same directory structure
- Uses same PROJECT.md template
- Adds comprehensive questioning layer
- Provides better onboarding experience

**Routes to next workflows:**
- YOLO mode → `/write:expand` (to be implemented)
- In-Depth mode → `/write:plan` (to be implemented)

**Sets up for later phases:**
- PROJECT.md frontmatter read by /write:chapter for length adaptation
- CHARACTERS.md and OUTLINE.md used for story context
- Word count goal tracked in /write:chapter
- Themes referenced during chapter generation

## Comparison to /write:init

| Feature | /write:new-project | /write:init |
|---------|-------------------|-------------|
| Audience | New users, beginners | Advanced users |
| Questions | 7 comprehensive questions with options | 5 quick questions |
| Option presentation | Clear formatting with descriptions | Basic prompts |
| Validation | Extensive with helpful errors | Basic validation |
| Guidance | Detailed next-step instructions | Brief next steps |
| Time | 5-10 minutes | 2-3 minutes |
| Experience | GSD-like comprehensive flow | Quick setup |

**Recommendation:** Use `/write:new-project` as the default entry point. Keep `/write:init` for users who want faster setup and already know their preferences.
