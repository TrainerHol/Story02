# Claudespeare - Multi-Step Story Writing System

## What This Is

A Claude Code skill/plugin similar to GSD (Get Shit Done) but specifically designed for writing stories and novels. It provides a structured, multi-step workflow for authors working with Claude to develop long-form creative writing projects.

## Core Concept

Based on the GSD architecture (workflows, templates, agents), Claudespeare guides writers through the creative process from concept to completed manuscript. Like GSD manages software development phases, Claudespeare manages story development phases.

## Key Differences from GSD

**What to Keep:**
- Multi-step workflow system with phases
- Agent spawning architecture for parallel work
- State management and tracking
- Command system (skills)
- Planning directory structure

**What to Remove:**
- Test generation and execution
- Human verification checkpoints (stories are subjective)
- Code linting/compilation checks
- Git branching strategies
- Technical verification systems

**What to Add:**
- AI language detection and removal hooks (catch phrases like "delve into", "tapestry", "navigate", etc.)
- Story consistency checking across chapters
- Character development tracking
- Plot thread management
- Writing style consistency checks
- Word count and pacing analysis

## Typical Workflow

1. **Story Concept Phase**: Gather premise, genre, themes, character sketches
2. **Outline Phase**: Develop plot structure, character arcs, major scenes
3. **Draft Phase**: Write chapters/scenes with consistency hooks
4. **Revision Phase**: Polish prose, remove AI clichés, strengthen voice

## Features Needed

### Story Planning
- Genre and theme definition
- Character profile creation
- World building documentation
- Plot outline structuring

### Writing System
- Chapter/scene generation with context awareness
- Character consistency checking (personality, voice, development)
- Plot thread tracking (ensure no dropped storylines)
- Pacing analysis

### Quality Checks
- **AI Language Filter**: Flag and suggest alternatives for common AI phrases
  - "delve/delved/delving"
  - "tapestry"
  - "navigate/navigated"
  - "testament to"
  - "juxtaposition"
  - Overly formal academic language
  - Purple prose patterns
- **Consistency Checker**: Track character details, world rules, timeline
- **Voice Analyzer**: Maintain consistent narrative voice

### Output Management
- Export chapters to standard manuscript format
- Compile full manuscript
- Generate synopsis and query materials

## Technical Approach

- Fork GSD architecture as starting point
- Node.js CLI tool (like gsd-tools.cjs)
- Workflow markdown files for each phase
- Agent system for parallel processing
- Template system for story documents

## Success Criteria

- Writers can go from concept to complete draft through guided workflow
- AI language is automatically flagged for revision
- Story consistency is maintained across chapters
- Workflow feels natural for creative writing (not overly technical)
