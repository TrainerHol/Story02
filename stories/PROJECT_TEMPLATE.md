# Story Project Structure

This document explains the standard structure for story projects in Claudespeare.

## Directory Structure

Each story project lives in its own directory under `stories/`:

```
stories/
└── {story-name}/
    ├── PROJECT.md       # Story metadata and overview
    ├── CHARACTERS.md    # Character profiles
    ├── OUTLINE.md       # Plot structure and beats
    ├── ARCS.md         # Character development arcs
    ├── WORLD.md        # World-building documentation
    └── chapters/       # Individual chapter drafts
        ├── 01.md
        ├── 02.md
        └── ...
```

## File Naming Conventions

- **Story names:** Use lowercase-with-hyphens (e.g., `the-silver-tower`, `dragons-end`)
- **Chapter files:** Use zero-padded numbers (e.g., `01.md`, `02.md`, `15.md`)
- **Template variables:** Use {UPPERCASE_WITH_UNDERSCORES} for placeholders

## Standard Files

### PROJECT.md
Contains story metadata including title, genre, premise, themes, and status. This is the entry point for understanding what the story is about.

### CHARACTERS.md
Detailed profiles for all characters including personality traits, backgrounds, goals, conflicts, and speech patterns. Helps maintain consistent character behavior.

### OUTLINE.md
Three-act plot structure with major story beats, key scenes, and subplot tracking. Provides the narrative framework.

### ARCS.md
Character development tracking showing transformation from starting beliefs through key growth moments to ending state. Ensures meaningful character change.

### WORLD.MD
World-building documentation covering setting, rules, culture, geography, and history with consistency tracking to avoid contradictions.

## Example: Fantasy Story Setup

```
stories/the-silver-tower/
├── PROJECT.md           # Fantasy, themes of power and corruption
├── CHARACTERS.md        # Protagonist: Kira (apprentice mage)
├── OUTLINE.md          # Three acts: training, betrayal, redemption
├── ARCS.md             # Kira's arc from naive to wise
├── WORLD.md            # Magic system rules, tower hierarchy
└── chapters/
    └── 01.md           # First chapter draft
```

## Getting Started

1. Create a new story directory under `stories/` with a descriptive lowercase-hyphenated name
2. Copy templates from `.planning/templates/` to initialize your story files
3. Fill in the placeholders with your story details
4. Begin drafting in the `chapters/` subdirectory

## Tips

- Update PROJECT.md status as you progress through planning and drafting phases
- Reference CHARACTERS.md and WORLD.md frequently while writing to maintain consistency
- Use ARCS.md to ensure character development feels earned and properly paced
- Keep OUTLINE.md updated if plot evolves during drafting
