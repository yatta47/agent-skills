---
name: til-extract
description: "Extract TILs (Today I Learned) from conversations or files and save as Markdown notes"
---

# TIL Extract

Extract Q&A, learnings, and gotchas from conversations or files, and save them as TIL (Today I Learned) Markdown notes.

**Manual trigger only**: Use `/til-extract` at the end of a conversation or when you encounter something worth noting.

## Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| TIL output directory | `til/` | Where TIL files are saved. Override by setting a different path in your project's CLAUDE.md |

If your project uses a different path (e.g., `knowledge/til/`, `docs/til/`), add to your CLAUDE.md:
```
TIL output directory: knowledge/til/
```

## Usage

```
/til-extract                          # Extract from current conversation
/til-extract path/to/file.md          # Extract from a specific file
/til-extract docs/deep-dive/*.md      # Extract from multiple files via glob
```

## Input Mode

| Argument | Mode | Source |
|----------|------|--------|
| None | Conversation mode | Current session's conversation |
| File path | File mode | Specified file contents |

## Steps

### 0. Determine Input Source

- **No argument**: Conversation mode → Step 1
- **With argument**: File mode → Step 1B

### 1. Review Conversation (Conversation Mode)

Review the current session and look for TIL signals:

**Detection signals**:
- Q&A patterns (user asked "what does this mean?" and got an answer)
- "I didn't know that", "TIL", "interesting"
- "Got stuck", "error", "broken", "gotcha"
- New findings from web searches or deep-dives
- "I see", "so that's how it works"
- Trial and error during configuration or tool setup

### 1B. Extract from File (File Mode)

Read the specified file and extract TILs.

**File mode extraction criteria (stricter than conversation mode)**:

Files are usually already organized. Extracting everything as TIL is pointless. Only extract:

- **Surprising facts**: Insights that differ from common understanding
- **Specific numbers, limits, specs**: Precise, actionable information
- **Gotchas and caveats**: Things that cause trouble if you don't know them
- **Comparison and selection criteria**: Why A instead of B, with concrete reasons

**Do not extract**:
- File summaries (just read the file itself)
- General explanations or definitions (textbook-level knowledge)
- Context-dependent information that loses meaning in isolation

**source**: For file mode, set frontmatter `source` to the file path (e.g., `source: docs/deep-dive/20260221-xxx.md`)

### 2. Auto-detect Type

Classify each TIL by type:

| Type | Detection Pattern |
|------|-------------------|
| troubleshoot | Error, stuck, fix, workaround context |
| discovery | Newly learned, first time knowing, research result |
| comparison | A vs B, comparison, selection, ended up choosing C |
| insight | Realization, mindset shift, "thinking about it this way works" |

### 3. Output Format (by type)

**troubleshoot**: Preserve error messages and commands in code blocks

```markdown
---
title: ""
type: troubleshoot
tags: []
created: YYYY-MM-DD
source: session  # or file path
---

Running `command` produced an error:

\```
$ command
Error message verbatim
\```

Cause: ...

Fix:

\```
$ fix command
\```
```

**discovery**:

```markdown
---
title: ""
type: discovery
tags: []
created: YYYY-MM-DD
source: session
---

What was learned. Background if relevant.
```

**comparison**:

```markdown
---
title: ""
type: comparison
tags: []
created: YYYY-MM-DD
source: session
---

Options: A vs B
Criteria: ...
Conclusion: Chose B because...
```

**insight**:

```markdown
---
title: ""
type: insight
tags: []
created: YYYY-MM-DD
source: session
---

The insight. Why it matters.
```

### 4. File Name and Location

- **Save to**: `til/` (or configured TIL output directory)
- **File name**: `YYYYMMDD-{slug}.md`
- slug: kebab-case generated from title (English, max 30 chars)
- 1 TIL = 1 file (never combine multiple TILs into one file)

### 5. Save and Commit

- `git add til/*.md` (adjust path to your TIL directory)
- Commit message: `Add TIL: {count} items ({date})`

### 6. Report

Report extraction results:

```
[til-extract] Reviewing conversation...          # Conversation mode
[til-extract] Reading files... (2 files)         # File mode
[til-extract] Found {N} TILs

1. [troubleshoot] mise fails to install procs → til/20260222-mise-procs-aqua-registry.md
2. [discovery] Kafka 4.2 Share Groups → til/20260222-kafka-42-share-groups.md
3. [insight] "Saying" vs "conveying" → til/20260222-saying-vs-conveying.md

Saved. Let me know if any should be removed.
```

## Extraction Rules

- **Respect the user's own words**. When the user rephrases their understanding ("so basically it's..."), preserve that as a "## My Understanding" section in the TIL. Don't rewrite it into a polished explanation. The value is in capturing how they understood it at the time
- **Don't force TILs**. If there's nothing to extract, report "No TILs found in this conversation"
- **Preserve error messages, logs, and command output verbatim** in code blocks (don't summarize)
- **Always redact secrets** (tokens, passwords, API keys, signed URLs, private hostnames). Replace with `<REDACTED>` or `xxx` before saving
- Stack traces: excerpt relevant parts only (full trace not needed)
- Include the executed command alongside errors (redact secrets in commands too)
- Multiple TILs per session is fine
- If same-day slug collision occurs, append a number (e.g., `20260222-mise-procs-aqua-registry-2.md`)
- **Include source URLs when possible**. Official docs, GitHub Issues/Discussions, blog posts — add a `## References` section at the end. If no URL is available (experience-based), skip it

## Notes

- Don't quote user statements verbatim (privacy consideration)
- TIL is "what I learned" memo. Article seeds are "what's worth sharing with others". Overlap is fine
- No need to check for duplicate TILs (manual cleanup later is fine)
