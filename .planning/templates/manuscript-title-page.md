# Manuscript Title Page Template

<!-- Industry-standard title page for manuscript submissions -->
<!-- Used by /write:export when creating full manuscript with title page -->

```




                                                                    {word_count} words
                                                                    {genre}




                    {TITLE}

                        by

                      {AUTHOR}





Contact:
{author_email}
{author_phone}
{author_address}
```

---

## Usage Notes

This template follows standard manuscript submission conventions recognized by agents, publishers, and contests.

### Layout Specifications

- **Word count:** Upper right corner (aligned ~65-70 characters from left margin)
- **Genre:** Below word count (optional, some submissions request this)
- **Title:** Centered, approximately 1/3 down the page (12-15 blank lines from top)
  - Use ALL UPPERCASE for professional submissions
- **By-line:** Centered below title (1 blank line separation)
- **Author name:** Centered below "by" (1 blank line separation)
- **Contact information:** Lower left corner, starting 8-12 blank lines from author name
  - Email address
  - Phone number (optional)
  - Mailing address (optional)
- **No header or page number** on title page itself

### Variable Replacement

During export, the `/write:export` workflow replaces these placeholders with actual values:

| Placeholder | Replaced With | Example |
|-------------|---------------|---------|
| `{word_count}` | Total manuscript word count | `75,000 words` |
| `{genre}` | Genre from PROJECT.md | `Fantasy` |
| `{TITLE}` | Story title in ALL UPPERCASE | `THE SHADOW'S APPRENTICE` |
| `{AUTHOR}` | Author name (prompted or from PROJECT.md) | `Jane Martinez` |
| `{author_email}` | Email address (optional) | `jane@email.com` |
| `{author_phone}` | Phone number (optional) | `(555) 123-4567` |
| `{author_address}` | Mailing address (optional) | `123 Main St, City, ST 12345` |

**Note:** Contact fields are omitted if not provided during export. Writer can choose to include email only, email + phone, or all contact details.

### Format Variations

The export workflow adapts the title page for different output formats:

#### Markdown Export (.md)

Uses markdown heading syntax with preserved spacing:

```markdown
                                                                    75,000 words
                                                                    Fantasy




# THE SHADOW'S APPRENTICE

## by

## Jane Martinez





**Contact:**
jane@email.com
(555) 123-4567
```

Renders nicely in markdown viewers while maintaining professional layout.

#### Plain Text Export (.txt)

Plain text with spacing preserved using blank lines and approximate centering:

```
                                                                    75,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





Contact:
jane@email.com
(555) 123-4567
123 Main St, Portland, OR 97201
```

Centering approximated using leading spaces based on typical 80-character text editor width.

#### Standard Manuscript Format (.txt)

Industry-standard plain text with exact positioning and spacing:

```
                                                                    75,000 words
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





Contact:
jane@email.com
(555) 123-4567
123 Main St, Portland, OR 97201
```

Follows industry submission guidelines:
- Word count right-aligned on first line
- Title approximately 1/3 down page (12-15 line breaks)
- All elements centered or positioned per convention
- Contact info lower left (not centered)
- NO running header or page number on title page

---

## Alternative Formats

### Minimal Title Page (Beta Readers)

For less formal sharing or beta reader copies:

```
THE SHADOW'S APPRENTICE
by Jane Martinez

75,000 words
Fantasy
```

Simple, concise, suitable for casual distribution.

### Conference Manuscript (Partial Submission)

For conference critiques or partial manuscript requests:

```
                                                                    First 50 pages
                                                                    75,000 word novel
                                                                    Fantasy




                    THE SHADOW'S APPRENTICE

                        by

                      Jane Martinez





Contact:
jane@email.com
```

Indicates partial submission with total novel length noted.

---

## Customization

Writers can customize the title page per project:

1. Copy this template to your story directory: `stories/{project}/TITLE-PAGE.md`
2. Modify layout, add elements, or adjust spacing
3. The export workflow will check for local template first before using this global version

**Common customizations:**
- Add copyright notice: `© 2026 Jane Martinez`
- Add agent information (if represented): `Represented by: [Agent Name, Agency]`
- Add word count category: `Middle Grade Fantasy Novel`
- Omit genre line if submission guidelines don't request it

---

## Industry Standards Reference

### Agent/Publisher Submissions

Most agents and publishers expect:
- **Word count** in upper right (some specify category like "Adult Fiction" instead of exact count)
- **Title and author** centered ~1/3 down page
- **Contact info** lower left or upper left (conventions vary slightly)
- **No decorative elements** - plain text only
- **12pt monospaced font** (Courier or Courier New) - simulated in .txt files

### Contests

Many writing contests require:
- **Anonymous submissions:** Omit author name and contact from title page
- **Title only** centered
- **Word count** upper right
- **Separate cover page** with author info for contest administrators

For anonymous submissions, create a separate version without author details.

### Self-Publishing

For self-publishing (Amazon KDP, IngramSpark):
- Title page formatting is flexible
- Can include copyright, ISBN, publisher name
- No specific industry standard required

This template focuses on traditional submission standards.

---

## Examples

### Example 1: Full Contact (Agent Submission)

```
                                                                    85,000 words
                                                                    Science Fiction




                    ECHOES OF THE VOID

                        by

                      Marcus Chen





Contact:
marcus.chen@email.com
(555) 987-6543
456 Oak Avenue
Seattle, WA 98101
```

### Example 2: Email Only (Contest Submission)

```
                                                                    12,000 words
                                                                    Short Fiction




                    BENEATH THE WILLOW

                        by

                      Sarah Kim





Contact:
sarah.kim@email.com
```

### Example 3: Anonymous (Contest Requirement)

```
                                                                    7,500 words
                                                                    Literary Fiction




                    THE LAST LETTER
```

No author or contact information (submitted separately).

---

## Common Questions

**Q: Should I include my home address?**
A: Optional. Many writers include email and phone only. Physical address is traditional but not required in digital era. Publishers and agents primarily use email.

**Q: What if my word count is approximate?**
A: Round to nearest hundred or thousand. "~75,000 words" or "75,000 words" both acceptable. Don't stress exact precision - ballpark is fine.

**Q: Should the title be in quotes?**
A: No. Use ALL CAPS without quotes for traditional submissions. Quotes and italic not standard on manuscript title pages.

**Q: What about pen names?**
A: Use legal name in contact info, pen name as byline author. Or use pen name throughout if established. Disclose legal name when requested by contract.

**Q: Do I need copyright notice?**
A: Not required. Work is copyrighted automatically upon creation. Some authors include "© [Year] [Name]" but not industry standard for submissions.

**Q: What if my title is very long?**
A: Long titles (10+ words) can be broken into multiple centered lines. Each line centered independently.

---

## Template Version

- **Version:** 1.0
- **Last updated:** 2026-02-27
- **Compatible with:** /write:export workflow
- **Standard:** Industry submission format (US market conventions)
