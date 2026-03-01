---
phase: 04-workflow-orchestration-gsd-integration
plan: 02
subsystem: workflow-orchestration
tags: [workflow, discussion, phase-planning, adaptive-questions]

dependency_graph:
  requires: [04-01]
  provides: [phase-discussion-flow, adaptive-questioning, context-capture]
  affects: [write-skill, workflow-patterns]

tech_stack:
  added: []
  patterns: [adaptive-questioning, phase-detection, workflow-orchestration]

key_files:
  created:
    - .claude/skills/write/discuss-phase.md
  modified:
    - .claude/skills/write/SKILL.md

decisions:
  - "Position /write:discuss-phase between /write:init and /write:expand in command sequence"
  - "Use phase detection logic based on phase number and project state (planning vs writing vs revision)"
  - "Capture decisions in PHASE-N-CONTEXT.md files within story project directories"
  - "Provide adaptive questions tailored to phase type (4 questions for planning, 6 for writing, 4 for revision)"
  - "Include resume support for existing phase contexts with archive/update options"
  - "Implement workflow orchestration guidance with explicit next-step commands"

metrics:
  duration_minutes: 4
  tasks_completed: 3
  files_created: 1
  files_modified: 1
  lines_added: 908
  commits: 3
  completed_date: "2026-02-27"
---

# Phase 04 Plan 02: Adaptive Discussion Workflow Summary

**One-liner:** Phase-based discussion workflow with adaptive questioning before planning, writing, and revision phases, capturing decisions in PHASE-N-CONTEXT.md files

## What Was Built

Created `/write:discuss-phase N` command that conducts adaptive discussions before each writing phase, similar to GSD's discuss-phase workflow. The system asks clarifying questions tailored to the phase type (planning, writing, or revision), captures the writer's decisions in structured PHASE-N-CONTEXT.md files, and provides clear next-step guidance for workflow progression.

**Key capabilities:**
- Phase detection (planning vs writing vs revision based on context)
- Adaptive questioning with 4-6 questions per phase type
- Decision capture in PHASE-N-CONTEXT.md with goals, decisions, focus areas, concerns, and next steps
- Workflow orchestration guidance with explicit command sequences
- Resume support for existing phase contexts with update/archive options
- Integration with all existing write commands (expand, plan, chapter, detect, check, export)

**User experience:**
- Numbered questions for clear flow
- Examples provided throughout (10 instances)
- Project context displayed at start (title, genre, progress)
- Encouraging, supportive language
- 10-20 minute discussion duration depending on phase complexity

## Implementation Details

### Task 1: Create Adaptive Discussion Workflow

**File created:** `.claude/skills/write/discuss-phase.md` (885 lines)

**Workflow structure:**
1. **Step 1: Validate Context** - Check PROJECT.md exists, validate phase number, load existing PHASE-N-CONTEXT.md if resuming
2. **Step 2: Phase Detection** - Determine phase type based on phase number and project state
3. **Step 3: Adaptive Questions** - Ask tailored questions for planning/writing/revision phases
4. **Step 4: Capture Decisions** - Create PHASE-N-CONTEXT.md with structured content
5. **Step 5: Workflow Orchestration Guidance** - Provide clear next steps based on phase type
6. **Step 6: Confirmation and Summary** - Display summary for writer confirmation

**Phase-specific questions:**

**Planning phases (Phase 1):**
- Q1: Planning approach (YOLO Expand vs In-Depth Planning)
- Q2: Story elements to develop (characters, plot, arcs, world, style)
- Q3: Detail level preference (light, moderate, comprehensive)
- Q4: Specific concerns or things to explore

**Writing phases (Phase 2+):**
- Q1: Which chapters to write
- Q2: Plot beats from outline to cover
- Q3: Character arcs to focus on
- Q4: Pacing or style adjustments
- Q5: Consistency concerns from previous chapters
- Q6: Plan to run /write:detect for AI language

**Revision phases:**
- Q1: Which chapters need revision
- Q2: Issues identified (plot holes, consistency, pacing, etc.)
- Q3: Use /write:check for consistency validation
- Q4: Ready for export or more drafting needed

**PHASE-N-CONTEXT.md format:**
```markdown
---
phase: {N}
phase_type: {planning|writing|revision}
created: {timestamp}
updated: {timestamp if resuming}
---

# Phase {N} Context

## Goals
## Decisions
## Focus Areas
## Concerns
## Next Steps
```

**Workflow orchestration examples:**
- Planning → `/write:expand` or `/write:plan` → `/write:style` → `/write:discuss-phase 2`
- Writing → `/write:chapter N` → `/write:detect` → `/write:check` → `/write:discuss-phase N+1`
- Revision → `/write:check` → fix issues → `/write:export`

**Resume support:**
- Display existing context if PHASE-N-CONTEXT.md exists
- Offer to review/update or start fresh
- Archive previous context with timestamp
- Preserve original decisions with "Updated:" markers

**Commit:** `4c0b595` - feat(04-02): create adaptive discussion workflow

### Task 2: Update Skill Index and Workflow Description

**File modified:** `.claude/skills/write/SKILL.md`

**Changes:**
1. **Added command entry** for `/write:discuss-phase N` between `/write:init` and `/write:expand`
2. **Updated Complete Workflow section** to show full 10-step phase-based flow:
   - Step 1: `/write:new-project` - Initialize
   - Step 2: `/write:discuss-phase 1` - Clarify planning approach
   - Step 3: `/write:expand` or `/write:plan` - Develop foundation
   - Step 4: `/write:style` - Define voice
   - Step 5: `/write:discuss-phase 2` - Plan writing phase
   - Step 6: `/write:chapter N` - Draft chapters
   - Step 7: `/write:detect` - Check AI patterns
   - Step 8: `/write:check` - Validate consistency
   - Step 9: `/write:discuss-phase 3` - Plan revisions
   - Step 10: `/write:export` - Compile manuscript
3. **Updated skill description** to mention "phase-based workflow orchestration with adaptive discussions"

**Positioning rationale:**
- Placed after `/write:init` (initialization comes first)
- Before `/write:expand` (discussion happens before planning/execution)
- Logical flow: init → discuss → plan → execute

**Commit:** `5c0be31` - feat(04-02): update skill index with discuss-phase command

### Task 3: Validate Workflow Consistency

**Verification performed:**

**Requirement coverage:**
- FLOW-04: Writer can run /write:discuss-phase N ✓
- FLOW-05: Adaptive questions based on phase goals ✓
- FLOW-06: Consistent workflow pattern (new → discuss → plan → execute → repeat) ✓
- FLOW-07: Clear next-step guidance provided ✓

**Adaptive logic:**
- Phase type detection for planning/writing/revision ✓
- Questions genuinely adaptive (different per phase type) ✓
- Context capture comprehensive ✓
- Next steps match phase type ✓

**Integration:**
- Reads PROJECT.md for story context ✓
- Creates PHASE-N-CONTEXT.md in project directory ✓
- References other commands appropriately (chapter, detect, check, expand, plan, export) ✓
- Workflow guidance matches existing command structure ✓

**User experience:**
- Questions clear and answerable (numbered Q1-Q6) ✓
- Examples provided (10 instances) ✓
- Resume support reduces friction ✓
- Next steps explicit and actionable (33 command references) ✓
- Presentation style guidelines included ✓

**Must-haves validation:**
- discuss-phase.md: 885 lines (exceeds 250 minimum) ✓
- All truths satisfied ✓
- All key links present ✓
- SKILL.md contains "/write:discuss-phase" ✓

**Commit:** `250e081` - chore(04-02): validate workflow consistency

## Deviations from Plan

None - plan executed exactly as written.

All tasks completed as specified:
- Task 1: Created comprehensive adaptive discussion workflow (885 lines)
- Task 2: Updated SKILL.md with command entry and workflow description
- Task 3: Validated workflow consistency and verified all requirements

No blocking issues encountered. No authentication gates. No scope changes needed.

## Integration Points

**Reads from:**
- `PROJECT.md` - Story title, genre, length, mode, progress, word count
- `PHASE-{N}-CONTEXT.md` - Existing phase context if resuming
- `CONSISTENCY-REPORT.md` - Detect revision phase
- `AI-DETECTION-REPORT.md` - Detect revision phase
- `chapters/*.md` - Understand current chapter progress

**Creates:**
- `PHASE-{N}-CONTEXT.md` - Captured decisions and next steps

**References in guidance:**
- `/write:new-project` - Project initialization
- `/write:expand` - YOLO planning
- `/write:plan` - In-Depth planning
- `/write:style` - Voice definition
- `/write:chapter` - Chapter drafting
- `/write:detect` - AI language detection
- `/write:check` - Consistency validation
- `/write:pacing` - Pacing guidance
- `/write:export` - Manuscript compilation

**Workflow pattern:**
```
new-project → discuss-phase 1 → expand/plan → style →
discuss-phase 2 → chapter N × M → detect → check →
discuss-phase 3 (if revision needed) → export
```

## Testing Notes

**Manual verification recommended:**

1. **Command availability:**
   - Check SKILL.md lists `/write:discuss-phase` with clear description ✓
   - Verify workflow file exists and is comprehensive ✓
   - Confirm command positioned correctly in sequence ✓

2. **Adaptive questioning:**
   - Verify planning phase has 4 questions ✓
   - Verify writing phase has 6 questions ✓
   - Verify revision phase has 4 questions ✓
   - Confirm questions differ meaningfully by phase type ✓

3. **Context capture:**
   - Verify PHASE-N-CONTEXT.md format is well-structured ✓
   - Check frontmatter includes phase, phase_type, timestamps ✓
   - Confirm sections: Goals, Decisions, Focus Areas, Concerns, Next Steps ✓

4. **Workflow guidance:**
   - Verify planning phase guidance mentions /write:expand or /write:plan ✓
   - Verify writing phase guidance includes chapter drafting sequence ✓
   - Verify revision phase guidance covers check → fix → export ✓
   - Confirm all guidance includes estimated time ranges ✓

5. **Resume support:**
   - Verify existing context detection logic present ✓
   - Confirm update/archive options documented ✓
   - Check timestamp preservation for updated decisions ✓

## Success Criteria Met

- [x] Writer can run `/write:discuss-phase N` before each phase
- [x] System asks adaptive questions based on phase type and goals
- [x] Decisions are captured in PHASE-N-CONTEXT.md
- [x] Writer receives clear next-step guidance matching their phase
- [x] Workflow follows consistent GSD-like pattern across all phases
- [x] Complete Workflow documentation enables self-guided progression

All success criteria from plan satisfied.

## Files Changed

**Created:**
- `.claude/skills/write/discuss-phase.md` (885 lines)
  - Comprehensive adaptive discussion workflow
  - Phase detection, adaptive questioning, context capture
  - Workflow orchestration guidance
  - Resume support, error handling, integration documentation

**Modified:**
- `.claude/skills/write/SKILL.md` (+23 lines, -2 lines)
  - Added `/write:discuss-phase N` command entry
  - Updated Complete Workflow section with 10-step flow
  - Enhanced skill description with workflow orchestration mention

## Metrics

- **Duration:** 4 minutes
- **Tasks completed:** 3/3
- **Files created:** 1
- **Files modified:** 1
- **Lines added:** 908 total (885 new file, 23 modified)
- **Commits:** 3
- **Requirements satisfied:** FLOW-04, FLOW-05, FLOW-06, FLOW-07

## Next Steps

This plan completes the adaptive discussion workflow for the write skill. The workflow is now ready for use:

1. Writers can run `/write:discuss-phase 1` before planning to clarify their approach
2. Writers can run `/write:discuss-phase 2+` before each writing phase to plan chapter batches
3. Writers can run `/write:discuss-phase N` before revisions to plan fixes

**Recommended follow-up:**
- Test the workflow with a real story project
- Gather user feedback on question clarity and usefulness
- Consider adding example PHASE-N-CONTEXT.md files to documentation

**Phase 4 progression:**
- Plan 04-01: ✓ Complete (Comprehensive project initialization)
- Plan 04-02: ✓ Complete (Adaptive discussion workflow) ← Current
- Plan 04-03: Pending (remaining Phase 4 work)

## Self-Check: PASSED

**Created files verification:**
```bash
[ -f ".claude/skills/write/discuss-phase.md" ] # ✓ FOUND
```

**Modified files verification:**
```bash
[ -f ".claude/skills/write/SKILL.md" ] # ✓ FOUND
grep -q "discuss-phase" .claude/skills/write/SKILL.md # ✓ FOUND
```

**Commits verification:**
```bash
git log --oneline --all | grep "4c0b595" # ✓ FOUND (Task 1)
git log --oneline --all | grep "5c0be31" # ✓ FOUND (Task 2)
git log --oneline --all | grep "250e081" # ✓ FOUND (Task 3)
```

**Line count verification:**
```bash
wc -l .claude/skills/write/discuss-phase.md # 885 lines (exceeds 250 minimum) ✓
```

All self-checks passed. Files exist, commits recorded, line counts verified.
