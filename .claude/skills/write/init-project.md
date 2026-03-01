# Initialize New Story Project

Create a new story project with structured initialization that captures essential information and routes to appropriate workflow based on writer preferences.

## What this does

This workflow:
1. Gathers essential story information (title, genre, premise)
2. Captures writer preferences (story length, workflow mode)
3. Creates project directory structure
4. Generates PROJECT.md with metadata and frontmatter
5. Routes to next steps based on selected mode

## Workflow

### Step 1: Welcome and Overview

Explain to the writer:
- We're setting up a new story project
- This takes 2-3 minutes to capture the essentials
- They'll choose between quick-start (YOLO) or detailed planning (In-Depth)
- They'll select story length to get appropriate templates

### Step 2: Gather Story Information

Ask the following questions in sequence:

#### Story Title (required)
"What's your story title?"

- Must be unique
- Will be used to create directory name (slugified)
- Can be changed later in PROJECT.md if needed

#### Story Length (required)
"What length are you planning?"

Options:
1. **Short story** (<7,500 words) - tight focus, single storyline, minimal characters
2. **Novella** (7,500-40,000 words) - focused narrative, 2-3 subplots, core cast
3. **Novel** (40,000+ words) - expansive story, multiple subplots, full world-building

This determines template depth in later phases.

#### Workflow Mode (required)
"Which workflow mode fits your style?"

Options:
1. **YOLO (quick start)** - For discovery writers
   - Start with vague ideas
   - Minimal upfront planning
   - Discover story through writing
   - Lighter templates
   - Best for: experimental projects, pantsers, time-limited writing

2. **In-Depth (detailed planning)** - For planners
   - Comprehensive character development
   - Detailed plot outlining
   - Full world-building
   - Best for: complex narratives, plotters, novels

This determines which workflow runs next (expand vs plan).

#### Genre (required)
"What genre is your story?"

Common options:
- Fantasy
- Science Fiction
- Romance
- Mystery / Thriller
- Horror
- Literary Fiction
- Historical Fiction
- Other (specify)

#### Premise / Logline (required)
"Describe your core story concept in 1-2 sentences."

Examples:
- "A detective with telepathy must solve murders in a city where magic is illegal"
- "Two rival scholars race to decipher an ancient prophecy before war erupts"
- "A spaceship mechanic discovers the AI running the station is sentient and planning rebellion"

For YOLO mode, this can be vague - the expand workflow will refine it.
For In-Depth mode, encourage a bit more detail.

### Step 3: Validation

Before creating project:

1. **Check title uniqueness:**
   ```bash
   SLUG=$(echo "{TITLE}" | tr '[:upper:]' '[:lower:]' | sed 's/[^a-z0-9]/-/g' | sed 's/--*/-/g' | sed 's/^-//' | sed 's/-$//')

   if [ -d "stories/$SLUG" ]; then
     echo "Error: Project 'stories/$SLUG' already exists. Choose a different title."
     exit 1
   fi
   ```

2. **Validate inputs:**
   - Title is not empty
   - Length is one of: short-story, novella, novel
   - Mode is one of: yolo, indepth
   - Genre is not empty
   - Premise is at least 10 words

### Step 4: Create Project Structure

```bash
# Create project directory
mkdir -p "stories/$SLUG"

# Generate PROJECT.md from template
```

Use the template at `.planning/templates/story-project.md` and populate:
- `{STORY_TITLE}` → provided title
- `{GENRE}` → provided genre
- `{DATE}` → current date (YYYY-MM-DD format)
- Add frontmatter at top:

```yaml
---
title: "{TITLE}"
genre: {genre}
length: {short-story|novella|novel}
mode: {yolo|indepth}
status: planning
created: {YYYY-MM-DD}
---
```

- In Premise section, insert provided logline
- Leave other sections with placeholders from template

Write to `stories/{slug}/PROJECT.md`

### Step 5: Confirm and Route to Next Steps

Display success message:

```
✓ Project created: stories/{slug}/

Next steps based on your mode:
```

**If YOLO mode selected:**
```
YOLO Mode: Quick Start
━━━━━━━━━━━━━━━━━━━━
Your project is initialized with lightweight planning.

Next: Run `/write:expand` to transform your vague idea into a structured premise with basic character sketches and plot outline.

After expansion, you'll be ready to start writing chapters immediately.
```

**If In-Depth mode selected:**
```
In-Depth Mode: Comprehensive Planning
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Your project is initialized for detailed story development.

Next: Run `/write:plan` to create comprehensive planning documents:
  - Detailed character profiles
  - Full plot structure with major beats
  - Character arcs and transformation
  - World-building documentation
  - Themes and motifs

This planning phase takes 30-60 minutes but builds a solid foundation for complex narratives.
```

### Step 6: Final Output

Show project location and next command:
```
Project created at: stories/{slug}/PROJECT.md

Current status: Planning
Story length: {length}
Workflow mode: {mode}

Ready for next step: /write:{expand|plan}
```

## Implementation Notes

### Title Slugification Logic

```bash
# Convert to lowercase
# Replace non-alphanumeric with hyphens
# Collapse multiple hyphens
# Remove leading/trailing hyphens
SLUG=$(echo "$TITLE" | tr '[:upper:]' '[:lower:]' | sed 's/[^a-z0-9]/-/g' | sed 's/--*/-/g' | sed 's/^-//' | sed 's/-$//')
```

### Frontmatter Format

The frontmatter must be valid YAML and parseable by later workflows:

```yaml
---
title: "The Crimson Prophecy"  # Quotes if title contains special chars
genre: fantasy                  # Lowercase, no spaces
length: novel                   # One of: short-story, novella, novel
mode: indepth                   # One of: yolo, indepth
status: planning                # Will progress to: planning-complete, drafting, revising, complete
created: 2026-02-26            # ISO date format
---
```

Later workflows will read these fields to determine:
- Which templates to use (YOLO vs In-Depth)
- Template depth (based on length)
- Current phase (based on status)

### Error Handling

- If directory exists: clearly state project already exists, suggest different title
- If invalid input: re-prompt with examples
- If template file missing: error with path to check

### Future Extensions

This initialization is Phase 1. Future phases will add:
- Chapter drafting workflow
- Revision workflow with AI pattern detection
- Style consistency checking
- Export and formatting
