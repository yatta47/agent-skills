---
name: session-feedback
description: "Review a session and propose improvements to project rules, skills, and workflows"
---

# Session Feedback

Extract insights from a working session and determine if any improvements should be made to project rules (CLAUDE.md), skills, or operational workflows.

**Manual trigger only**: Use `/session-feedback` at the end of a working session.

## When to Use

- End of a working session
- After trying a new workflow or tool
- After troubleshooting or trial-and-error

## Review Perspectives

Review the session from these 5 perspectives:

### 1. Project Rules (CLAUDE.md)

- Were there policy or rule changes that affect the whole project?
- Is there anything that should always be kept in mind for future sessions?

### 2. New Skills

- Was there a repeatable workflow that could be turned into a skill?
- Was there a work pattern that could be standardized?

### 3. Existing Skills Improvements

- Were there issues with skills used during the session?
- Were there missing features or perspectives?

### 4. Operational Rules

- Were there improvements needed in issue management, git workflow, file structure, etc.?
- Did new operational patterns emerge?

### 5. Writing Voice Observations (optional)

- Were there notable expressions, phrasing patterns, or thought patterns from the user?
- Are there characteristics worth recording for content generation consistency?
- Were there impressive phrases that could be added to a reference collection?

## Output Format

```markdown
## Session Feedback

### 1. Project Rules
- (content if any, otherwise "None")

### 2. New Skills
- (content if any, otherwise "None")

### 3. Existing Skills Improvements
- (content if any, otherwise "None")

### 4. Operational Rules
- (content if any, otherwise "None")

### 5. Writing Voice Observations
- (content if any, otherwise "None")

### Summary
(One-line comment)
```

## Guidelines

- Don't force content. "None" is a normal result — not every session produces actionable feedback
- When proposing changes, include specific actions (what to change, where to add it)
- Present proposals for user approval (don't make changes without confirmation)
