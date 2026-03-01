# /write:check - Story Consistency Checker

Scan your story for consistency violations across all chapters. Detects contradictions in character details, timeline continuity, world rules, and POV consistency.

## Overview

**What it does:**
- Scans chapters against established story context (CHARACTERS.md, WORLD.md, all chapters)
- Detects 5 consistency violation types:
  1. Character detail contradictions (appearance, background)
  2. Character voice inconsistencies (speech patterns, tone)
  3. Timeline and continuity errors (temporal contradictions, event order)
  4. World rule violations (magic/tech limits, established facts)
  5. POV shifts within scenes (head-hopping, perspective breaks)
- Generates detailed CONSISTENCY-REPORT.md with locations and specific issues
- **Execution time:** 5-15 minutes for full story scan

## Prerequisites

Before running consistency check:
- Valid story project must exist
- At least 1 chapter written (`chapters/chapter-*.md` files)
- At least 1 context file exists (CHARACTERS.md or WORLD.md)

If prerequisites not met, the check will exit with guidance on what's needed.

## Workflow

### Step 1: Load story context

Read all baseline context files to build consistency checking foundation:

**From CHARACTERS.md (or yolo-characters.md):**
Extract for each character:
- **Physical description:** Appearance details like eye color, hair color/style, height, distinctive features (scars, tattoos), build
- **Voice/speech patterns:** Tone (formal/casual), vocabulary level, distinctive phrases or speech tics, accent notes
- **Personality traits:** Core consistent behaviors, habits, decision patterns
- **Background facts:** History, relationships, occupation, skills, traumas, motivations

Example extraction:
```
Sarah Martinez:
- Eyes: Green (mentioned Chapter 1)
- Hair: Long black hair, usually in braid
- Speech: Formal, reflects magical academy training, uses arcane terminology
- Personality: Stubborn, methodical, protective of students
- Background: Former academy professor, lost family in fire 10 years ago
```

**From WORLD.md (if exists):**
Extract:
- **World Rules > Key Rules:** Magic systems, technology limitations, supernatural laws
- **World Rules > Limitations:** Explicit "what can't happen" rules
- **Consistency Tracking > Details to Maintain:** Geography, travel times, cultural norms
- **Consistency Tracking > Established Facts:** Facts from prior chapters with references

**From all chapters (chapters/chapter-*.md):**
Build sequential chapter list with metadata:
- Chapter number and file
- POV character (from frontmatter)
- Word count
- Plot threads active in this chapter
- Scene count (marked by `---` scene breaks)

### Step 2: Scan for character detail inconsistencies (CONS-01, CONS-02)

For each chapter in sequence:

**Parse character mentions** in prose:
- Identify when each character appears
- Extract any physical descriptions mentioned
- Note dialogue and speech patterns
- Observe behavior and personality expression

**Check physical descriptions against CHARACTERS.md baseline:**

Flag inconsistencies:
- Eye color changes: "Chapter 3 describes blue eyes but CHARACTERS.md established brown eyes"
- Hair color/style changes: "Sarah's hair becomes blonde in Ch 5 with no explanation"
- Height contradictions: "Character described as tall in Ch 1, short in Ch 4"
- Missing/appearing physical features: "Scar mentioned in Ch 2 is gone in Ch 7"
- Build changes: "Described as thin, later as muscular, with no time passage or training"

**Check voice consistency against CHARACTERS.md patterns:**

Flag speech pattern violations:
- Formality shifts: "Character speaks casually in Ch 5 but CHARACTERS.md established formal speech reflecting magical training"
- Vocabulary level changes: "Simple vocabulary becomes complex without explanation"
- Distinctive phrase abandonment: "Character's signature phrase 'blessed be' never used after Ch 3"
- Accent disappears: "Irish accent noted in intro, gone by mid-story"

**Check personality consistency:**

Flag behavior contradictions:
- Actions against traits: "Stubborn character gives up easily in Ch 7 without character growth justification"
- Reaction inconsistencies: "Brave character suddenly fearful with no trauma explanation"
- Decision pattern violations: "Methodical character makes impulsive choice without setup"

**Report format for character violations:**
```
Character: Sarah Martinez
Issue: Eye color contradiction
Location: Chapter 7, paragraph 3
Baseline: CHARACTERS.md established green eyes
Violation: "Her brown eyes widened in surprise"
Severity: Critical
Suggestion: Change to "Her green eyes widened" or explain contact lenses/magic if intentional
```

### Step 3: Scan for timeline and continuity errors (CONS-03)

Build complete timeline from:
- Chapter Notes sections (explicit timeline markers)
- Prose content (implied time passage, dates mentioned)
- Event sequences and cause-effect chains

**Check for temporal contradictions:**
- **Event order violations:** "Event A happens after B in Ch 3, but Ch 6 says B happened after A"
- **Missing time/teleportation:** "Character in City A at end of Ch 4, in City B (5 days travel) at start of Ch 5 with no time skip"
- **Seasonal inconsistencies:** "Winter in Ch 2, summer in Ch 3, winter again in Ch 4, all within one week"
- **Age contradictions:** "Character stated as 25 in Ch 1, 30 in Ch 4 with only 2 months elapsed"
- **Knowledge before learning:** "Character knows secret in Ch 2, learns it in Ch 5"
- **Duration conflicts:** "Task takes 2 hours in Ch 1, same task takes 2 days in Ch 8 with no explanation"

**Timeline reconstruction example:**
```
Chapter 1: Monday morning - Sarah arrives at academy
Chapter 2: Monday afternoon - First class, meets Marcus
Chapter 3: [Missing: Tuesday entire day]
Chapter 4: Wednesday - Marcus references "yesterday's conversation" but they haven't spoken since Monday
^ Continuity gap: Tuesday missing, or Wednesday should reference Monday
```

**Report format for timeline violations:**
```
Issue: Event order contradiction
Chapters: 3, 6
Timeline conflict:
  - Ch 3: Fire happens, then Marcus leaves academy
  - Ch 6: Marcus mentions leaving academy before the fire
Severity: Critical
Suggestion: Reorder events in Ch 3 or clarify Marcus left temporarily, returned
```

### Step 4: Scan for world rule violations (CONS-04)

Read WORLD.md rules and check prose compliance.

**Magic/Technology/Science limitations:**
Flag when:
- Rule says "can't read minds" but Ch 6 has mind reading with no exception
- Magic costs vitality but character uses it 10 times in one scene with no fatigue
- Technology requires fuel, but device runs indefinitely
- Supernatural creatures can't cross water, but do so without explanation

**Established facts contradictions:**
- WORLD.md: "Travel to mountain takes 5 days"
  Chapter violation: Character travels in 1 day with no magic/transport explanation
- WORLD.md: "Magic requires spoken incantations"
  Chapter violation: Character performs magic silently

**Geography violations:**
- Map shows city east of river, chapter says west
- Distance contradictions (2 hours vs 2 days for same journey)
- Impossible routes (would require crossing impassable terrain)

**Cultural/Social rule violations:**
- WORLD.md: "Women cannot own property in this society"
  Chapter: Female character buys land without comment
- Check if intentional (character deliberately breaks rules) vs oversight

**Report format for world rule violations:**
```
Rule: Magic drains caster's vitality
Issue: Limitation ignored in combat scene
Location: Chapter 8, battle sequence
Rule states: "Each spell costs vitality; casters need rest after 3-4 uses" (WORLD.md line 47)
Chapter text: Sarah casts 15 spells in rapid succession, shows no fatigue
Severity: Critical
Suggestion: Reduce spell count, add exhaustion/consequences, or establish Sarah has special stamina
```

### Step 5: Scan for POV inconsistencies (CONS-05)

Extract POV from chapter frontmatter `pov: {character}` field.

**Scan prose for POV violations:**

**Head-hopping (accessing non-POV character thoughts):**
```
POV: Sarah (Chapter 5)
Violation: "Marcus wondered if she suspected the truth"
^ We're in Sarah's POV, cannot know what Marcus is wondering
Correct: "Marcus's expression suggested he wondered..." (Sarah's observation)
```

**Narrator omniscience exceeding POV limits:**
```
POV: Sarah (Chapter 3)
Violation: "In the tower three miles away, the council debated her fate"
^ Sarah can't know what's happening three miles away
```

**Perspective shifts mid-scene:**
```
POV: Third-person limited Sarah (Chapter 2)
Violation paragraph 10: Switches to first-person ("I felt...")
^ Tense/perspective consistency break
```

**Scene break requirements:**
If POV must shift within a chapter, requires scene break (`---`) between sections.

**Report format for POV violations:**
```
Chapter: 5
Scene: Confrontation with Marcus
Established POV: Sarah (third-person limited)
Violation: "Marcus wondered if she suspected the truth" (paragraph 8)
Location: Mid-scene, no scene break
Severity: Warning
Suggestion: Add scene break and switch to Marcus POV, or revise to "Marcus's expression suggested worry"
```

### Step 6: Generate CONSISTENCY-REPORT.md

Use `.planning/templates/consistency-report.md` template and populate:

**Frontmatter (YAML):**
```yaml
---
story: {project-slug}
checked: {ISO timestamp}
chapters_scanned: {count}
total_flags: {number}
critical: {count}
warnings: {count}
notes: {count}
---
```

**Summary Section:**
```
## Summary

Scanned {N} chapters totaling {word_count} words.

**Flags by severity:**
- Critical: {N} (require immediate attention)
- Warning: {N} (may be intentional, should verify)
- Note: {N} (verify if intentional)

**Flags by type:**
- Character details: {N}
- Character voice: {N}
- Timeline/Continuity: {N}
- World rules: {N}
- POV: {N}

**Most common issue:** {type}
```

**Findings Sections:**

For each violation type, populate section with findings:

```markdown
## Character Consistency

### Character: Sarah Martinez

**Issue:** Eye color contradiction
**Location:** Chapter 7, paragraph 3 (estimated line 42)
**Baseline:** CHARACTERS.md established green eyes (line 15)
**Violation:** "Her brown eyes widened in surprise"
**Severity:** Critical
**Suggestion:** Change to "green eyes" or explain if character uses colored contacts/magical disguise

[Repeat for each character violation]
```

**Next Steps Section:**
```
## Next Steps

1. Review each flagged issue in the report
2. For intentional changes:
   - Update CHARACTERS.md or WORLD.md baseline if detail evolved
   - Add note in ARCS.md explaining character growth
3. For genuine errors:
   - Revise chapter prose to fix contradiction
   - Update chapter file and save
4. Re-run `/write:check` after fixes to verify resolution
5. Mark fixed items in "Notes" section below
```

**Notes Section:**
```
## Writer Notes

{Empty section for writer annotations}

Mark fixes:
- [ ] Issue 1: Fixed in chapter 7
- [ ] Issue 2: Intentional, noted in ARCS.md
- [ ] Issue 3: Ignore (false positive)
```

Save report to: `CONSISTENCY-REPORT.md` in story project root.

Display to writer:
```
✓ Consistency check complete

Report: CONSISTENCY-REPORT.md
Chapters scanned: {N}
Total flags: {N} ({critical} critical, {warnings} warnings, {notes} notes)

Review report and address critical issues before finalizing manuscript.
```

## Examples

### Example 1: Character Detail Contradiction

**Setup:**
- CHARACTERS.md establishes Sarah has green eyes
- Chapter 1 confirms: "Her green eyes scanned the room"
- Chapter 7 says: "Her brown eyes widened"

**Detection:**
```
Character: Sarah Martinez
Issue: Eye color contradiction
Location: Chapter 7, paragraph 3
Baseline: Green eyes (CHARACTERS.md line 15, Chapter 1 paragraph 2)
Violation: Brown eyes (Chapter 7)
Severity: Critical
```

### Example 2: World Rule Violation

**Setup:**
- WORLD.md: "Teleportation magic is impossible in this universe"
- Chapter 9: Character teleports to escape danger

**Detection:**
```
Rule: Teleportation impossible
Issue: Character uses forbidden magic
Location: Chapter 9, escape sequence
Rule states: "Teleportation magic is impossible; violates conservation laws" (WORLD.md)
Chapter text: "Sarah teleported across the room"
Severity: Critical
Suggestion: Change to conventional escape (running, hiding) or explain exception
```

### Example 3: POV Shift

**Setup:**
- Chapter 4 frontmatter: `pov: Sarah`
- Mid-chapter: "Marcus knew she was lying" (Marcus's internal knowledge)

**Detection:**
```
Chapter: 4
POV: Sarah (third-person limited)
Violation: "Marcus knew she was lying"
Issue: Head-hopping - accessing Marcus's thoughts from Sarah POV
Severity: Warning
Suggestion: Revise to "Marcus's expression suggested he didn't believe her" (Sarah's observation)
```

## FAQ

**Q: What if an inconsistency is intentional character growth?**
A: Review the report and verify the change was deliberate. Update ARCS.md to document the character growth arc, or add a note in WORLD.md explaining the evolution. The checker flags all changes; you determine which are errors vs growth.

**Q: Can I customize what gets checked?**
A: Yes. The checker reads from CHARACTERS.md and WORLD.md, so those are your baseline truth sources. Update those files to reflect legitimate changes, and future checks will use the new baseline.

**Q: How often should I run consistency checks?**
A: Recommended after every 3-5 chapters, or before major revisions. For long novels, run at end of each act (25%, 50%, 75%, 100%) to catch issues early.

**Q: What if I don't have a WORLD.md?**
A: The checker will skip world rule checks and focus on character and POV consistency. For simple stories without complex world-building, this is fine.

**Q: Can I add my own custom checks?**
A: Not yet, but you can request additional violation types be added to the system.

**Q: What counts as "critical" vs "warning"?**
A:
- **Critical:** Objective contradiction (eye color changes, timeline impossible, world rule broken)
- **Warning:** Possible inconsistency that might be intentional (personality shift that could be growth, POV access that might be narrative choice)
- **Note:** Minor or subjective issues (verify if intentional)

**Q: Does this replace human proofreading?**
A: No. This catches structural consistency errors. You still need beta readers for plot holes, character motivation issues, pacing problems, and prose quality.

**Q: How long does a full check take?**
A: 5-15 minutes depending on chapter count:
- Short story (3 chapters): ~5 min
- Novella (10 chapters): ~8 min
- Novel (25+ chapters): ~12-15 min

**Q: What if the report has false positives?**
A: Mark them in the Notes section as "ignore" or "false positive." The checker errs on the side of flagging potential issues; you have final judgment.
