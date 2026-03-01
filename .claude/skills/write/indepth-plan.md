# In-Depth Planning: Comprehensive Story Development

Guide writers through detailed story development with comprehensive planning for characters, plot, world, arcs, and themes.

## What this does

For writers who benefit from thorough upfront planning, this workflow:
1. Validates project is in In-Depth mode
2. Guides through detailed character development
3. Structures full plot with major beats and subplots
4. Facilitates character arc planning
5. Documents world-building details
6. Captures themes and motifs
7. Adapts template depth based on story length (short story → novel)

## When to use

Run this after `/write:init` creates an In-Depth mode project. This comprehensive planning takes 30-60 minutes but builds a solid foundation for complex narratives.

## Workflow

### Step 1: Entry Validation

Check PROJECT.md frontmatter for mode:

```bash
MODE=$(grep "^mode:" stories/{slug}/PROJECT.md | cut -d: -f2 | tr -d ' ')

if [ "$MODE" != "indepth" ]; then
  echo "Error: This project is in $MODE mode."
  echo "For YOLO quick-start planning, use /write:expand instead."
  exit 1
fi

# Also read story length for template depth
LENGTH=$(grep "^length:" stories/{slug}/PROJECT.md | cut -d: -f2 | tr -d ' ')
```

### Step 2: Planning Phase Overview

Explain the process to the writer:

```
In-Depth Planning Workflow
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

We'll create detailed planning documents for your story across five areas:

1. Characters - Detailed profiles, backgrounds, goals, conflicts
2. Plot - Three-act structure with major beats and subplots
3. Character Arcs - Transformation tracking from start to end
4. World-Building - Setting, rules, culture, consistency
5. Themes - Core themes, voice, style decisions

Estimated time: 30-60 minutes
Story length: {LENGTH}
Template depth: {Novel = extensive | Novella = moderate | Short story = focused}

This planning builds a foundation for complex narratives. I'll prompt you
through each area. You can skip optional sections, but comprehensive planning
pays off during drafting.

Ready to begin? Let's start with characters.
```

### Step 3: Character Development (STORY-01)

Prompt for number of main characters:
- Typical: 2-4 for most stories
- Novels can have more, short stories usually 2-3

For each character, prompt through the following:

#### Name
"What's this character's name?"

Provide genre-appropriate examples if needed.

#### Role
"What's their role in the story?"
- Protagonist (main character)
- Antagonist (opposing force)
- Supporting (ally, mentor, love interest, etc.)

#### Age and Occupation
"How old are they? What do they do?"

This grounds the character in concrete details.

#### Personality Traits (3-5)
"Describe their personality in 3-5 traits."

Show examples:
- "Determined but reckless"
- "Brilliant but socially awkward"
- "Loyal but naive"
- "Cynical from past betrayals"
- "Optimistic despite hardship"

Mix strengths and flaws for dimensional characters.

#### Background
"What's their background? What shaped who they are?"

Prompt for:
- Upbringing (family, environment)
- Formative events (trauma, triumph, loss, discovery)
- Why they're in this story at this time

2-4 paragraphs for protagonists, 1-2 for supporting characters.

#### External Goal
"What do they want in this story? What are they trying to achieve?"

This is their conscious, stated objective:
- Solve the murder
- Win the competition
- Find the lost artifact
- Overthrow the tyrant

Be specific and active.

#### Internal Goal
"What do they need to learn or overcome internally?"

This is their unconscious need - the character arc driver:
- Learn to trust others
- Overcome fear of failure
- Accept their identity
- Forgive themselves

Often conflicts with or complicates external goal.

#### Conflicts
"What internal and external conflicts do they face?"

**Internal:** Fears, doubts, contradictions, wounds
**External:** Antagonists, obstacles, competing loyalties

#### Voice and Speech Patterns
"How do they speak? What's distinctive about their voice?"

Examples:
- "Formal and scholarly, uses precise language"
- "Speaks in clipped military phrases"
- "Uses humor to deflect emotional topics"
- "Rambles when nervous, confident when focused"

This helps maintain consistent character voice in dialogue.

#### Physical Description
"Describe their appearance - key traits readers should picture."

Focus on:
- Most distinctive features (not exhaustive catalogs)
- Details that reflect personality or role
- 2-3 memorable specifics

**Length-aware character depth:**
- **Short story:** 2-3 characters max, focus on essentials only
- **Novella:** 3-4 characters, moderate detail
- **Novel:** 4+ characters, full detail with relationships section

#### Repeat for Each Character

After gathering all characters, generate `stories/{slug}/CHARACTERS.md` from template `.planning/templates/characters.md`

**For novel-length:** Include all sections including relationships map
**For shorter lengths:** Exclude LENGTH:novel marked sections

### Step 4: Plot Structure (STORY-02)

Guide through three-act structure:

```
Plot Structure
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

We'll map your story using three-act structure. This provides the backbone
for your narrative beats.
```

#### Act 1: Setup (First 25%)

**Opening Scene:**
"How does your story begin?"
- Where are we?
- Who do we meet?
- What's the normal world before disruption?

Prompt for 2-3 sentences describing the opening.

**Inciting Incident:**
"What event disrupts the normal world and sets the story in motion?"
- The murder that must be solved
- The invitation to adventure
- The threat that appears
- The discovery that changes everything

Be specific about the moment things change.

**First Plot Point / Commitment:**
"What locks your protagonist into this journey? When do they commit?"
- Accepting the quest
- Crossing the threshold
- Point of no return

End of Act 1: protagonist is committed to the journey.

**Key Scenes in Act 1 (3-5 scenes):**
"What are the major scenes between opening and commitment?"

For each scene:
- Brief description (1-2 sentences)
- Purpose (what it establishes or advances)

#### Act 2: Confrontation (Middle 50%)

**Rising Action / Complications:**
"What obstacles and complications does your protagonist face?"

Prompt for 4-6 major complications (more for novels, fewer for short stories):
- New obstacles that escalate conflict
- Relationships that develop or break
- Skills or knowledge protagonist must gain
- Failures and setbacks
- Subplots that interweave

**Midpoint:**
"What's the major twist or shift at the story's center?"

Common midpoint types:
- False victory (seems to win, but it's temporary)
- Major revelation (new information changes everything)
- Commitment deepens (raise stakes, can't back out now)
- Mirror moment (protagonist sees themselves clearly)

2-3 sentences describing the midpoint event.

**Subplots (for novels):**
"What subplots develop alongside the main plot?"

For novel-length stories, prompt for 2-4 subplots:
- Relationship subplot (romance, friendship, rivalry)
- Mystery subplot (something to uncover)
- Character subplot (secondary character's journey)
- Thematic subplot (explores theme from different angle)

For each subplot:
- Brief description
- How it intersects with main plot
- Resolution point

**Skip subplot section for short stories** (LENGTH:novel marker)

**Second Plot Point / Crisis:**
"What's the darkest moment? When does everything seem lost?"
- Protagonist's plan fails
- Ally betrays or is lost
- Truth revealed that shatters assumptions
- Defeat seems certain

End of Act 2: protagonist faces their greatest challenge.

**Key Scenes in Act 2 (6-10 scenes for novel, 4-6 for novella, 3-4 for short story):**
"What are the major scenes in this act?"

Length-aware prompting:
- Novel: detailed scene list with purpose for each
- Novella/Short story: major beats only

#### Act 3: Resolution (Final 25%)

**Climax:**
"What's the final confrontation or ultimate test?"

Prompt for:
- What's at stake?
- What choice must protagonist make?
- How do earlier skills/knowledge pay off?
- What's the moment of maximum tension?

3-5 sentences describing the climax.

**Resolution:**
"How does the story end? What's the new normal?"
- How is conflict resolved?
- What's changed?
- How is character growth demonstrated?
- What's the final image or moment?

2-3 sentences for resolution.

**Denouement (optional for longer stories):**
"What happens after climax? How does world settle?"

This is the "tying up loose ends" section - more important for novels.

#### Generate Outline

Write to `stories/{slug}/OUTLINE.md` from template `.planning/templates/outline.md`

Process LENGTH:novel markers:
- **Novel:** Include subplots, detailed scene lists, pacing notes
- **Shorter:** Core three-act structure only

### Step 5: Character Arcs (STORY-03)

For each main character (especially protagonist and antagonist):

```
Character Arcs
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Now we'll track how your characters transform through the story.
```

#### For Each Character:

**Starting State:**
"At the story's beginning, what does {character} believe? What are their flaws?"
- Core belief that will be challenged
- Flaw or wound that holds them back
- False belief about themselves or world

**Arc Type:**
"What type of arc do they follow?"
- Positive change (overcome flaw, grow, transform)
- Flat arc (already complete, changes world around them)
- Negative arc (corruption, decline, tragic fall)
- Disillusionment (lose innocence or idealism)

**Growth Moments (3-5 for short stories, 5+ for novels):**
"What are the key moments where this character is tested or learns?"

For each growth moment:
- What happens (event or scene)
- What they learn (realization or new understanding)
- How they change (behavior or belief shift)

Length-aware:
- Novel: 5-7 growth moments with detailed tracking
- Novella: 4-5 growth moments
- Short story: 3 key moments

**Ending State:**
"By the story's end, what has {character} become?"
- New belief or understanding
- Flaw overcome (or deepened if negative arc)
- Growth demonstrated

#### Generate Arcs Document

Write to `stories/{slug}/ARCS.md` from template `.planning/templates/arcs.md`

Process LENGTH:novel markers:
- **Novel:** Full arc tracking with 5+ growth moments
- **Shorter:** Simplified arc with 3 moments

### Step 6: World-Building (STORY-04)

Depth varies significantly by genre and length:

```
World-Building
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Let's document your story's setting and world details.
The depth here depends on your genre and story length.

For contemporary/realistic: Setting and cultural details
For fantasy/sci-fi: Full world rules and systems
```

#### Setting
"Where and when does your story take place?"

**Time:**
- Historical period / year
- Season or time of year
- Duration of story events

**Location:**
- Primary location(s)
- Geographic scope (single city, kingdom, galaxy?)
- Atmosphere and mood of places

2-4 paragraphs describing the setting.

#### World Rules (for fantasy/sci-fi)
"What are the rules of your world? What's possible?"

**Magic or Technology System:**
- How does it work?
- What are its limitations?
- What's the cost of using it?
- Who can access it?

**Physical Laws:**
- Different from our world?
- Important constraints?

Skip this section for contemporary/realistic fiction.

#### Social Structure
"How is society organized in your world?"

- Governance (government, power structures)
- Social classes or hierarchies
- Key institutions
- Power dynamics

Depth varies by genre:
- Fantasy/Sci-fi: Often crucial to plot
- Contemporary: May be minimal

#### Culture (LENGTH:novel for extensive detail)
"What cultural details matter for your story?"

**Values and Beliefs:**
- What does society value?
- Taboos or forbidden things
- Customs and traditions
- Religion or philosophy

**Language:**
- Naming conventions
- Important phrases or slang
- Communication norms

This section more relevant for novels and genre fiction.

#### Geography (LENGTH:novel for detailed maps)
"What are the key locations we'll visit?"

For each important location (2-6 depending on length):
- Name and description
- Significance to story
- Who inhabits or controls it
- Atmosphere and sensory details

#### History (LENGTH:novel)
"What historical events shaped this world?"

Timeline of 3-6 major events:
- What happened
- When
- How it affects the current story

More important for novels and secondary world fantasy.

#### Consistency Tracking (LENGTH:novel)
This section starts empty - fill during drafting to track:
- Place names and spellings
- Distance and travel times
- Technology or magic limitations
- Cultural details mentioned

#### Generate World Document

Write to `stories/{slug}/WORLD.md` from template `.planning/templates/world.md`

Process LENGTH:novel markers:
- **Novel:** Comprehensive world-building with history, culture, consistency tracking
- **Novella:** Moderate detail on essentials
- **Short story:** Basic setting and world rules only

### Step 7: Themes and Motifs (STORY-05)

Update PROJECT.md with thematic elements:

"Let's capture the deeper elements of your story."

**Core Themes (3-5):**
"What themes does your story explore?"

Examples:
- Power and corruption
- Loyalty vs. truth
- Coming of age
- Identity and belonging
- Redemption
- Sacrifice
- Love and loss

**Story Inspiration:**
"What inspired this story? What questions does it explore?"

Free-form notes about:
- What sparked the idea
- Questions you're exploring
- Why this story matters to you
- What you hope readers feel

**Target Audience:**
"Who is this story for?"

- Age range (YA, adult, etc.)
- Genre expectations
- Reader profile

**Voice and Style:**
"What are your narrative choices?"

- POV (first person, third limited, third omniscient, multiple)
- Tense (past, present)
- Tone (dark, light, humorous, serious, lyrical, sparse)
- Style notes (literary, commercial, experimental)

**Planned Word Count:**
"What's your target word count?"

Ranges by length:
- Short story: <7,500 words
- Novella: 7,500-40,000 words
- Novel: 40,000-100,000+ words

More specific targets help with pacing.

#### Update PROJECT.md

Add or enhance these sections in PROJECT.md:
- Core Themes (update list)
- Development Notes / Story Inspiration
- Target Audience
- Voice and Style
- Planned Length (word count)

### Step 8: Planning Completion

Update status and show completion summary:

```bash
# Update PROJECT.md frontmatter
status: planning-complete
```

Show completion message:

```
✓ In-Depth Planning Complete
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your comprehensive story foundation is built:

✓ Character profiles created (CHARACTERS.md)
✓ Plot structure mapped (OUTLINE.md)
✓ Character arcs defined (ARCS.md)
✓ World-building documented (WORLD.md)
✓ Themes and style captured (PROJECT.md)

Files created in stories/{slug}/:
- CHARACTERS.md ({character count} characters)
- OUTLINE.md (three-act structure{, subplots if novel})
- ARCS.md (transformation tracking)
- WORLD.md (setting and world details)

Template depth: {LENGTH-based}
- {For novel: Comprehensive sections with full detail}
- {For novella: Moderate depth focused on essentials}
- {For short story: Core elements for focused narrative}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Ready to Draft
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

You have a solid foundation for your {LENGTH} story.
These planning documents will guide your drafting and help
maintain consistency.

Next: When ready to draft, use /write:chapter (Phase 2)

Your planning documents are reference tools - revisit and
update them as the story evolves during drafting.
```

## Implementation Notes

### Length-Aware Template Processing

When generating documents from templates:

1. Read story length from PROJECT.md frontmatter
2. Read template file
3. Process LENGTH markers:

```bash
# If novel: include LENGTH:novel sections
# If shorter: remove LENGTH:novel sections

if [ "$LENGTH" = "novel" ]; then
  # Keep all content
  cat template.md > output.md
else
  # Remove LENGTH:novel sections
  sed '/<!--LENGTH:novel-->/,/<!--\/LENGTH:novel-->/d' template.md > output.md
fi
```

4. Replace {VARIABLE} placeholders with gathered content

### Prompting Style

- Conversational, not form-like
- Show examples for each question
- Allow "skip" or "I'll add this later" for optional sections
- Confirm understanding: "So your protagonist is a {description}. Is that right?"
- Encourage depth: "Tell me more about..." when answers are superficial

### Template Depth by Length

**Short story (< 7,500 words):**
- 2-3 characters max
- Simple three-act structure
- 3 growth moments per character
- Basic setting only
- Skip: subplots, extensive world-building, detailed scene lists

**Novella (7,500-40,000 words):**
- 3-4 characters
- Three acts with moderate scene detail
- 4-5 growth moments
- Moderate world-building
- 1-2 subplots if relevant

**Novel (40,000+ words):**
- 4+ characters
- Full three-act structure with detailed scenes
- 5-7 growth moments
- Comprehensive world-building
- Multiple subplots
- Full sections: history, culture, relationships, consistency tracking

### Error Handling

- If project doesn't exist: "Run /write:init first"
- If project is YOLO mode: "This project uses YOLO mode. Use /write:expand instead."
- If template files missing: Report path and offer to create from defaults
- If writer wants to skip a section: Mark with "TODO" placeholder for later

## Future Extensions

Phase 2 will add:
- `/write:chapter` for drafting chapters with planned character voices and arcs
- Consistency checking against planning documents
- Chapter progress tracking

Phase 3 will add:
- AI pattern detection in drafted chapters
- Voice authenticity verification against planned style
- Pacing analysis based on length targets
