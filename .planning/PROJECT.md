# Claudespeare

## What This Is

A Claude Code skill/plugin for writing stories and novels through a structured, multi-step workflow. Built on GSD architecture but tailored for creative writing, it guides authors from concept to completed manuscript with AI language detection, consistency checking, and story development tools.

## Core Value

Writers can develop complete, consistent long-form stories with automated detection and removal of AI-generated language patterns, ensuring authentic human voice.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Writers can initialize new story projects with genre, themes, and premise
- [ ] Writers can create and track character profiles with consistency checking
- [ ] Writers can outline plot structure with major beats and character arcs
- [ ] Writers can generate chapters/scenes with story context awareness
- [ ] System flags common AI language patterns for revision ("delve", "tapestry", "navigate", etc.)
- [ ] System tracks character details and flags inconsistencies
- [ ] System tracks plot threads to prevent dropped storylines
- [ ] Writers can export chapters to standard manuscript format
- [ ] Writers can compile full manuscript from individual chapters

### Out of Scope

- Test generation and execution — stories are subjective, no automated tests
- Human verification checkpoints — creative work doesn't need approval gates
- Git branching strategies — simple linear workflow sufficient
- Code linting/compilation checks — not applicable to prose
- Real-time collaborative writing — single author workflow
- Publishing platform integration — defer to manual submission

## Context

**Inspired by GSD**: The Get Shit Done workflow system (https://github.com/gsd-build/get-shit-done) provides the architectural foundation - multi-step workflows, agent spawning, state tracking, and command system. Claudespeare adapts this for creative writing instead of software development.

**Target users**: Fiction writers using Claude Code who want structured guidance through the writing process without losing creative control.

**Key innovation**: Automated AI language detection. Writers struggle to identify when Claude's prose sounds "too AI" - this system actively flags common patterns and suggests more human alternatives.

## Constraints

- **Architecture**: Must follow GSD plugin patterns (skills, workflows, agents, templates)
- **Simplicity**: 3 phases maximum for v1 - keep workflow streamlined
- **No verification gates**: Writers make creative decisions, system provides tools not approval
- **Language focus**: AI language detection is core differentiator

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Fork GSD architecture | Proven multi-step workflow system, agent spawning, state management | — Pending |
| Remove verification checkpoints | Creative work is subjective, checkpoints create friction | — Pending |
| Add AI language hooks | Core value proposition, differentiates from simple prompting | — Pending |
| 3-phase workflow for v1 | Concept → Outline → Draft is minimum viable for story development | — Pending |

---
*Last updated: 2026-02-27 after initialization*
