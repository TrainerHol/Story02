# Character Bank Management Workflow

Persistent character database for consistent character portrayal across all chapters.

## Overview

The character bank is a single source of truth for all character details in your story. It lives in `.writing/characters/` and persists across chapters, preventing character inconsistencies. Chapter generation automatically references the bank to maintain voice, appearance, and behavior consistency.

**Storage Location:** `.writing/characters/` (in your story project root)
**Format:** One markdown file per character (`.writing/characters/{character-slug}.md`)
**When to use:** During project setup, before writing chapters, after character development moments
**Time:** 5-10 minutes per character

## Character Bank Structure

Each character file follows a comprehensive format capturing all aspects needed for consistent portrayal.

### File Naming Convention

- **Protagonist:** `protagonist-{first-name}.md` (e.g., `protagonist-sarah.md`)
- **Antagonist:** `antagonist-{first-name}.md` (e.g., `antagonist-mark.md`)
- **Supporting:** `{first-name}-{last-initial}.md` (e.g., `detective-rivera.md`, `sarah-mom.md`)

Use lowercase, hyphens for spaces, memorable identifiers.

### Character Profile Format

```markdown
---
name: {Full Character Name}
slug: {character-slug}
role: {protagonist|antagonist|supporting}
first_appearance: chapter-{N}
last_updated: {ISO timestamp}
---

# {Character Name}

## Core Identity

**Role:** {protagonist/antagonist/supporting}
**Age:** {specific age or range, e.g., "34" or "mid-40s"}
**Occupation:** {job/role in the story}

## Physical Appearance

{Detailed visual description}

**Height:** {specific or approximate}
**Build:** {body type, physique}
**Hair:** {color, length, style, texture}
**Eyes:** {color, distinctive features}
**Skin:** {tone, texture, notable marks}
**Distinguishing Features:** {scars, tattoos, birthmarks, unique characteristics}
**Typical Style:** {clothing preferences, how they present themselves}

**Key Visual:** {1-2 sentence memorable description that will appear in prose}

Example: "She always wore that leather jacket—the one with the torn pocket and cigarette burns on the sleeve. Dark hair pulled back tight, silver scar cutting through her left eyebrow."

## Personality

**Core Traits:** {3-5 primary personality characteristics}
- {Trait 1 with brief explanation}
- {Trait 2 with brief explanation}
- {Trait 3 with brief explanation}

**Quirks and Mannerisms:** {small behaviors that make them distinctive}
- {Physical habit or gesture}
- {Speech pattern or verbal tic}
- {Reaction pattern under stress}

**Voice:** {how they speak and sound}
- **Formality:** {formal/casual/shifts between}
- **Verbosity:** {terse/balanced/verbose}
- **Catchphrases:** {any repeated phrases or expressions}
- **Speech Patterns:** {rhythm, word choices, grammar quirks}

Example: "Speaks in short, clipped sentences. Never uses contractions when angry. Has a habit of ending statements with 'yeah?' like she's challenging you to disagree."

## Background

{Relevant history and formative experiences}

**Origin:** {where they come from, early life}
**Education:** {formal education, training, life lessons}
**Key Experiences:** {2-3 formative events that shaped who they are}
**Relationships:** {connections to other characters, family, friends, enemies}

Keep focused on what's relevant to the story. Not a full biography.

## Goals and Motivations

**External Goal (What they want):**
{Concrete, observable objective in the story}

**Internal Motivation (Why they want it):**
{Psychological/emotional drive beneath the external goal}

**Obstacles:**
{What stands in their way—external and internal}

Example:
- **External:** Find proof that her mother was murdered
- **Internal:** Needs to know the truth to stop blaming herself for not being there
- **Obstacles:** Police closed the case, family wants her to move on, she's afraid of what she might discover

## Character Arc

**Starting Point:** {who they are at story beginning}
{Beliefs, behaviors, emotional state, worldview}

**Transformation:** {how they change through the story}
{Key moments of growth, realizations, shifts in perspective}

**Ending Point:** {who they become by story end}
{Changed beliefs, new behaviors, evolved understanding}

This section maps the internal journey. The plot is what happens; the arc is how it changes them.

## Consistency Notes

**Appearance Locks:** {details that must NEVER change}
- {Physical attribute 1}
- {Physical attribute 2}
- {Physical attribute 3}

Example: "Green eyes (not hazel, not blue), 5'8" (shorter than her brother), scar through left eyebrow (from childhood accident)"

**Voice Markers:** {speech patterns that must remain consistent}
- {Marker 1}
- {Marker 2}
- {Marker 3}

Example: "Never swears (raised religious), uses 'reckon' frequently, drops 'g' on -ing words when relaxed"

**Behavior Patterns:** {consistent reactions}
- {Stress response}
- {Conflict handling}
- {Trust indicators}

Example: "Goes silent when angry (never yells), trusts actions over words, pushes people away when she needs help most"

## Chapter References

Running log of this character's appearances and development across chapters.

- **Chapter 1:** {brief note on what happened with this character}
- **Chapter 3:** {brief note}
- **Chapter 5:** {brief note}
- ...

Updated automatically by chapter generation workflow. Helps track character journey and ensure continuity.

Example:
- **Chapter 1:** Introduced at mother's funeral. Tense with family. Noticed inconsistencies in police report.
- **Chapter 3:** First visit to mother's house. Discovered hidden documents. Confronted father.
- **Chapter 5:** Interview with detective. Learned about sealed evidence. Realized case was closed too quickly.
```

## Commands

### `/write:character <name>` - Query Character Profile

Retrieve and display full character profile from the bank.

**Usage:**
```
/write:character Sarah
/write:character Detective Rivera
/write:character antagonist
```

**Process:**

1. **Validate story project exists**
   - Check for PROJECT.md in current or parent directory
   - Confirm `.writing/characters/` directory exists
   - If not: "Not in a story project. Run `/write:new-project` or `/write:init` first."

2. **Look up character**
   - Convert name to slug format (lowercase, hyphens)
   - Search `.writing/characters/` for matching file
   - Try variations: `{name}.md`, `protagonist-{name}.md`, `antagonist-{name}.md`, `{name}-*.md`

3. **If found: Display full profile**
   - Read and display entire character file
   - Highlight last_updated timestamp
   - Show chapter references section last
   - Offer actions: "Update this character? (`/write:update-character {name}`)"

4. **If not found: Offer creation options**

   **Option A: Create from CHARACTERS.md**
   - Check if CHARACTERS.md or yolo-characters.md exists
   - Search for character by name in that file
   - If found: "Character '{name}' exists in CHARACTERS.md. Create bank entry from this data?"
   - If confirmed: Extract available information, create bank entry with populated sections, leave unfilled sections as templates

   **Option B: Create new character from scratch**
   - If character not in CHARACTERS.md or user declines Option A
   - Prompt: "Create new character '{name}' in the bank?"
   - If confirmed: Create bank entry with template structure, prompt for role (protagonist/antagonist/supporting), set first_appearance to next chapter, provide empty sections for user to fill

**Output:**

```
Character Profile: Sarah Martinez

Role: Protagonist
Age: 34
Occupation: Investigative journalist

[... full profile content ...]

Last updated: 2026-02-27T10:30:00Z

─────────────────────────────────
Actions:
- Update profile: /write:update-character sarah
- View another: /write:character {name}
```

**Duration:** < 1 minute (instant lookup and display)

### `/write:update-character <name>` - Update Character Profile

Modify existing character profile in the bank.

**Usage:**
```
/write:update-character Sarah
/write:update-character detective-rivera
```

**Process:**

1. **Load existing character**
   - Look up character file in `.writing/characters/{slug}.md`
   - If not found: "Character '{name}' not in bank. Create first with `/write:character {name}`"
   - Display current profile

2. **Ask what to update**

   Present options:
   ```
   What would you like to update for {Character Name}?

   1. Physical appearance (add/change description)
   2. Personality traits (add/modify traits, quirks, voice)
   3. Background information (history, relationships)
   4. Goals and motivations (external/internal)
   5. Voice markers (speech patterns, catchphrases)
   6. Consistency locks (appearance/behavior that must never change)
   7. Character arc (starting point, transformation, ending)
   8. Chapter references (add note about character in recent chapter)
   9. Multiple sections (guided update)
   ```

3. **For each selected section:**
   - Show current content
   - Prompt for changes: "What should change?" or "What should be added?"
   - Apply changes to that section only
   - Preserve all other sections unchanged

4. **Update metadata**
   - Set `last_updated: {current ISO timestamp}`
   - Preserve other frontmatter fields

5. **Save and confirm**
   - Write updated file to `.writing/characters/{slug}.md`
   - Display: "Updated {Character Name}. Last modified: {timestamp}"
   - Show what changed (summary of edits)

**Special Cases:**

**Adding chapter reference:**
- If option 8 selected: "Which chapter?" → get chapter number
- "What happened with {character} in this chapter?" → get brief note
- Append to Chapter References section: `- **Chapter {N}:** {note}`

**Multiple sections:**
- If option 9 selected: walk through sections interactively
- For each: "Update {section}? (y/n)" → if yes, prompt for changes
- Apply all changes at once, update timestamp once

**Consistency locks:**
- When updating appearance or voice markers, prompt: "Add to consistency locks?"
- Locks are details that must never change in future chapters
- Helps maintain continuity during chapter generation

**Output:**

```
Updated Sarah Martinez

Changed:
- Physical appearance: Added detail about leather jacket and scar
- Consistency locks: Added eye color (green) to appearance locks

Last updated: 2026-02-27T14:15:00Z

Profile saved to .writing/characters/protagonist-sarah.md
```

**Duration:** 3-8 minutes depending on scope of updates

### `/write:populate-bank` - Auto-Populate Bank from CHARACTERS.md

Create character bank entries automatically from existing CHARACTERS.md or yolo-characters.md file.

**Usage:**
```
/write:populate-bank
```

**When to use:**
- During project initialization (after `/write:init` or `/write:new-project`)
- When transitioning from planning to writing phase
- To bootstrap character bank before first chapter

**Process:**

1. **Validate story project**
   - Check for PROJECT.md
   - Confirm CHARACTERS.md or yolo-characters.md exists
   - If missing: "No character file found. Create CHARACTERS.md first or add characters manually with `/write:character {name}`"

2. **Parse character file**
   - Read CHARACTERS.md (or yolo-characters.md)
   - Extract character entries (typically marked by ## headers or numbered lists)
   - For each character: extract name, role, available details

3. **Create bank entries**
   - For each character found:
     - Generate slug from name
     - Create `.writing/characters/{slug}.md` file
     - Set frontmatter: name, slug, role, first_appearance (null), last_updated (current timestamp)
     - Populate sections with available data from CHARACTERS.md
     - Leave empty sections as templates with instructions

4. **Map data intelligently**

   **From CHARACTERS.md to Bank format:**
   - Name → Core Identity section and frontmatter
   - Age/occupation → Core Identity section
   - Physical description → Physical Appearance section
   - Personality traits → Personality section
   - Background/history → Background section
   - Goals/wants → Goals and Motivations section
   - Character arc notes → Character Arc section
   - Voice notes → Personality > Voice subsection

   **Initialize empty sections:**
   - Consistency Notes (appearance locks, voice markers, behavior patterns)
   - Chapter References (empty, will populate during chapter writing)

5. **Report results**
   - List all characters created
   - Show file paths
   - Note any characters that had incomplete data
   - Suggest next step: "Character bank populated. Review and update profiles with `/write:character {name}` before writing chapters."

**Output:**

```
Character Bank Populated

Created 4 character profiles:

✓ protagonist-sarah.md (Sarah Martinez)
  - Core identity, appearance, personality populated
  - Goals and background populated
  - Chapter references: empty (will populate during chapter writing)

✓ antagonist-mark.md (Mark Davidson)
  - Core identity and basic details populated
  - Background and motivation populated
  - Appearance: partial (add more detail with /write:update-character mark)

✓ detective-rivera.md (Detective Maria Rivera)
  - Supporting character profile created
  - Basic details populated from CHARACTERS.md

✓ sarah-mom.md (Ellen Martinez)
  - Supporting character profile created
  - Minimal data available (referenced but not detailed in CHARACTERS.md)
  - Update with /write:update-character sarah-mom before her chapter

─────────────────────────────────
All files saved to .writing/characters/

Next steps:
1. Review profiles: /write:character {name}
2. Add missing details: /write:update-character {name}
3. Begin writing: /write:chapter
```

**Duration:** 5-15 minutes depending on character count and detail level

## Integration with Chapter Generation

The character bank integrates seamlessly with the `/write:chapter` workflow to ensure consistency.

### Before Chapter Generation (Automatic Loading)

When `/write:chapter` is invoked:

1. **Load character bank**
   - List all files in `.writing/characters/`
   - Identify POV character (user specifies at chapter start)
   - Identify major characters appearing in this chapter (from scene breakdown or plot beat)

2. **Read relevant profiles**
   - Load full profile for POV character
   - Load profiles for any other characters in the scene
   - If character appears who isn't in bank: prompt to create entry before continuing

3. **Include bank data in generation context**
   - **Voice markers:** Use for dialogue and internal monologue
   - **Appearance locks:** Ensure consistent physical descriptions
   - **Behavior patterns:** Apply to character reactions and decisions
   - **Personality traits:** Inform character actions and emotions
   - **Goals/motivations:** Drive character choices in the scene

**Example context building:**
```
POV Character: Sarah Martinez
- Voice: Speaks in short sentences, never uses contractions when angry, ends statements with "yeah?"
- Appearance: Leather jacket with torn pocket, dark hair pulled back, silver scar through left eyebrow
- Behavior: Goes silent when angry, trusts actions over words
- Current goal: Find proof mother was murdered
- Motivation: Stop blaming herself for not being there

Scene characters: Detective Rivera
- Voice: Formal, bureaucratic language, uses "per department protocol"
- Appearance: Early 50s, gray suit, tired eyes
- Behavior: By-the-book, defensive when questioned, protective of closed cases
```

This context ensures Sarah sounds like Sarah and the detective sounds like the detective.

### During Chapter Generation (Consistency Checking)

As prose is generated:

- **Dialogue:** Match character voice markers from bank
- **Internal thoughts:** Reflect POV character's personality and concerns
- **Physical descriptions:** Use appearance locks from bank
- **Character reactions:** Apply behavior patterns from bank
- **Continuity:** Reference character's goals and arc position

If chapter generation suggests action inconsistent with character profile, flag it:
```
⚠️  Character consistency check:
Generated action shows Sarah yelling at detective, but her behavior pattern says "goes silent when angry"
Revise to: Sarah falls silent, jaw tight, eyes locked on the detective
```

### After Chapter Generation (Bank Updates)

After chapter is written and saved:

1. **Update chapter references**
   - For each character who appeared in the chapter
   - Add brief note to their Chapter References section
   - Format: `- **Chapter {N}:** {what happened with this character}`

2. **Flag potential updates**
   - If chapter includes character development moment: "Character arc update recommended for {name}"
   - If new character detail revealed: "Update {name} profile to include {new detail}"
   - If relationship changed: "Update background section for {name} to reflect relationship with {other character}"

3. **Prompt for updates**
   - After chapter saved: "Update character profiles now, or continue writing?"
   - User can defer updates until later
   - Consistency check (via `/write:check`) will catch missed updates

**Example post-chapter update:**

```
Chapter 5 saved successfully.

Character bank updates:
✓ Added chapter reference for Sarah Martinez
✓ Added chapter reference for Detective Rivera

Recommended updates:
- Sarah's personality: Chapter shows new behavior pattern (bluffing/deception). Update with /write:update-character sarah?
- Detective Rivera: Revealed he knew Sarah's mother. Update background section?

Update now or continue writing? (update/continue)
```

## Workflow Integration Summary

```mermaid
graph TD
    A[/write:new-project or /write:init] --> B[Create CHARACTERS.md]
    B --> C[/write:populate-bank]
    C --> D[.writing/characters/ created]
    D --> E[Review/update profiles]
    E --> F[/write:chapter]
    F --> G[Load character bank]
    G --> H[Generate prose with consistency]
    H --> I[Update chapter references]
    I --> J{More chapters?}
    J -->|Yes| K[/write:update-character as needed]
    K --> F
    J -->|No| L[Story complete]
```

**Key Points:**

- **Persistent:** Character bank lives in `.writing/characters/`, survives project sessions
- **Automatic:** Chapter generation loads bank automatically, no manual steps
- **Consistent:** Voice markers, appearance locks, behavior patterns enforced
- **Growing:** Bank updates as characters develop through the story
- **Safe:** Original CHARACTERS.md preserved; bank is separate, editable

## Usage Examples

**Example 1: Starting with populated CHARACTERS.md**

```
> /write:populate-bank

Character Bank Populated
Created 3 character profiles:
✓ protagonist-alex.md
✓ antagonist-dr-vaughn.md
✓ maya-k.md

> /write:character alex

[Full Alex profile displayed]

> /write:chapter

[System loads Alex's profile from bank]
[Generates Chapter 1 with Alex's voice markers and appearance]
[After generation, adds "Chapter 1: Introduced at research facility" to Alex's references]
```

**Example 2: Discovering new character mid-story**

```
> /write:chapter
Chapter: 5
POV: Sarah
Scene: Sarah meets her mother's old partner, Detective Chen

⚠️  Character "Detective Chen" not in bank. Create profile before writing scene?

> Yes

Creating new character: Detective Chen
Role? (protagonist/antagonist/supporting): supporting
[Prompts for basic details]

✓ detective-chen.md created

[Chapter generation proceeds with Chen's profile]
```

**Example 3: Updating character after development moment**

```
> /write:chapter
[Writes Chapter 8 where Sarah confronts her fear]

Chapter 8 saved successfully.

Character arc update recommended for Sarah Martinez:
- Major development: Overcame trust issues, asked for help
- Update arc section?

> /write:update-character sarah

What would you like to update?
> 7. Character arc

Current arc:
Starting Point: Pushes people away, doesn't trust anyone
Transformation: [empty]
Ending Point: [empty]

Add transformation note?
> Yes. Chapter 8: Realized she can't solve everything alone. Asked Rivera for help despite fear of being vulnerable.

Updated Sarah Martinez
- Character Arc: Added transformation note

[Arc now tracked, informs future chapter generation]
```

## Best Practices

**1. Populate bank before writing chapters**
- Run `/write:populate-bank` after project setup
- Review and enhance profiles with `/write:update-character`
- Ensure POV characters have detailed voice markers

**2. Consistency locks are critical**
- Add appearance locks for easily-forgotten details (eye color, height, scars)
- Add voice markers for distinctive speech patterns
- Add behavior patterns for stress responses

**3. Update references after each chapter**
- Track character journey through chapter references
- Helps maintain continuity
- Reveals character arc progression

**4. Use bank queries during writing**
- When drafting scene with new character: `/write:character {name}` to review their voice
- When unsure about detail: Query bank instead of guessing
- Prevents contradictions

**5. Evolve bank with story**
- Characters change through story events
- Update arc section after development moments
- Add new traits discovered during writing

**6. Don't over-specify initially**
- Start with essentials (voice, appearance, core personality)
- Add detail as you discover character through writing
- Bank grows with your understanding

## Common Questions

**Q: What if I create a character bank entry but then change my mind about the character?**
A: Edit the markdown file directly in `.writing/characters/`, or use `/write:update-character` to modify any section. The bank is flexible.

**Q: Can I have multiple characters with the same first name?**
A: Yes. Use slugs to differentiate: `sarah-m.md` vs `sarah-protagonist.md`. The slug is what matters for lookups.

**Q: What if I write a chapter without character profiles?**
A: The chapter generation workflow will still work, but you'll get more generic, less distinctive character voices. Bank enables true consistency.

**Q: Do I need a bank entry for every minor character?**
A: No. Focus on POV characters and recurring characters. One-scene characters don't need full profiles—brief notes in the chapter are fine.

**Q: How does this handle character name changes (nicknames, aliases)?**
A: Add nicknames and aliases to the character profile. The slug remains constant. Search will find variations if they're documented in the profile.

**Q: What if CHARACTERS.md and the bank diverge?**
A: The bank is the source of truth during chapter generation. CHARACTERS.md is planning; the bank is operational. If you update planning, run `/write:populate-bank` again or manually sync with `/write:update-character`.

**Q: Can I delete a character from the bank?**
A: Yes. Delete the `.writing/characters/{slug}.md` file directly. Or move it to a `_archive/` folder within characters if you want to keep it but exclude it from active use.

**Q: How do I handle character relationships in the bank?**
A: Use the Background > Relationships section. Note connections to other characters. Example: "Sarah's mother—deceased, catalyst for investigation. Complicated relationship, guilt over final argument."

**Q: What about characters who appear but aren't named yet?**
A: Create a bank entry with a placeholder slug like `mysterious-woman.md`. Update the name and slug when revealed. If you rename the file, update any chapter references manually or via find/replace.

---

**Ready to build your character bank?**

Start with: `/write:populate-bank` (if you have CHARACTERS.md)
Or: `/write:character {name}` (to create from scratch)
