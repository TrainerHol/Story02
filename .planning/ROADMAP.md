# Roadmap: Claudespeare

## Overview

Claudespeare transforms Claude Code into a structured creative writing environment supporting both quick-start (YOLO) and in-depth workflows for short stories through novels. Phase 1 establishes dual-mode project initialization with story length adaptation. Phase 2 builds the core writing system with style seeding and comprehensive AI language detection (10 patterns). Phase 3 adds consistency checking and manuscript export capabilities. Phase 4 implements GSD-like workflow orchestration with comprehensive project initialization, adaptive discussion phases, character bank persistence, and chapter version control, completing the v1 writer's toolkit.

## Phases

**Phase Numbering:**
- Integer phases (1, 2, 3): Planned milestone work
- Decimal phases (2.1, 2.2): Urgent insertions (marked with INSERTED)

Decimal phases appear between their surrounding integers in numeric order.

- [ ] **Phase 1: Project Foundation & Adaptive Story Setup** - Initialize projects with story length, workflow mode (YOLO vs In-Depth), and complete story elements
- [ ] **Phase 2: Style-Aware Writing & Comprehensive AI Detection** - Core writing workflow with style seeding and 10-pattern AI detection
- [ ] **Phase 3: Consistency, Pacing & Export** - Consistency checking, length-adapted pacing, and manuscript output
- [ ] **Phase 4: Workflow Orchestration & GSD Integration** - GSD-like workflow with new-project initialization, discuss-phase, character bank, and version control

## Phase Details

### Phase 1: Project Foundation & Adaptive Story Setup
**Goal**: Writers can initialize story projects with configurable depth (short story vs novel, YOLO vs In-Depth mode) and define all foundational story elements
**Depends on**: Nothing (first phase)
**Requirements**: INIT-01, INIT-02, INIT-03, INIT-04, INIT-05, YOLO-01, YOLO-02, YOLO-03, YOLO-04, STORY-01, STORY-02, STORY-03, STORY-04, STORY-05, LENGTH-01, LENGTH-02
**Success Criteria** (what must be TRUE):
  1. Writer can select story length (short story, novella, novel) and system adapts template depth accordingly
  2. Writer can choose YOLO mode (quick start from vague idea) or In-Depth mode (detailed planning)
  3. In YOLO mode: Writer provides vague idea, system expands to premise, generates basic character sketches, and suggests simple plot structure
  4. In In-Depth mode: Writer can create detailed character profiles (name, role, personality, background, voice)
  5. In In-Depth mode: Writer can outline plot structure with major beats, define character arcs, document world-building, and define themes/motifs
  6. Short story projects use lighter templates (minimal planning), novel projects use extensive templates (full planning depth)
  7. All story elements are stored in structured files and retrievable for later phases
  8. Writer can skip directly to writing phase in YOLO mode without extensive planning
**Plans**: 3 plans in 2 waves

Plans:
- [ ] 01-01-PLAN.md — Initialization system and mode selection
- [ ] 01-02-PLAN.md — YOLO mode implementation with light templates
- [ ] 01-03-PLAN.md — In-Depth mode and template adaptation

### Phase 2: Style-Aware Writing & Comprehensive AI Detection
**Goal**: Writers can generate prose matching their personal style with comprehensive AI language pattern detection, removal, and word count tracking
**Depends on**: Phase 1
**Requirements**: STYLE-01, STYLE-02, STYLE-03, STYLE-04, WRITE-01, WRITE-02, WRITE-03, WRITE-04, WRITE-05, WRITE-06, WRITE-07, WRITE-08, WRITE-09, WRITE-10, AI-01, AI-02, AI-03, AI-04, AI-05, AI-06, AI-07, AI-08, AI-09, AI-10
**Success Criteria** (what must be TRUE):
  1. Writer can provide sample paragraphs of desired writing style for system analysis
  2. System analyzes style samples for patterns (sentence length, vocabulary, tone, formality)
  3. Writer can define voice characteristics (POV, tense, formality level)
  4. Writer can set word count goals for project (short story: 1k-7.5k, novella: 7.5k-40k, novel: 40k+)
  5. System tracks current word count across all chapters and displays progress
  6. Writer can set chapter target word counts
  7. Writer can generate chapters and scenes with story context awareness
  8. Generated prose matches writer's style seed patterns (sentence structure, vocabulary, tone)
  9. System maintains character voice consistency across chapters
  10. System tracks plot threads to prevent dropped storylines
  11. System adapts output length based on story type (short story = concise, novel = detailed descriptions)
  12. System flags 10 AI language patterns: "delve/delved/delving", "tapestry", "navigate/navigated", "testament to", "juxtaposition", overly formal academic language, "it's worth noting" phrases, purple prose patterns
  13. System provides concrete replacement suggestions for each flagged phrase
  14. Writer can add custom phrases to detection list
**Plans**: 4 plans in 2 waves

Plans:
- [ ] 02-01-PLAN.md — Style seeding system with analysis and voice configuration
- [ ] 02-02-PLAN.md — Chapter generation with context awareness and style matching
- [ ] 02-03-PLAN.md — Word count tracking and goal management
- [ ] 02-04-PLAN.md — AI pattern detection with 10 patterns and custom phrases

### Phase 3: Consistency, Pacing & Export
**Goal**: Writers can verify story consistency with length-adapted pacing guidance and export completed manuscripts in standard format
**Depends on**: Phase 2
**Requirements**: CONS-01, CONS-02, CONS-03, CONS-04, CONS-05, LENGTH-03, LENGTH-04, OUT-01, OUT-02, OUT-03, OUT-04
**Success Criteria** (what must be TRUE):
  1. System tracks character details (appearance, personality, background, voice) across all chapters
  2. System flags character inconsistencies when detected (e.g., eye color changes, voice shifts)
  3. System tracks timeline events and flags continuity errors
  4. System tracks world rules and flags violations
  5. System maintains POV consistency within scenes
  6. System suggests appropriate chapter count based on story type (short story vs novel)
  7. System provides pacing guidance adapted to story length
  8. Writer can export individual chapters as properly formatted markdown files
  9. Writer can compile full manuscript from all chapters
  10. Exported files follow standard manuscript format (title page, headers, page numbers)
  11. Writer can export to .txt format for submission platforms
**Plans**: 3 plans in 1 wave

Plans:
- [ ] 03-01-PLAN.md — Consistency checking system with 5 violation types
- [ ] 03-02-PLAN.md — Length-adapted pacing guidance and chapter recommendations
- [ ] 03-03-PLAN.md — Manuscript export with 3 formats (markdown, text, standard manuscript)

### Phase 4: Workflow Orchestration & GSD Integration
**Goal**: Writers experience smooth GSD-like workflow with comprehensive project initialization, adaptive discussion phases, persistent character bank, and chapter version control
**Depends on**: Phase 3
**Requirements**: FLOW-01, FLOW-02, FLOW-03, FLOW-04, FLOW-05, FLOW-06, FLOW-07, BANK-01, BANK-02, BANK-03, BANK-04, BANK-05, BANK-06, VER-01, VER-02, VER-03, VER-04, VER-05
**Success Criteria** (what must be TRUE):
  1. Writer can run `/write:new-project` and system asks comprehensive clarifying questions (story type, genre, mode, premise)
  2. System presents clear options at each workflow step (like GSD's option presentation)
  3. Writer can run `/write:discuss-phase N` before planning a writing phase
  4. Discussion phase asks adaptive questions based on phase goals (e.g., "What chapters will you write in this phase?")
  5. Workflow follows consistent pattern: new project → discuss phase → plan phase → execute phase → revisions → next phase
  6. System provides clear next-step guidance after each command (e.g., "Run /write:discuss-phase 1 to begin Phase 1")
  7. Character bank persists across all chapters in `.writing/characters/` directory
  8. Writer can query character bank with `/write:character <name>` to view full profile
  9. Writer can update character bank with `/write:update-character <name>`
  10. Chapter generation automatically references character bank for consistency
  11. System stores chapter revision history in `.writing/chapters/<name>/revisions/`
  12. Writer can view revision list with `/write:revisions <chapter-name>`
  13. Writer can restore previous version with `/write:restore <chapter-name> <revision-number>`
  14. Each revision includes metadata (timestamp, revision number, word count)
  15. Writer can compare two revisions with `/write:diff <chapter-name> <rev1> <rev2>`
**Plans**: 3 plans in 2 waves

Plans:
- [ ] 04-01-PLAN.md — Comprehensive project initialization (/write:new-project) with questioning workflow
- [ ] 04-02-PLAN.md — Adaptive discussion phase (/write:discuss-phase) and workflow orchestration
- [ ] 04-03-PLAN.md — Character bank system and chapter version control

## Progress

**Execution Order:**
Phases execute in numeric order: 1 → 2 → 3 → 4

| Phase | Plans Complete | Status | Completed |
|-------|----------------|--------|-----------|
| 1. Project Foundation & Adaptive Story Setup | 0/3 | Planned | - |
| 2. Style-Aware Writing & Comprehensive AI Detection | 0/4 | Planned | - |
| 3. Consistency, Pacing & Export | 0/3 | Planned | - |
| 4. Workflow Orchestration & GSD Integration | 2/3 | In Progress|  |
