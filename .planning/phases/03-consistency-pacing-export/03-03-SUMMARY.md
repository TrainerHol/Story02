# Plan 03-03: Manuscript Export System - SUMMARY

**Completed:** 2026-02-27
**Duration:** ~22 minutes
**Result:** Success - All requirements met

## What Was Built

Implemented comprehensive manuscript export system with multiple modes and formats for submission-ready manuscript generation:

1. **Three export modes (OUT-01, OUT-02)**
   - **Single chapter:** Export one specific chapter as standalone file
   - **Range:** Export chapter range (e.g., chapters 3-8 for beta readers)
   - **Full manuscript:** Compile all chapters into complete manuscript

2. **Three output formats (OUT-04)**
   - **Markdown (.md):** Preserves markdown formatting for web publishing, conversion to EPUB/PDF
   - **Plain text (.txt):** Clean, readable text stripped of all formatting - maximum compatibility
   - **Standard manuscript (.txt):** Industry submission format with:
     - Running headers: `{LAST NAME} / {TITLE} / {PAGE}`
     - Page breaks between chapters
     - Scene breaks as `#` centered
     - Proper spacing (double-spaced simulation)
     - No special formatting (industry requirement)

3. **Professional title page generation (OUT-03)**
   - Industry-standard layout:
     - Word count upper right
     - Genre below word count
     - Title centered ~1/3 down page (ALL CAPS)
     - By-line centered
     - Author name centered
     - Contact info lower left (email, phone, address - all optional)
   - No header or page number on title page
   - Format-specific rendering (markdown heading syntax vs plain text spacing)

4. **Chapter compilation with proper formatting**
   - Sequential chapter reading and ordering
   - Chapter heading insertion (format-appropriate)
   - Scene break conversion:
     - Markdown: `---` (horizontal rule)
     - Plain text: `* * *` centered
     - Manuscript: `#` centered
   - Paragraph structure preservation
   - Frontmatter stripping (YAML not included in export)

5. **Export file management**
   - Output to `exports/` directory
   - Timestamp-based filenames prevent overwriting
   - Version tracking: `{slug}-{mode}-{YYYY-MM-DD-HHMM}.{ext}`
   - Word count calculation and display

## Key Files Created

### .claude/skills/write/export.md (1,072 lines)
Complete `/write:export` workflow command with:
- Prerequisites validation
- 8-step workflow:
  1. Prompt for export parameters (mode, format, title page)
  2. Load story metadata (PROJECT.md, chapter files)
  3. Generate title page with variable replacement
  4. Compile chapters in sequence
  5. Apply format-specific formatting
  6. Calculate final word count
  7. Write export file with timestamp
  8. Confirm export and provide next steps
- Detailed format specifications for all 3 formats
- Scene break handling per format
- Page structure and headers for manuscript format
- 3 complete examples (single chapter markdown, full text with title page, standard manuscript)
- FAQ section with 20+ questions

**Export examples:**
- Single chapter: `shadow-apprentice-chapter-5-2026-02-27-1430.md`
- Range: `shadow-apprentice-chapters-3-8-2026-02-27-1430.txt`
- Full manuscript: `shadow-apprentice-manuscript-2026-02-27-1430.txt`

**Format conversion examples:**
- Markdown: `# Chapter 1` → Plain text: `Chapter 1`
- Markdown: `**bold**` → Plain text: `bold` (stripped)
- Scene break `---` → `* * *` (text) or `#` (manuscript)

### .planning/templates/manuscript-title-page.md (400+ lines)
Professional title page template with:
- Industry-standard layout specification
- Variable placeholders: `{word_count}`, `{genre}`, `{TITLE}`, `{AUTHOR}`, contact fields
- Usage notes section:
  - Layout specifications (positioning, spacing)
  - Variable replacement table
  - Format variations (markdown/text/manuscript)
- Alternative formats section:
  - Minimal title page for beta readers
  - Conference partial submission format
  - Anonymous contest submission format
- Customization instructions
- Industry standards reference
- 3 complete examples with different contact info levels

**Title page example (manuscript format):**
```
                                                                    85,000 words
                                                                    Science Fiction




                    ECHOES OF THE VOID

                        by

                      Marcus Chen





Contact:
marcus.chen@email.com
(555) 987-6543
456 Oak Avenue, Seattle, WA 98101
```

### .claude/skills/write/SKILL.md (updated)
- Added `/write:export` command entry with modes, formats, features
- Updated skill description to include "manuscript export and formatting"
- Added complete workflow line: "Initialize → Plan → Style seed → Write chapters → Detect AI patterns → Check consistency → Get pacing guidance → Export finished manuscript"

## Technical Approach

**Export mode handling:**
```
if mode == "single":
    read chapters/chapter-{N}.md
else if mode == "range":
    read chapters/chapter-{start} through chapter-{end}
else if mode == "full":
    glob chapters/chapter-*.md, sort numerically
```

**Format-specific processing:**
- Markdown: Preserve syntax, use H1 for headings, keep `---` scene breaks
- Plain text: Strip all markdown (`#`, `**`, `*`, links), convert to plain text
- Manuscript: Plain text + industry conventions (headers, page breaks, `#` scene breaks)

**Title page generation:**
1. Load template
2. Replace variables with actual values
3. Uppercase transformation for TITLE and author last name
4. Optional contact fields (omit if not provided)
5. Format-specific rendering (spacing/headings)

**Chapter compilation:**
- Read each chapter file
- Parse frontmatter (chapter number, title, word count)
- Extract prose content (between frontmatter and ## Notes)
- Strip frontmatter from export
- Add chapter heading (format-appropriate)
- Convert scene breaks per format
- Concatenate in numeric order

**Filename generation:**
```
{story-slug}-{mode-indicator}-{timestamp}.{ext}
mode-indicator:
  - chapter-{N} (single)
  - chapters-{start}-{end} (range)
  - manuscript or full-manuscript (full)
timestamp: YYYY-MM-DD-HHMM
ext: .md or .txt
```

## Deviations from Plan

None. All tasks completed as specified:
- ✓ Task 1: export.md workflow created (200+ lines, actual: 1,072)
- ✓ Task 2: manuscript-title-page.md template created (30+ lines, actual: 400+)
- ✓ Task 3: SKILL.md updated with /write:export entry and workflow

## Verification

**Requirements coverage:**
- OUT-01: Export individual chapters as markdown ✓
- OUT-02: Compile full manuscript from all chapters ✓
- OUT-03: Standard manuscript format (title page, headers, formatting) ✓
- OUT-04: Export to .txt for submission platforms ✓

**Must-haves validation:**
- Writer can export individual chapters ✓
- Writer can compile full manuscript ✓
- Manuscripts include professional title pages ✓
- Manuscripts follow standard format (headers, spacing) ✓
- Writer can export to plain text .txt ✓

**Artifact checks:**
- export.md: 1,072 lines (exceeds 200 min) ✓
- manuscript-title-page.md: 400+ lines (exceeds 30 min) ✓
- SKILL.md exports export command ✓
- Key links documented ✓

## Impact

Writers can now:
- Export single chapters for critique groups or isolated review
- Compile chapter ranges for beta readers (send chapters 1-5, then 6-10 later)
- Generate full manuscripts ready for agent/publisher submission
- Produce industry-standard manuscript format with proper headers and spacing
- Create plain text versions for submission platforms (Submittable, etc.)
- Preserve markdown versions for web publishing or EPUB conversion
- Include professional title pages with contact information
- Version exports with timestamps (re-export after edits without overwriting)

**Workflow integration:**
Complete writing pipeline now available:
1. Initialize project (`/write:init`)
2. Expand or plan story content
3. Seed writing style (`/write:style`)
4. Write chapters (`/write:chapter`)
5. Detect AI patterns (`/write:detect`)
6. Check consistency (`/write:check`)
7. Get pacing guidance (`/write:pacing`)
8. **Export manuscript (`/write:export`)** ← Final step

**Submission-ready outputs:**
- Standard manuscript .txt: Ready for traditional publishing submissions
- Plain text .txt: Ready for online submission platforms
- Markdown .md: Ready for self-publishing conversion pipelines

**Use case examples:**
- Agent submission: Full manuscript, standard format, title page with contact
- Contest submission: Full manuscript, anonymous (no author), plain text
- Beta readers: Chapter range, plain text or markdown, minimal title page
- Self-publishing: Full manuscript, markdown, convert to EPUB/PDF
- Critique group: Single chapter, markdown, no title page

## Commits

```
e05d065 feat(03-03): implement manuscript export system
- Created /write:export workflow with 3 export modes
- Single chapter, range, and full manuscript compilation
- 3 format options: markdown, plain text, standard manuscript
- Professional title page generation with industry formatting
- Scene break conversion per format
- Running headers and page structure for manuscript format
- Timestamp-based versioning
- Updated write skill with /write:export and complete workflow
```

**Files modified:** 2 created, 1 updated
**Lines added:** 1,472+
**Lines removed:** 0

## Self-Check

- [x] All requirements implemented
- [x] All must-haves deliverable
- [x] All artifacts meet minimum line requirements
- [x] Workflow documented with 3 complete examples
- [x] FAQ section with 20+ questions
- [x] All 3 formats specified and documented
- [x] Title page template with industry standards
- [x] Complete workflow integrated in SKILL.md
- [x] Committed to git with proper message format
- [x] No blockers or issues

**Status:** PASSED ✓
