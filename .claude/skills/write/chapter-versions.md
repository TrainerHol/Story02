# Chapter Version Control Workflow

Automatic revision tracking with version history, rollback capability, and diff comparison for safe chapter experimentation.

## Overview

Chapter version control gives you the freedom to experiment with revisions knowing you can always restore a previous version. Every time a chapter is updated, the current version is automatically saved as a revision with timestamp and metadata. You can view revision history, compare versions, and restore any previous draft.

**Storage Location:** `.writing/chapters/{chapter-slug}/revisions/`
**Format:** Timestamped revision files with metadata index
**When to use:** Automatically during chapter updates; manually to view/restore versions
**Safety:** No chapter content is ever lost—every version is preserved

## Revision Storage Structure

### Directory Layout

```
.writing/chapters/
├── chapter-1/
│   ├── current.md                    # Latest version (or use chapters/chapter-1.md in project root)
│   └── revisions/
│       ├── index.json                # Revision metadata
│       ├── v01-2026-02-27T10-30-00Z.md
│       ├── v02-2026-02-27T14-15-00Z.md
│       └── v03-2026-02-28T09-45-00Z.md
├── chapter-2/
│   ├── current.md
│   └── revisions/
│       ├── index.json
│       └── v01-2026-02-28T11-20-00Z.md
...
```

**File Naming:**
- **Current version:** `chapters/chapter-{N}.md` (in project root) OR `.writing/chapters/chapter-{N}/current.md`
- **Revisions:** `.writing/chapters/chapter-{N}/revisions/v{NN}-{timestamp}.md`
  - Version number: Two-digit, zero-padded (v01, v02, v03...)
  - Timestamp: ISO 8601 format with colons replaced by hyphens for filesystem compatibility
  - Example: `v03-2026-02-28T14-30-45Z.md`

### Revision Metadata (index.json)

Each chapter has a metadata file tracking all revisions.

**Format:**

```json
{
  "chapter": "chapter-1",
  "chapter_number": 1,
  "title": "The Beginning",
  "slug": "chapter-1",
  "revisions": [
    {
      "version": 1,
      "timestamp": "2026-02-27T10:30:00Z",
      "word_count": 2340,
      "note": "Initial draft",
      "file": "v01-2026-02-27T10-30-00Z.md"
    },
    {
      "version": 2,
      "timestamp": "2026-02-27T14:15:00Z",
      "word_count": 2450,
      "note": "Added opening scene detail",
      "file": "v02-2026-02-27T14-15-00Z.md",
      "changes": "+110 words, enhanced opening"
    },
    {
      "version": 3,
      "timestamp": "2026-02-28T09:45:00Z",
      "word_count": 2380,
      "note": "Tightened dialogue in scene 2",
      "file": "v03-2026-02-28T09-45-00Z.md",
      "changes": "-70 words, dialogue revision"
    }
  ],
  "current_version": 3,
  "created": "2026-02-27T10:30:00Z",
  "last_updated": "2026-02-28T09:45:00Z"
}
```

**Fields:**
- `chapter`: Chapter identifier (slug)
- `chapter_number`: Numeric chapter number
- `title`: Chapter title (optional, from frontmatter)
- `slug`: Chapter slug for file paths
- `revisions[]`: Array of revision metadata
  - `version`: Sequential version number (1, 2, 3...)
  - `timestamp`: When this revision was created (ISO 8601)
  - `word_count`: Word count for this version
  - `note`: User-provided description of changes (optional)
  - `file`: Revision filename
  - `changes`: Auto-generated summary (word count delta, brief description)
- `current_version`: Version number of current draft
- `created`: Timestamp of first draft
- `last_updated`: Timestamp of most recent revision

## Automatic Revision Saving

Revisions are saved automatically whenever a chapter is updated. No manual intervention required.

### Trigger Events

Save revision before:
1. **Chapter regeneration** (via `/write:chapter` for existing chapter)
2. **Manual overwrite** (if user edits chapter file directly and saves with workflow)
3. **Restoration** (when restoring previous version, current version becomes new revision)

### Save Process

When chapter is about to be updated:

1. **Check if chapter exists**
   - Look for `chapters/chapter-{N}.md` or `.writing/chapters/chapter-{N}/current.md`
   - If not exists: This is initial draft, no revision needed (but will be v01 in index)
   - If exists: Current version needs to be saved

2. **Create revisions directory**
   - Ensure `.writing/chapters/chapter-{N}/revisions/` exists
   - Create if missing
   - Create `index.json` if this is first revision

3. **Calculate metadata**
   - Count words in current chapter (same method as chapter generation)
   - Generate timestamp (ISO 8601 format)
   - Determine next version number (read index.json, increment)

4. **Prompt for revision note** (optional)
   ```
   Saving current version as revision before updating Chapter {N}.

   Current version: {word_count} words

   Revision note (optional, press Enter to skip):
   > _
   ```

   User can:
   - Enter note: "Added dialogue", "Rewrote ending", "Tightened pacing"
   - Press Enter: Use auto-generated note like "Automatic save before regeneration"
   - Skip: Leave note empty

5. **Copy current version to revisions**
   - Copy `chapters/chapter-{N}.md` to `.writing/chapters/chapter-{N}/revisions/v{NN}-{timestamp}.md`
   - Preserve all content, frontmatter, formatting

6. **Update index.json**
   - Add new revision entry to `revisions[]` array
   - Set metadata: version, timestamp, word_count, note, file
   - Update `current_version` to new number (will be set after update completes)
   - Update `last_updated`

7. **Confirm save**
   ```
   ✓ Saved as revision v02 ({word_count} words)

   Proceeding with chapter update...
   ```

8. **After update completes: Update current_version**
   - After new chapter content written
   - Update `index.json` with final `current_version` number
   - If new content has different word count, store that separately

### Auto-Generated Change Summary

When saving revision, calculate automatic changes summary:

```javascript
const wordDelta = newWordCount - previousWordCount;
const changeType = determineChangeType(delta, note);

// Change types:
// "+{N} words" - content addition
// "-{N} words" - content reduction
// "~{N} words" - similar length, revision
// "+/-{N} words" - mixed changes

const changeSummary = `${wordDelta > 0 ? '+' : ''}${wordDelta} words, ${note || 'revision'}`;
```

Example summaries:
- `"+110 words, enhanced opening"`
- `"-70 words, dialogue revision"`
- `"~15 words, style tweaks"`
- `"+350 words, added scene"`

## Commands

### `/write:revisions <chapter-name>` - View Revision History

Display all saved versions of a chapter with timestamps, word counts, and notes.

**Usage:**
```
/write:revisions chapter-1
/write:revisions 1
/write:revisions "The Beginning"
```

Accepts: chapter number, chapter slug, or chapter title.

**Process:**

1. **Validate story project**
   - Check for PROJECT.md
   - Confirm in valid story project directory

2. **Look up chapter**
   - Parse chapter identifier (number, slug, or title)
   - Find matching chapter in `chapters/` or `.writing/chapters/`
   - If not found: "Chapter '{name}' not found. Available chapters: {list}"

3. **Load revision metadata**
   - Read `.writing/chapters/chapter-{N}/revisions/index.json`
   - If not exists: "No revisions for Chapter {N}. This chapter has not been revised yet."
   - Parse revisions array

4. **Display revision history**

   **Format:**
   ```
   ═══════════════════════════════════════
   Revisions for Chapter {N}: {Title}
   ═══════════════════════════════════════

   | Ver | Date       | Time  | Words | Change      | Note                          |
   |-----|------------|-------|-------|-------------|-------------------------------|
   | 3   | 2026-02-28 | 09:45 | 2380  | -70 words   | Tightened dialogue in scene 2 |
   | 2   | 2026-02-27 | 14:15 | 2450  | +110 words  | Added opening scene detail    |
   | 1   | 2026-02-27 | 10:30 | 2340  | Initial     | Initial draft                 |

   Current: Version 3 (2380 words)
   Created: 2026-02-27 | Last updated: 2026-02-28

   ─────────────────────────────────────────
   Actions:
   - Restore version: /write:restore chapter-1 <version>
   - Compare versions: /write:diff chapter-1 <v1> <v2>
   - View specific version: /write:restore chapter-1 <version> --preview
   ```

   **Table Notes:**
   - Versions listed newest first (reverse chronological)
   - Date and time split for readability
   - Change column shows word count delta
   - Note column shows user-provided or auto-generated description
   - Current version highlighted or marked

5. **Offer actions**
   - View specific version
   - Restore previous version
   - Compare two versions
   - Return to current

**Output Variations:**

**Single revision (chapter never updated):**
```
Revisions for Chapter 1: The Beginning

| Ver | Date       | Time  | Words | Note          |
|-----|------------|-------|-------|---------------|
| 1   | 2026-02-27 | 10:30 | 2340  | Initial draft |

Current: Version 1 (2340 words)
No revisions yet—this is the original draft.
```

**Many revisions:**
```
Revisions for Chapter 5: The Confrontation

Showing 10 most recent revisions (15 total):

| Ver | Date       | Time  | Words | Change     | Note                    |
|-----|------------|-------|-------|------------|-------------------------|
| 15  | 2026-03-02 | 16:20 | 3100  | +50 words  | Final polish            |
| 14  | 2026-03-02 | 14:00 | 3050  | -120 words | Cut redundant dialogue  |
| 13  | 2026-03-01 | 11:30 | 3170  | +200 words | Expanded climax         |
...

View all revisions: /write:revisions chapter-5 --all
```

**Duration:** < 1 minute (instant lookup and display)

### `/write:restore <chapter-name> <version-number>` - Restore Previous Version

Roll back a chapter to a previous version. Current version is saved as new revision before restoring.

**Usage:**
```
/write:restore chapter-1 2
/write:restore 1 v02
/write:restore "The Beginning" 2
```

**Process:**

1. **Validate inputs**
   - Parse chapter identifier
   - Parse version number (accept "2" or "v02" or "v2")
   - Check chapter exists
   - Check version exists in revisions

2. **Load specified revision**
   - Read `.writing/chapters/chapter-{N}/revisions/v{NN}-{timestamp}.md`
   - Load full content

3. **Display preview**
   ```
   ═══════════════════════════════════════
   Restore Chapter {N} to Version {V}?
   ═══════════════════════════════════════

   Version {V} details:
   - Date: {date} at {time}
   - Word count: {count}
   - Note: {note}

   Preview (first 500 characters):

   {excerpt...}

   ─────────────────────────────────────────
   Current version will be saved as revision v{current+1} before restoring.
   No data will be lost.

   Restore this version? (yes/no):
   > _
   ```

4. **If user confirms:**

   **Save current version as new revision:**
   - Run automatic revision save process
   - Create new revision entry with note: "Saved before restoring to v{N}"
   - Increment version number

   **Restore specified version:**
   - Copy revision file content to current chapter location
   - Update `chapters/chapter-{N}.md` (or `.writing/chapters/chapter-{N}/current.md`)
   - Preserve frontmatter if needed

   **Update index.json:**
   - Update `current_version` to restored version number (NO—actually increment version)
   - Actually: Restoring creates a NEW version that is a copy of old content
   - So if restoring v02 and current is v05, the new version becomes v06 with v02's content
   - This preserves true history (all changes are forward in time)

   **Update metadata:**
   - Update chapter frontmatter `revised:` timestamp
   - Update PROJECT.md `current_word_count` if changed

5. **Display confirmation**
   ```
   ✓ Chapter {N} restored to version {V}

   Previous current version saved as v{new_revision_number}

   New current version: v{new_number} ({word_count} words)
   Content from: v{restored_version} ({date})

   ─────────────────────────────────────────
   Next steps:
   - View revisions: /write:revisions chapter-{N}
   - Continue editing or regenerate chapter
   ```

**Options:**

`--preview` flag: View revision without restoring
```
/write:restore chapter-1 2 --preview
```

Shows full content of specified revision without making changes.

**Safety:**

- Current version ALWAYS saved before restore
- No revision is ever deleted
- Can restore from restore (if you restore v02, don't like it, can restore back to v05)
- Full revision history maintained

**Duration:** 1-2 minutes (including confirmation)

### `/write:diff <chapter-name> <version1> <version2>` - Compare Two Versions

View differences between two versions of a chapter. Shows word count changes and paragraph-level additions/deletions.

**Usage:**
```
/write:diff chapter-1 1 3
/write:diff 1 v02 v05
/write:diff "The Beginning" 1 current
```

Version identifiers: version number (1, 2, 3...), v-prefixed (v01, v02...), or "current"

**Process:**

1. **Validate inputs**
   - Parse chapter identifier
   - Parse both version identifiers
   - Check chapter exists
   - Check both versions exist
   - If "current" specified: load current chapter, get current_version from index.json

2. **Load both versions**
   - Read version 1 content from revisions file
   - Read version 2 content from revisions file (or current if specified)
   - Load metadata for both from index.json

3. **Calculate differences**

   **Word count comparison:**
   ```
   v1_count = word_count_for_version_1
   v2_count = word_count_for_version_2
   delta = v2_count - v1_count
   percent_change = (delta / v1_count) * 100
   ```

   **Paragraph-level comparison:**
   - Split both versions into paragraphs
   - Compare paragraph by paragraph
   - Identify:
     - **Added paragraphs:** Present in v2, not in v1
     - **Deleted paragraphs:** Present in v1, not in v2
     - **Modified paragraphs:** Different content between versions
     - **Unchanged paragraphs:** Identical in both versions

   **Scene-level changes:**
   - Identify scene breaks (typically `---` or `* * *`)
   - Note if scenes added, removed, or reordered

4. **Display comparison**

   **Format:**
   ```
   ═══════════════════════════════════════
   Comparing Chapter {N}: Version {V1} vs Version {V2}
   ═══════════════════════════════════════

   Version {V1}:
   - Date: {date} at {time}
   - Word count: {count}
   - Note: {note}

   Version {V2}:
   - Date: {date} at {time}
   - Word count: {count}
   - Note: {note}

   ─────────────────────────────────────────
   CHANGES SUMMARY

   Word Count: {v1_count} → {v2_count} ({delta >= 0 ? '+' : ''}{delta} words, {percent_change}%)

   Paragraphs:
   + {added_count} added
   - {deleted_count} removed
   ~ {modified_count} modified
   = {unchanged_count} unchanged

   ─────────────────────────────────────────
   DETAILED CHANGES

   + Added paragraph (after paragraph 2):
     "The morning mist clung to the valley, thick enough to taste.
     Sarah pulled her jacket tighter and stepped off the porch."

   + Added dialogue exchange (scene 3):
     "You knew her," Sarah said.
     Rivera didn't answer. That was answer enough.

   ~ Modified ending paragraph:
     Was: "She had to know the truth, whatever it cost."
     Now: "She would find the truth. No matter what it cost her."

   - Removed transitional sentence (scene 2):
     "She walked to the car and got in."

   ─────────────────────────────────────────
   Actions:
   - Restore v{V1}: /write:restore chapter-{N} {V1}
   - Restore v{V2}: /write:restore chapter-{N} {V2}
   - View full version: /write:restore chapter-{N} {V} --preview
   ```

**Comparison Modes:**

**Brief mode (default):**
- Shows summary statistics
- Shows major paragraph-level changes
- Excerpts only (first 100 chars of each change)

**Detailed mode:**
```
/write:diff chapter-1 1 3 --detailed
```
- Shows full text of all changes
- Includes unchanged sections for context
- More verbose, complete picture

**Statistics only:**
```
/write:diff chapter-1 1 3 --stats
```
- Just word counts and change counts
- No content excerpts
- Quick overview

**Output Variations:**

**No changes (versions identical):**
```
Comparing Chapter 1: Version 2 vs Version 3

No differences found.
These versions have identical content.
```

**Minor changes:**
```
CHANGES SUMMARY

Word Count: 2450 → 2455 (+5 words, +0.2%)

Paragraphs:
~ 1 modified (minor wording changes)
= 47 unchanged

DETAILED CHANGES

~ Modified paragraph 12:
  Changed "She knew it" to "She understood it now"
```

**Major revision:**
```
CHANGES SUMMARY

Word Count: 2340 → 3100 (+760 words, +32.5%)

Paragraphs:
+ 12 added
- 3 removed
~ 8 modified
= 25 unchanged

Scenes:
+ Added new scene (Scene 4: "The Basement")

DETAILED CHANGES

[... extensive change list ...]
```

**Duration:** 2-5 minutes depending on chapter length and change extent

## Integration with Chapter Writing

Version control integrates automatically with the `/write:chapter` workflow.

### Before Chapter Generation/Update

When user runs `/write:chapter` for existing chapter:

```
> /write:chapter
Chapter number: 5
Chapter 5 already exists (2450 words, last updated 2026-02-27).

Options:
1. Regenerate chapter (current version will be saved as revision)
2. Generate new chapter
3. Cancel

> 1

Saving current Chapter 5 as revision...

Revision note (optional):
> Saving before regeneration with new plot direction

✓ Saved as revision v03 (2450 words)

[Proceeds with chapter regeneration...]
```

**Auto-save logic:**
1. Detect existing chapter
2. Prompt for action (regenerate vs new chapter)
3. If regenerate: Save current as revision
4. Prompt for note (optional)
5. Save revision with metadata
6. Proceed with generation

### During Chapter Editing

If user manually edits chapter file and then runs workflow command:

```
> /write:chapter --update-tracking

Checking chapter status...

Chapter 3 has been modified outside workflow (frontmatter 'revised' is null, but content changed).

Save current version as revision before continuing? (yes/no):
> yes

Revision note:
> Manual edits to dialogue in scene 2

✓ Saved as revision v04
```

**Manual edit detection:**
- Compare frontmatter `revised:` timestamp with file modification time
- If file modified but `revised:` not updated: manual edit detected
- Offer to save as revision
- Update tracking

### After Chapter Generation

After new chapter content written:

```
Chapter 5 regenerated successfully (2680 words)

Version history:
- v01: Initial draft (2340 words)
- v02: Added scene detail (2450 words)
- v03: Saved before regeneration (2450 words)
- v04: Current version (2680 words) ← NEW

View revisions: /write:revisions 5
Compare with previous: /write:diff 5 v03 current
```

**Post-generation actions:**
- Display version history summary
- Show what changed (word count delta)
- Offer comparison commands

### Periodic Backup Reminder

After multiple chapter generations without revisions check:

```
[After 5 chapter updates]

💾 Revision History Status:

Recent chapters with multiple revisions:
- Chapter 3: 6 revisions
- Chapter 5: 4 revisions
- Chapter 7: 2 revisions

Consider reviewing revision history to identify patterns or restore preferred versions.

View all revisions: /write:revisions --all
```

**Helps user:**
- Track revision volume
- Identify heavily-revised chapters
- Remember to clean up or consolidate if needed

## Integration Workflow Summary

```mermaid
graph TD
    A[/write:chapter for existing chapter] --> B{Chapter exists?}
    B -->|No| C[Generate new chapter v01]
    B -->|Yes| D[Prompt: Regenerate or New?]
    D -->|Regenerate| E[Save current as revision]
    E --> F[Prompt for revision note]
    F --> G[Create revision file and update index.json]
    G --> H[Generate new chapter content]
    H --> I[Increment version, update current]
    D -->|New| C
    I --> J[Offer comparison/history actions]
    C --> K[Initialize revisions structure]
```

**Key Integration Points:**

1. **Automatic saving:** No user action required, revisions saved before overwrite
2. **Optional notes:** User can describe changes, but not required
3. **Metadata tracking:** Word counts, timestamps, change summaries automatic
4. **Action prompts:** After generation, suggest comparison and history commands
5. **Safety-first:** Never overwrites without saving previous version

## Best Practices

**1. Add revision notes for major changes**
- Brief notes help future you understand what changed
- "Rewrote ending", "Added flashback scene", "Tightened dialogue"
- Auto-generated notes are fine for minor tweaks

**2. Review revisions periodically**
- Check revision history after several updates
- Identify if you're cycling (adding/removing same content repeatedly)
- Consider if earlier version was better

**3. Use diff to understand evolution**
- Compare first draft to current: see full journey
- Compare recent versions: see if changes are improvements
- Learn your revision patterns

**4. Restore without fear**
- Restoring creates new version, doesn't delete current
- Experiment freely: "Let me try the old ending again"
- Can always return to any version

**5. Clean up old revisions (optional)**
- If chapter has 20+ revisions, consider archiving early drafts
- Keep milestone versions (v01 initial, v10 major revision, current)
- Move others to `_archive/` subfolder if desired

**6. Compare before major changes**
- Before regenerating heavily-revised chapter, compare current to initial
- See how far you've come
- Ensure changes align with story goals

## Common Questions

**Q: How many revisions are saved?**
A: All revisions are saved. No automatic deletion. You control cleanup if desired.

**Q: What if I don't want automatic revision saving?**
A: You can disable it in workflow, but not recommended. Revisions are safety net for experimentation.

**Q: Can I manually create a revision checkpoint?**
A: Yes. Run `/write:chapter --save-revision` to save current version as revision without regenerating.

**Q: Do revisions count toward word count goals?**
A: No. Only current chapter version counts in PROJECT.md `current_word_count`.

**Q: Can I compare versions across different chapters?**
A: No. Diff is within-chapter only. Comparing Chapter 1 v1 vs Chapter 2 v1 wouldn't be meaningful.

**Q: What if I accidentally delete current chapter file?**
A: Restore latest revision from `.writing/chapters/chapter-{N}/revisions/`. All versions preserved.

**Q: How do I see just the current version and most recent revision?**
A: `/write:diff chapter-{N} current prev` (use alias "prev" for previous version)

**Q: Can I export revision history?**
A: Yes. Export all revisions for a chapter to see full evolution. Useful for process analysis or teaching.

**Q: Do revisions include frontmatter?**
A: Yes. Full chapter file is saved, including frontmatter. Frontmatter changes (POV, scene count, etc.) are preserved.

**Q: What about revision notes for automatic saves?**
A: Auto-saves get default note: "Automatic save before regeneration" or "Saved before restoring to v{N}". You can still add custom note.

**Q: Can I tag revisions (like "final draft", "editor feedback version")?**
A: Not built-in, but you can use revision notes for tags: "FINAL DRAFT - submitted to editor". Search notes to find tagged versions.

**Q: How much disk space do revisions use?**
A: Text is small. A 3000-word chapter is ~15-20KB. 20 revisions = ~300-400KB. Negligible for modern storage.

**Q: Can I see revision history across all chapters?**
A: `/write:revisions --all` shows summary for all chapters. Useful for project-wide revision overview.

---

**Ready to track your chapter evolution?**

Revisions are automatic—just write and revise freely.

Commands:
- View history: `/write:revisions <chapter>`
- Restore version: `/write:restore <chapter> <version>`
- Compare versions: `/write:diff <chapter> <v1> <v2>`
