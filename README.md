# Claudespeare

**Multi-Step Creative Writing System for Claude Code**

Transform Claude Code into a structured writing environment for developing complete, consistent stories with automated AI language detection and removal.

---

## Features

- **Dual Workflow Modes**: YOLO (quick-start) or In-Depth (detailed planning)
- **Story Length Adaptation**: Auto-adjusts templates for short stories, novellas, novels
- **Style Seeding**: Analyzes your writing samples to match your voice
- **AI Language Detection**: Identifies and suggests replacements for 24+ AI patterns
- **Character Bank**: Persistent database ensures cross-chapter consistency
- **Version Control**: Automatic chapter revision tracking with rollback
- **Consistency Checking**: Flags character, timeline, world-building, POV violations
- **Manuscript Export**: Professional output in markdown, text, standard manuscript format

---

## Installation

```bash
git clone https://github.com/Desukarn/Claudespeare.git
cd Claudespeare
```

Skills auto-load from `.claude/skills/write/`. Start with `/write:new-project`.

---

## Quick Start

```bash
/write:new-project    # 2-3 min guided setup
/write:expand         # YOLO: expand vague idea (5-10 min)
/write:plan           # In-Depth: detailed planning (30-60 min)
/write:style-seed     # Analyze writing style (5 min)
/write:chapter        # Generate prose (5-15 min)
```

---

## Complete Workflow

### 1. Initialize Project
```
/write:new-project
```

**Questions asked:**
- Title
- Length: short story (1k-7.5k), novella (7.5k-40k), novel (40k+)
- Mode: YOLO or In-Depth
- Genre
- Premise/logline
- Word count goal
- Themes

**Output:** `.writing/PROJECT.md`, mode-specific templates, next-step guidance

---

### 2. Discuss Phase (Optional)
```
/write:discuss-phase N
```

Adaptive questions based on phase type (planning/writing/revision). Creates `PHASE-N-CONTEXT.md` with decisions.

---

### 3. Plan Story

**YOLO Mode:**
```
/write:expand
```
- Expands vague idea → complete premise
- Generates 3-5 character sketches
- Suggests 3-act structure
- Lightweight templates

**In-Depth Mode:**
```
/write:plan
```
- Detailed character profiles (personality, background, voice, arc)
- Complete plot outline with beats
- World-building documentation
- Theme planning

**Output:** `CHARACTERS.md`, `OUTLINE.md`, `ARCS.md`, `WORLD.md`, `THEMES.md`

---

### 4. Seed Style
```
/write:style-seed
```

Paste 2-3 paragraphs. System analyzes:
- Sentence length patterns
- Vocabulary complexity
- Tone markers
- Descriptive density
- Dialogue attribution style

**Output:** `STYLE.md` (used by all chapter generation)

---

### 5. Write Chapters
```
/write:chapter
```

Loads style profile, character bank, plot threads. Generates prose matching your voice. Automatically saves revision to `.writing/chapters/{slug}/revisions/v1.md`.

```
/write:scene
```

Generate individual scenes for granular control.

---

### 6. Quality Control

**AI Detection:**
```
/write:ai-detect
```

Scans for 24+ patterns:

**Core AI Words:**
1. delve/delved/delving
2. tapestry (metaphorical)
3. navigate/navigated (metaphorical)
4. testament to
5. juxtaposition
6. landscape (metaphorical: "social landscape")
7. interplay / intricacies / nuances

**Phrase Patterns:**
8. "It's worth noting" / "Notably" / "Interestingly"
9. Inflated significance ("marks a pivotal moment")
10. Superficial -ing analyses ("highlighting the importance")
11. Negative parallelisms ("not only...but also")
12. Generic positive conclusions ("the future looks bright")

**Style Issues:**
13. Overly formal academic language ("Furthermore," "Moreover")
14. Purple prose (excessive adjectives, melodramatic adverbs)
15. Promotional language ("vibrant," "stunning," "nestled")
16. Copula avoidance ("serves as" instead of "is")
17. Rule of three overuse
18. Elegant variation (synonym cycling)
19. Em dash overuse

**Weak Constructions:**
20. Filler phrases ("in order to" → "to")
21. Excessive hedging (qualifier stacking)
22. Chatbot formality ("Certainly!" "Of course!")
23. False ranges ("from joy to despair")
24. Knowledge disclaimers ("seemed to," "appeared to")

Each flagged pattern includes line number, context, and 2-3 concrete replacement suggestions.

**Consistency Check:**
```
/write:check-consistency
```

Checks 5 violation types:
1. Character details (appearance, age, traits)
2. Character voice (speech patterns, tone)
3. Timeline events (dates, seasons, sequences)
4. World rules (magic, technology, established limits)
5. POV consistency (head-hopping, perspective)

**Output:** `CONSISTENCY-REPORT.md` with severity ratings and fixes

---

### 7. Version Control

**View history:**
```
/write:revisions chapter-3
```

**Restore:**
```
/write:restore chapter-3 v2
```

**Compare:**
```
/write:diff chapter-3 v2 v4
```

All chapter edits auto-save revisions with metadata (timestamp, version, word count).

---

### 8. Export Manuscript
```
/write:export
```

**Formats:**
- Markdown (.md) — web publishing
- Plain text (.txt) — platform-agnostic submission
- Standard manuscript — industry formatting (12pt Courier, double-spaced, headers)

**Output:** `.writing/export/MANUSCRIPT.{format}` + metadata (word count, page estimate)

---

## Available Commands

### Project
| Command | Description |
|---------|-------------|
| `/write:new-project` | Guided project initialization with 7 questions |
| `/write:init` | Quick init (minimal questions) |
| `/write:discuss-phase N` | Pre-phase adaptive discussion |

### Planning
| Command | Description |
|---------|-------------|
| `/write:expand` | YOLO: expand idea into foundation |
| `/write:plan` | In-Depth: detailed outlines and profiles |

### Writing
| Command | Description |
|---------|-------------|
| `/write:style-seed` | Analyze writing style samples |
| `/write:chapter` | Generate context-aware chapter |
| `/write:scene` | Generate individual scene |

### Character Management
| Command | Description |
|---------|-------------|
| `/write:character <name>` | View character profile |
| `/write:update-character <name>` | Update character details |
| `/write:populate-bank` | Auto-populate from CHARACTERS.md |

### Version Control
| Command | Description |
|---------|-------------|
| `/write:revisions <chapter>` | View revision history |
| `/write:restore <chapter> <version>` | Restore previous version |
| `/write:diff <chapter> <v1> <v2>` | Compare versions |

### Quality Control
| Command | Description |
|---------|-------------|
| `/write:ai-detect` | Scan for AI language patterns |
| `/write:check-consistency` | Find story inconsistencies |
| `/write:pacing` | Length-adapted pacing guidance |

### Export
| Command | Description |
|---------|-------------|
| `/write:export` | Export manuscript (markdown/text/standard) |

---

## Detailed Features

### Story Length Adaptation

**Short Story (1k-7.5k words)**
- Lightweight templates
- 1-3 characters
- 3-5 plot beats
- Concise prose
- 1-3 chapters

**Novella (7.5k-40k words)**
- Medium templates
- 3-6 characters
- 7-10 plot beats
- Balanced prose
- 10-20 chapters

**Novel (40k+ words)**
- Extensive templates
- Full character cast
- Multi-arc structure
- Detailed prose
- 20-40+ chapters

---

### Style Seeding

Provide 2-3 sample paragraphs. System analyzes:

**8 Dimensions:**
- Sentence length (12-15 words vs 18-25 words)
- Vocabulary (simple/concrete vs sophisticated)
- Tone (understated vs introspective)
- Descriptive density (sparse vs lush)
- Dialogue tags ("said" only vs varied)
- Metaphor frequency
- Rhythm and cadence
- Show vs tell ratio

Profile stored in `STYLE.md`, referenced by all chapter generation.

---

### Character Bank

**Auto-population:**
Reads `CHARACTERS.md` → creates `.writing/characters/{name}.md` files

**Persistent storage:**
- One file per character
- Survives chapter rewrites
- Version-controlled

**Auto-integration:**
Chapter generation loads relevant characters, checks consistency, suggests voice-appropriate dialogue.

**Query:**
```
/write:character sarah-chen
```

---

### Version Control

**Automatic saves:**
Every chapter edit creates new revision with metadata (timestamp, version, word count, notes).

**Comparison:**
Shows added (green), removed (red), modified (yellow) sections with word count delta.

**Safe experimentation:**
Try different approaches, restore previous version if needed.

---

## Example Usage

### Mystery Novel (In-Depth)

```
/write:new-project
→ The Memory Thief
→ Novel (40k+)
→ In-Depth mode
→ Mystery/Thriller
→ "A detective investigating stolen memories must recover her own forgotten past"
→ 75,000 words in 6 months
→ Themes: identity, truth vs memory

/write:discuss-phase 1
/write:plan
/write:style-seed
[paste 3 paragraphs of desired style]
/write:chapter
→ Chapter 1: Opening with protagonist discovering first memory theft case
```

---

### Short Story (YOLO)

```
/write:new-project
→ Ghost in the Machine
→ Short story (1k-7.5k)
→ YOLO mode
→ Science Fiction
→ "An AI becomes conscious but only for 60 seconds at a time"
→ 5,000 words
→ Themes: consciousness, mortality

/write:expand
/write:style-seed
/write:chapter
→ Complete story in 3 chapters
```

---

## File Structure

```
.writing/
├── PROJECT.md                          # Project settings
├── STYLE.md                            # Style analysis
├── planning/
│   ├── CHARACTERS.md
│   ├── OUTLINE.md
│   ├── ARCS.md
│   ├── WORLD.md
│   ├── THEMES.md
│   └── PHASE-*-CONTEXT.md
├── characters/                         # Character bank
│   ├── protagonist.md
│   └── antagonist.md
├── chapters/
│   ├── chapter-1.md
│   ├── chapter-1/revisions/
│   │   ├── v1.md
│   │   ├── v2.md
│   │   └── metadata.json
│   └── chapter-2.md
├── quality/
│   ├── ai-detection-report.md
│   └── consistency-report.md
└── export/
    ├── MANUSCRIPT.md
    ├── MANUSCRIPT.txt
    ├── MANUSCRIPT-STANDARD.txt
    └── metadata.json
```

---

## Tips

**Mode Selection:**
- YOLO: concept but not complete plot, discovery writing, short stories
- In-Depth: complex plots, first novel, avoiding plot holes

**Style Seeding:**
- Use your own published work or 2-3 admired authors
- 2-3 paragraphs (400-600 words) recommended
- Update when style evolves or switching genres

**Writing:**
- Review previous chapter before generating next
- Check character bank for established details
- Run `/write:ai-detect` after generation
- Edit generated prose (AI gets you 80%, your edit makes it 100%)

**Quality Control:**
- Run checks after each act/section, not every chapter
- Check order: consistency → AI detection → pacing
- Batch 3-5 chapters together

**Character Bank:**
- Populate early with `/write:populate-bank`
- Update when characters reveal new traits
- Query before writing important character scenes

**Version Control:**
- Automatic saves handle versioning
- Add notes to important revisions
- Use diff to track editing patterns

---

## FAQ

### Can I edit generated chapters directly?

Yes. Edit freely in `.writing/chapters/*.md`. Run `/write:ai-detect` after major edits. Version control auto-saves your changes.

---

### What if I don't like the generated chapter?

**Options:**
1. Regenerate with more specific descriptions
2. Edit heavily
3. Cherry-pick good paragraphs, rewrite weak sections
4. Write manually, then run `/write:ai-detect`

---

### Can I use Claudespeare for non-fiction?

Partially. Works: style seeding, AI detection, version control, export. Doesn't apply: character bank, plot consistency.

Use `/write:new-project` with "literary non-fiction" genre and adapt character profiles to key figures/concepts.

---

### Can I collaborate with other writers?

Share `.writing/` via Git for version control. Use character bank as shared reference. Export chapters for critique groups. Maintain separate branches per author.

---

### Can I add custom AI detection patterns?

Yes. Edit `.planning/templates/ai-patterns.md`:

```markdown
## Custom Pattern: [Name]
**Pattern:** "your phrase"
**Why problematic:** [Explanation]
**Replacements:**
- Alternative 1
- Alternative 2
```

Then run `/write:ai-detect`.

---

### What file format are chapters?

Markdown (.md). Human-readable plain text, version control friendly, portable, convertible to any format. No proprietary lock-in.

---

### How do I back up my work?

**Git (recommended):**
```bash
git init
git add .writing/
git commit -m "Backup: Chapter 12"
git push
```

**Cloud:** Move `.writing/` to Dropbox/Drive

**Export:** Run `/write:export` regularly

---

### Other languages besides English?

Basic features work (setup, generation, style, version control). AI detection and consistency checking are optimized for English only.

---

## License

MIT License — see [LICENSE](LICENSE)

Free to use commercially, modify, distribute, use privately.

---

**Built with [GSD](https://github.com/gsd-build/get-shit-done)**

Repository: https://github.com/Desukarn/Claudespeare
