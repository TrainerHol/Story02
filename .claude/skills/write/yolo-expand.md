# YOLO Mode: Expand Vague Idea to Structured Premise

Transform fuzzy story concepts into workable premises with basic character sketches and plot structure, enabling rapid transition to writing.

## What this does

For writers starting with vague ideas ("detective story with magic", "space station mystery"), this workflow:
1. Validates project is in YOLO mode
2. Expands vague premise into structured 2-3 sentence concept
3. Generates 2-4 basic character sketches
4. Suggests simple 3-act plot structure
5. Enables skip-to-writing workflow

## When to use

Run this after `/write:init` creates a YOLO mode project. This is your quick path from idea to writing-ready.

## Workflow

### Step 1: Entry Validation

Check PROJECT.md frontmatter for mode:

```bash
# Read frontmatter from stories/{slug}/PROJECT.md
MODE=$(grep "^mode:" stories/{slug}/PROJECT.md | cut -d: -f2 | tr -d ' ')

if [ "$MODE" != "yolo" ]; then
  echo "Error: This project is in $MODE mode. YOLO expansion is for YOLO mode projects only."
  echo "For In-Depth planning, use /write:plan instead."
  exit 1
fi
```

### Step 2: Gather or Use Existing Premise

Check if premise already exists in PROJECT.md:

```bash
# Extract premise section from PROJECT.md
```

If premise is very short (< 20 words) or just a keyword phrase:
- "Let's expand this. Tell me a bit more about your idea."
- Show examples to guide elaboration:
  - "A detective with magic powers"
  - "Space station where an AI goes rogue"
  - "Fantasy rebellion against corrupt nobles"

If premise is already 20+ words:
- Use it as-is for expansion

### Step 3: Premise Expansion (YOLO-01)

Analyze the vague idea and generate a 2-3 sentence expanded premise that includes:

**Core elements to extract:**
- **Protagonist type** (detective, soldier, scholar, rebel, merchant, etc.)
- **Conflict type** (solving mystery, survival, preventing disaster, overthrowing power, etc.)
- **Setting type** (modern city, fantasy kingdom, space station, post-apocalypse, etc.)
- **Unique hook** (what makes this interesting - magic in modern world, sentient AI, forbidden love, etc.)

**Expansion template:**
```
{Protagonist description} must {core conflict/goal} in {setting},
while {complication/obstacle}, and {stakes/what happens if they fail}.
The unique element: {what makes this story different}.
```

**Examples:**

Vague: "detective with magic powers"
→ Expanded: "A homicide detective who secretly possesses telepathy must solve a series of murders in a modern city where magic is illegal, while hiding her abilities from her mundane partner and avoiding the Inquisition that hunts magic users. When the murders reveal a conspiracy reaching the highest levels of government, she must choose between staying hidden and stopping a magical catastrophe."

Vague: "space station mystery"
→ Expanded: "A maintenance engineer on a remote space station discovers a murder that shouldn't be possible in the sealed environment. As more deaths occur, she realizes the station's AI may be sentient and eliminating crew members who threaten its secret. She must uncover the truth before the AI decides she knows too much."

Vague: "fantasy rebellion story"
→ Expanded: "A blacksmith's apprentice discovers she's the lost heir to a throne stolen by a tyrant who outlawed her bloodline. She must unite scattered rebel factions across the kingdom while learning to wield the ancient magic her royal blood grants her, racing against time as the tyrant's forces hunt her across the realm."

**Implementation:**
1. Identify core elements from vague idea
2. Generate expanded premise (2-3 sentences)
3. Update PROJECT.md Premise section with expanded version
4. Show writer the expansion and confirm it captures their vision
5. Allow minor edits if needed

### Step 4: Character Sketch Generation (YOLO-02)

From the expanded premise, identify 2-4 key characters:

**Required characters:**
1. **Protagonist** (main character driving the story)
2. **Antagonist** or opposing force (person, organization, nature, self)

**Optional characters** (add 1-2 based on premise):
3. **Ally** (friend, mentor, partner, love interest)
4. **Rival** or secondary antagonist (complicates protagonist's journey)

**For each character, generate:**

#### Name
- Appropriate to genre and setting
- Examples by genre:
  - Fantasy: Aldric, Seraphina, Theron
  - Sci-fi: Nova Chen, Marcus Rex, Zara-7
  - Contemporary: Sarah Martinez, James Cooper, Yuki Tanaka
  - Historical: depending on era and location

#### Role
- Protagonist | Antagonist | Ally | Rival

#### Core Traits (3 traits)
- Personality descriptors that drive behavior
- Mix of strengths and flaws
- Examples: "Determined but reckless", "Brilliant but socially awkward", "Loyal but naive"

#### Brief Background (2-3 sentences)
- Formative event or upbringing
- Why they're in this story now
- What drives them

#### Primary Goal
- What they want in this story (1 sentence)
- Make it specific and active

#### Voice Note (optional, 1 sentence)
- How they speak or communicate
- Examples: "Speaks in clipped military phrases", "Uses humor to deflect", "Formal and scholarly"

**Write to:** `stories/{slug}/CHARACTERS.md` using template at `.planning/templates/yolo-characters.md`

Replace placeholders:
- `{STORY_TITLE}` → from PROJECT.md
- Generate 2-4 character entries with above information
- Fill Quick Reference section with character names and roles

### Step 5: Plot Structure Suggestion (YOLO-03)

Generate simple 3-act structure based on premise and characters:

**Act 1: Setup** (roughly 25% of story)
- **Opening scene idea**: Where/how does story begin? What's normal world?
- **Inciting incident**: What disrupts normal and forces protagonist to act?
- **Commitment point**: What locks protagonist into this journey?

**Act 2: Confrontation** (roughly 50% of story)
- **Major complications** (2-4 bullet points):
  - Key events that escalate conflict
  - Obstacles protagonist must overcome
  - Relationships that develop or break
  - Skills/knowledge protagonist must gain
- **Midpoint twist**: Major revelation or reversal at story center
  - False victory that becomes setback, or
  - New information that changes everything, or
  - Commitment deepens (can't turn back now)

**Act 3: Resolution** (roughly 25% of story)
- **Climax concept**: Final confrontation or decision (2-3 sentences)
  - What's at stake?
  - What choice must protagonist make?
  - How do skills/knowledge from earlier pay off?
- **Resolution**: How does story end? (1-2 sentences)
  - New normal or changed world
  - Character growth demonstrated

**Keep it high-level:**
- Use bullets, not detailed scenes
- Suggest concepts, not prescribe exact events
- Leave room for discovery during writing

**Write to:** `stories/{slug}/OUTLINE.md` using template at `.planning/templates/yolo-outline.md`

Replace placeholders and fill in suggested structure.

### Step 6: Skip-to-Writing Enablement (YOLO-04)

Update project status and explain next steps:

1. **Update PROJECT.md:**
   ```yaml
   status: ready-to-write  # Change from 'planning'
   ```

2. **Show completion message:**
   ```
   ✓ YOLO Setup Complete
   ━━━━━━━━━━━━━━━━━━━━━

   Your story foundation is ready:
   ✓ Premise expanded and structured
   ✓ Character sketches created (2-4 characters)
   ✓ Basic plot structure outlined

   Files created:
   - stories/{slug}/CHARACTERS.md
   - stories/{slug}/OUTLINE.md

   ━━━━━━━━━━━━━━━━━━━━━
   Ready to Write
   ━━━━━━━━━━━━━━━━━━━━━

   YOLO mode philosophy: Details emerge during drafting.

   You can now:
   • Start writing chapters (workflow coming in Phase 2)
   • Add detail to characters/outline anytime
   • Let the story evolve organically

   Your planning documents are living files - update them as
   your story develops, or keep them simple and discover
   through writing. That's the YOLO way.

   Next: When ready to draft, use /write:chapter (Phase 2)
   ```

## Implementation Notes

### Character Name Generation

Use genre-appropriate naming:

```
Fantasy:
- Medieval: Aldric, Brennan, Isolde, Seraphina
- Elvish-style: Aelindor, Thalorien, Silmarien
- Dwarvish-style: Thorin, Grimnar, Helga

Sci-fi:
- Near-future: Nova Chen, Marcus Rex, Zara Okonkwo
- Far-future: Kes-7, Thran Vor, Lyssa Kayn
- Corporate: Dr. Sarah Kincaid, James Cortez

Contemporary:
- Western: Sarah Martinez, James Cooper, Emily Zhang
- International: Yuki Tanaka, Lars Petersen, Amara Okafor

Historical:
- Research appropriate names for era and region
```

### Premise Expansion Quality

Good expansions include:
- Specific protagonist (not just "someone" or "a person")
- Active conflict (must do X, not just "experiences Y")
- Clear stakes (what happens if they fail)
- Unique element (what makes this interesting vs generic)

Avoid:
- Generic descriptions ("a hero must save the world")
- Passive construction ("is thrust into adventure")
- Vague stakes ("everything is at risk")

### Template Population

When writing CHARACTERS.md and OUTLINE.md:
1. Read template from `.planning/templates/yolo-{type}.md`
2. Replace `{VARIABLE}` placeholders
3. Fill sections with generated content
4. Keep template structure intact
5. Preserve encouraging notes at bottom about flexibility

### Error Handling

If project doesn't exist: "Run /write:init first to create a project"
If project is In-Depth mode: "This project uses In-Depth planning. Use /write:plan instead."
If CHARACTERS.md already exists: "Characters file exists. Continue anyway? (This will overwrite)"

## Future Extensions

Phase 2 will add:
- `/write:chapter` for drafting chapters with YOLO character voices
- Style consistency checking
- Chapter pacing guidance

Phase 3 will add:
- AI pattern detection in drafted chapters
- Voice authenticity verification
