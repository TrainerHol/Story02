# /write:export - Manuscript Export

Export individual chapters or compile full manuscript in submission-ready formats. Supports markdown, plain text, and standard manuscript format with professional title pages.

## Overview

**What it does:**
- Exports individual chapters or compiles full manuscript from all chapters
- Supports 3 formats:
  1. **Markdown (.md):** Preserves markdown formatting for web publishing or conversion
  2. **Plain text (.txt):** Clean, readable text suitable for any platform
  3. **Standard manuscript (.txt):** Industry submission format with headers, spacing, and conventions
- Generates professional title pages with author info and contact details
- Applies proper formatting: headers, scene breaks, spacing, page structure
- Outputs to `exports/` directory with automatic timestamping
- **Execution time:** 5-15 minutes depending on manuscript length

## Prerequisites

Before exporting:
- Valid story project must exist
- At least 1 chapter written (`chapters/chapter-*.md` files exist)
- PROJECT.md exists for story metadata (title, genre, author)

If no chapters found, export will exit with guidance to write chapters first.

## Workflow

### Step 1: Prompt for export parameters

Ask writer for export configuration:

**1. Export mode:**
- **single:** Export one specific chapter
- **range:** Export chapter range (e.g., chapters 5-10)
- **full:** Export complete manuscript (all chapters)

**2. Format:**
- **markdown:** Preserve markdown formatting (.md file)
- **text:** Clean plain text (.txt file)
- **manuscript:** Standard manuscript format (.txt with industry conventions)

**3. Include title page:**
- Yes (for full/range exports)
- No (optional)

**Mode-specific prompts:**
- If `single`: Ask for chapter number to export
- If `range`: Ask for start and end chapter numbers (e.g., "3" and "8" for chapters 3-8)
- If `full`: Automatically detect and use all chapter files

### Step 2: Load story metadata (OUT-01, OUT-02)

Read PROJECT.md and extract metadata:

**From PROJECT.md:**
- **Story title:** Extract from heading `# {STORY_TITLE}` (line 1)
- **Genre:** Extract from Metadata section
- **Current word count:** For reference (or calculate from chapters)
- **Author name:** If present in PROJECT.md, use it; otherwise prompt writer

**Prompt for title page information (if title page requested):**
- Author name (if not in PROJECT.md)
- Email address (optional)
- Phone number (optional)
- Mailing address (optional)

Note: Contact information is optional. Writer can decline any/all fields.

**Read chapter files in correct sequence:**

Determine which chapters to read based on mode:
- **Single:** Read `chapters/chapter-{N}.md` (e.g., chapter-05.md)
- **Range:** Read `chapters/chapter-{start}.md` through `chapters/chapter-{end}.md`
- **Full:** Glob all `chapters/chapter-*.md` files and sort numerically

For each chapter file:
1. **Read file content**
2. **Parse frontmatter** (YAML between `---` markers):
   - `chapter: {number}`
   - `title: {optional chapter title}`
   - `word_count: {number}`
   - `pov: {character}` (optional)
3. **Extract prose content:**
   - Everything between frontmatter close (`---`) and `## Notes` section
   - Preserve scene breaks (marked with `---`)
   - Preserve paragraph structure
4. **Strip chapter metadata frontmatter** from exported content (don't include YAML in final export)

**Calculate total word count:**
Sum word counts from chapter frontmatter, or count words in extracted prose content.

### Step 3: Generate title page (OUT-03)

If title page requested, use `.planning/templates/manuscript-title-page.md` template:

**Template variable replacement:**

Replace placeholders with actual values:
- `{word_count}`: Total word count of exported content
- `{genre}`: Genre from PROJECT.md
- `{TITLE}`: Story title in ALL CAPS (uppercase transformation)
- `{AUTHOR}`: Author name from prompt or PROJECT.md
- `{author_email}`: Email if provided, otherwise omit line
- `{author_phone}`: Phone if provided, otherwise omit line
- `{author_address}`: Address if provided, otherwise omit line

**Format-specific rendering:**

**For markdown format:**
- Use markdown heading syntax (`#` for title)
- Preserve template spacing (blank lines for positioning)
- Keep centered-looking layout using whitespace

**For text format:**
- Plain text with spacing preserved using blank lines
- Approximate center-alignment using leading spaces
- Calculate centering based on typical 80-character line width

**For standard manuscript format:**
- Plain text with exact industry spacing:
  - Word count upper right (60+ spaces from left margin)
  - Title centered ~1/3 down page (12-15 blank lines from top)
  - "by" line centered
  - Author name centered
  - Contact info lower left (leave 8-12 blank lines from author to contact)
- No header or page number on title page

Example title page (manuscript format):
```
                                                                    5,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Author





Contact:
jane@email.com
(555) 123-4567
123 Main St, City, ST 12345
```

### Step 4: Compile chapters

Concatenate chapters in numeric order with proper formatting:

**For single chapter export:**
- Export only the requested chapter's prose content
- Include chapter heading at top
- No additional compilation needed

**For range/full export:**
- Combine chapters sequentially in numeric order
- Add chapter separators between each chapter

**Chapter headings (between chapters):**

Format varies by export format:

**Markdown format:**
```markdown
# Chapter 1: The Beginning

{prose content}

# Chapter 2: Discovery

{prose content}
```
- Use H1 heading (`#`)
- Include chapter title if present in frontmatter
- If no title: `# Chapter {N}`

**Plain text format:**
```
Chapter 1: The Beginning

{prose content}


Chapter 2: Discovery

{prose content}
```
- Plain text heading
- Include chapter title if present
- Blank lines for separation (2 before chapter heading, 1 after)

**Standard manuscript format:**
```
AUTHOR / TITLE / 1

Chapter 1: The Beginning

{prose content}

[page break indicated by form feed character or multiple blank lines]

AUTHOR / TITLE / 5

Chapter 2: Discovery

{prose content}
```
- New page for each chapter (form feed `\f` or 3-4 blank lines to simulate page break)
- Running header on each page: `{LAST NAME} / {STORY TITLE (shortened if long)} / {PAGE #}`
- Headers use UPPERCASE for last name and title
- Page numbers increment across entire manuscript

**Scene breaks within chapters:**

Chapters may have internal scene breaks marked by `---` in the source. Convert appropriately:

**Markdown format:**
- Preserve `---` (renders as horizontal rule in markdown)

**Plain text format:**
- Convert to `* * *` centered (standard scene break symbol)
- Blank line before and after

**Standard manuscript format:**
- Use single `#` centered (industry standard scene break marker)
- Blank line before and after

Example:
```
Sarah opened the door, her heart pounding.

#

Three hours later, Marcus arrived at the tower.
```

### Step 5: Apply format-specific formatting (OUT-04)

Each export format has specific conventions:

#### Markdown Format (.md)

**Characteristics:**
- Preserve all markdown syntax (headings, bold, italic, links)
- Keep chapter headings as H1 (`#`)
- Preserve scene breaks as `---`
- Maintain paragraph structure (double newline between paragraphs)
- Suitable for: Web publishing, static site generators, markdown editors, conversion to HTML/EPUB

**Output filename:** `exports/{story-slug}-{mode}-{timestamp}.md`

Example: `exports/shadow-apprentice-full-manuscript-2026-02-27-1430.md`

**Structure:**
```markdown
{Title page in markdown if requested}

# Chapter 1

Prose content with **bold** and *italic* preserved.

---

More content after scene break.

# Chapter 2

{continues...}
```

#### Plain Text Format (.txt)

**Characteristics:**
- Strip ALL markdown syntax (no `#`, `**`, `*`, `[]()`, etc.)
- Convert headings to plain text
- Scene breaks become `* * *`
- Preserve paragraph breaks (double newline)
- Clean, readable text suitable for any text editor or platform
- Suitable for: Email, plain text editors, copy-paste, maximum compatibility

**Output filename:** `exports/{story-slug}-{mode}-{timestamp}.txt`

**Conversion rules:**
- `# Heading` → `Heading` (just remove `#` markers)
- `**bold**` → `bold` (remove asterisks)
- `*italic*` → `italic` (remove asterisks)
- `[link text](url)` → `link text` (remove markdown link syntax)
- `---` scene break → `* * *` (centered if possible)

**Structure:**
```
{Title page in plain text if requested}

Chapter 1

Prose content with formatting stripped.

* * *

More content after scene break.

Chapter 2

{continues...}
```

#### Standard Manuscript Format (.txt)

Industry-standard formatting for submissions to agents, publishers, contests.

**Characteristics:**
- Plain text file (.txt) with specific conventions:
  - **Simulated 12pt monospace:** Plain text (no actual font control in .txt)
  - **Double-spaced:** Blank line between paragraphs
  - **1-inch margins:** Approximate with 65-70 characters per line
  - **Running headers:** `{LAST NAME} / {TITLE} / {PAGE}` on each page
  - **Page breaks:** Between chapters (form feed `\f` or 3-4 blank lines)
  - **Scene breaks:** Single `#` centered
  - **No special formatting:** No bold, italic, or other formatting
  - **First line NOT indented:** Submission standard (some editors indent, but modern standard is block paragraphs)

**Output filename:** `exports/{story-slug}-manuscript-{timestamp}.txt`

**Page header format:**
```
MARTINEZ / SHADOW'S APPRENTICE / 5
```
- Last name in UPPERCASE
- Story title in UPPERCASE (shorten if > 30 chars to fit line)
- Page number
- Separated by ` / ` (space-slash-space)

**Page structure:**
```
MARTINEZ / SHADOW'S APPRENTICE / 1

Chapter 1: The Beginning

Sarah opened the door, her heart pounding. The hallway stretched before her, dark and silent. She took a breath and stepped inside.

"Hello?" she called. No answer.

#

Three hours later, Marcus arrived at the tower. He found the door ajar and Sarah's bag on the floor.

[3-4 blank lines simulating page break]

MARTINEZ / SHADOW'S APPRENTICE / 2

Chapter 2: Discovery

Marcus knelt beside the bag, examining its contents. Sarah's journal lay open to the last entry.

{continues...}
```

**Page numbering:**
- Start at 1 for first page of content (title page has no header)
- Increment continuously across entire manuscript
- Include in running header on every page except title page

**Line wrapping:**
- Wrap lines at ~65-70 characters for readability
- Or leave long lines (text editors will wrap)

Suitable for: Agent/publisher submissions, contests, industry-standard formatting

### Step 6: Calculate final word count

Count words in exported prose content:

**Word counting rules:**
- Split content on whitespace (spaces, tabs, newlines)
- Exclude frontmatter YAML (already stripped)
- Exclude markdown symbols in plain text exports
- Exclude headers and page numbers in manuscript format
- Count only actual prose words

Display total to writer at completion.

### Step 7: Write export file

Create exports directory if it doesn't exist:

```bash
mkdir -p stories/{project-slug}/exports
```

**Generate filename:**

Pattern: `{story-slug}-{mode-indicator}-{timestamp}.{ext}`

**Mode indicators:**
- Single chapter: `chapter-{N}` (e.g., `chapter-05`)
- Range: `chapters-{start}-{end}` (e.g., `chapters-3-8`)
- Full manuscript: `full-manuscript` or just `manuscript` for manuscript format

**Extension:**
- Markdown: `.md`
- Plain text: `.txt`
- Manuscript: `.txt`

**Timestamp format:** `YYYY-MM-DD-HHMM` for version tracking

**Examples:**
- `shadow-apprentice-chapter-05-2026-02-27-1430.md`
- `shadow-apprentice-chapters-3-8-2026-02-27-1430.txt`
- `shadow-apprentice-manuscript-2026-02-27-1430.txt`
- `shadow-apprentice-full-manuscript-2026-02-27-1515.md`

Timestamps prevent overwriting previous exports. Writer can re-export after edits and keep version history.

### Step 8: Confirm export and provide next steps

Display completion message to writer:

```
═══════════════════════════════════════════════════════
        EXPORT COMPLETE
═══════════════════════════════════════════════════════

File: exports/{filename}
Format: {Markdown | Plain Text | Standard Manuscript}
Chapters: {count or range}
Total word count: {number} words
Includes title page: {Yes | No}

───────────────────────────────────────────────────────
NEXT STEPS
───────────────────────────────────────────────────────

1. Review the exported file in your preferred text editor
2. Run spell check and grammar check
3. For submissions:
   - Standard manuscript format ready for agent/publisher submission
   - Plain text suitable for submission platforms (Submittable, etc.)
4. For beta readers:
   - Plain text or markdown for easy sharing
5. For publication:
   - Markdown can be converted to HTML, EPUB, or PDF
   - Import plain text into Word/Google Docs for formatting

═══════════════════════════════════════════════════════
```

## Examples

### Example 1: Single Chapter Markdown Export

**User inputs:**
- Mode: single
- Chapter: 5
- Format: markdown
- Title page: No

**Process:**
1. Read `chapters/chapter-05.md`
2. Extract frontmatter: chapter 5, title "The Revelation"
3. Extract prose (2,800 words)
4. Generate markdown with heading:
   ```markdown
   # Chapter 5: The Revelation

   {prose content with markdown preserved}
   ```
5. Write to `exports/shadow-apprentice-chapter-5-2026-02-27-1430.md`

**Output preview:**
```markdown
# Chapter 5: The Revelation

Sarah stared at the ancient tome, her hands trembling. The symbols **glowed** faintly in the candlelight, revealing a truth she'd never imagined.

"This changes everything," she whispered.

---

Marcus burst through the door. "Sarah, we need to leave. *Now.*"

{prose continues...}
```

### Example 2: Full Manuscript Plain Text Export

**User inputs:**
- Mode: full
- Format: text
- Title page: Yes
- Author: Jane Martinez
- Email: jane@email.com
- Phone/Address: (declined)

**Process:**
1. Read all 10 chapter files
2. Extract prose from each (total 25,000 words)
3. Generate plain text title page:
   ```
                                                                    25,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





   Contact:
   jane@email.com
   ```
4. Compile chapters with text headings and `* * *` scene breaks
5. Write to `exports/shadow-apprentice-full-manuscript-2026-02-27-1430.txt`

**Output preview:**
```
                                                                    25,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





Contact:
jane@email.com


Chapter 1: The Beginning

Sarah opened the door, her heart pounding. The hallway stretched before her, dark and silent.

* * *

Three hours later, Marcus arrived.

{continues through all 10 chapters...}
```

### Example 3: Standard Manuscript Format for Submission

**User inputs:**
- Mode: full
- Format: manuscript
- Title page: Yes
- Author: Jane Martinez
- Email: jane@email.com
- Phone: (555) 123-4567
- Address: 123 Main St, Portland, OR 97201

**Process:**
1. Read all chapters (25,000 words)
2. Generate manuscript title page with full contact info
3. Compile chapters with:
   - Running headers: `MARTINEZ / SHADOW'S APPRENTICE / {PAGE}`
   - Page breaks between chapters
   - Scene breaks as `#`
   - Page numbers incrementing from 1
4. Write to `exports/shadow-apprentice-manuscript-2026-02-27-1430.txt`

**Output preview:**
```
                                                                    25,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





Contact:
jane@email.com
(555) 123-4567
123 Main St, Portland, OR 97201


[page break]

MARTINEZ / SHADOW'S APPRENTICE / 1

Chapter 1: The Beginning

Sarah opened the door, her heart pounding. The hallway stretched before her, dark and silent.

#

Three hours later, Marcus arrived.

[page continues...]

[page break]

MARTINEZ / SHADOW'S APPRENTICE / 5

Chapter 2: Discovery

Marcus knelt beside the bag, examining its contents.

{continues with proper headers on each page...}
```

## FAQ

**Q: What's the difference between text and manuscript format?**
A: Plain text is clean, readable text stripped of all formatting. Manuscript format follows industry submission standards with running headers, page numbers, specific spacing, and scene break conventions. Use manuscript format for agent/publisher submissions. Use plain text for maximum compatibility or when pasting into another system.

**Q: Can I export to Word (.docx) or PDF?**
A: Not directly. Export to `.txt` (plain text or manuscript), then import into Word or Google Docs. From there, apply fonts and formatting, then export to PDF. Future versions may support direct Word/PDF export.

**Q: What if some chapter numbers are missing?**
A: The export will skip missing chapters and warn you. For example, if you have chapters 1, 2, 4, 5 (no chapter 3), the export will include 1, 2, 4, 5 and note that chapter 3 was missing.

**Q: Can I re-export after making edits?**
A: Yes! Timestamps prevent overwriting. You can export multiple times and compare versions. Example: `shadow-apprentice-manuscript-2026-02-27-1430.txt` and `shadow-apprentice-manuscript-2026-02-27-1600.txt` after edits.

**Q: Should I include a title page for beta readers?**
A: Optional. Title pages are mainly for formal submissions. For beta readers, you might include a simplified title page with just title and author, or skip it entirely and jump straight to chapter 1.

**Q: What about prologue and epilogue?**
A: Name them as `chapter-00.md` (prologue) and the final chapter number + 1 for epilogue (e.g., if 20 chapters, epilogue is `chapter-21.md`). The export will include them in sequence. Or name them `prologue.md` and `epilogue.md` and export separately if you prefer.

**Q: Can I customize the title page template?**
A: Yes. Copy `.planning/templates/manuscript-title-page.md` to your story directory and modify it. The export workflow will check for a local template first before using the global one.

**Q: How are scene breaks handled in different formats?**
A:
- Markdown: `---` (horizontal rule)
- Plain text: `* * *` centered
- Manuscript: `#` centered (industry standard)

**Q: What if my manuscript is very long (100k+ words)?**
A: Export will work fine. Large text files (1-2 MB for 100k-200k words) open in any text editor. For Word import, consider breaking into parts if Word becomes sluggish.

**Q: Can I export a chapter range for beta readers?**
A: Yes! Use range mode. For example, export chapters 1-5 for an early beta reader, then export 6-10 later. Great for chapter-by-chapter feedback.

**Q: How do I know which format to use?**
A:
- **Manuscript format:** Agent/publisher submissions, contests
- **Plain text:** Submission platforms (Submittable), email, maximum compatibility
- **Markdown:** Web publishing, blog posts, static sites, further conversion to EPUB/PDF

**Q: What about poetry or non-prose formatting?**
A: Current version optimized for prose narrative. Poetry, lyrics, or special formatting may not export perfectly. For poetry, markdown format is recommended to preserve line breaks and stanza structure.

**Q: Can I export just one scene instead of a full chapter?**
A: Not automatically. Workaround: Copy the scene to a temporary `chapter-temp.md` file, export that chapter, then delete the temp file.

**Q: Will italics be preserved?**
A:
- Markdown: Yes, `*italic*` preserved
- Plain text: No, markdown syntax stripped, just plain text
- Manuscript: No, industry standard prohibits special formatting in .txt submissions

**Q: What about dialogue formatting?**
A: Dialogue formatting (paragraph structure, quote marks) is preserved in all formats. Just the markdown enhancement symbols are stripped in plain text/manuscript formats.

**Q: How often should I export?**
A:
- After each draft completion (full manuscript)
- When sending to beta readers (range or full)
- Before major revisions (backup version)
- When ready to submit (manuscript format)

**Q: Can I change the export directory?**
A: Not currently. All exports go to `stories/{project}/exports/`. You can move them afterward.

**Q: What's the maximum manuscript size for export?**
A: No hard limit. The system has successfully exported 200k+ word manuscripts. Very large files (500k+ words) may take a few extra seconds to process.
