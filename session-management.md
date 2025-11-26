# Session Management Guide

Manage Claude Code sessions to avoid context rot while maintaining continuity.

## When to Restart

**After 2-3 major features, or when you notice:**
- Claude suggesting patterns different from what you established
- Having to re-explain things covered earlier
- Code quality declining
- More errors or back-and-forth

## Before Restarting: Document

**Create a session notes file capturing:**

1. **Accomplished:** Features completed, tests written, bugs fixed, files changed
2. **Current State:** What's working, tested, deployed/merged
3. **What's Next:** Immediate steps, known issues, questions for team
4. **Context for Fresh Session:** Patterns established, decisions made, key info Claude needs

## Where to Save

**Team Projects (Balance):**
```bash
.claude/sessions/YYYY-MM-DD-feature-name.md
# or
docs/dev-sessions/YYYY-MM-DD-your-name.md
```

**Solo Projects:**
```bash
.claude/sessions/YYYY-MM-DD.md
# or simple
dev-log.md  # Append to running log
```

**Why in project?** Version controlled, visible to team, persists across computers, easy for Claude to find.

## Session Notes Templates

### Team Project Template

```markdown
# [Date] - [Feature]

## Context
Working on: [Feature]
Related: [Issue/PR]

## Accomplished
- [Task 1]
- [Task 2]

## Files Changed
- path/file1.tsx (added X)
- path/file2.test.tsx (added tests)

## Current State
- ✅ [Working and tested]
- ⚠️  [Partially done]
- ❌ [Not started]

## Next
1. [Immediate task]
2. [Following task]

## Patterns Established
- Matching X pattern for Y components
- Using Z helpers (not reinventing)

## Questions/Blockers
- @name: Question about X

## Commits
- abc123: Description
```

### Solo Project Template

```markdown
# [Date] - [Feature]

## Done
- [Task 1]
- [Task 2]

## Working
- [What works]
- Tests passing

## Next
1. [Task]
2. [Task]

## Notes
- Using X approach because Y
```

## Starting Fresh Session

### Step 1: Load Context

**Team project:**
```markdown
Continuing [feature] for [project].

Context:
- Read .claude/sessions/YYYY-MM-DD-feature.md
- Read pm-who-codes.md and quality-gates.md

Task: [What you're working on]
```

**Solo project:**
```markdown
Continuing [project].

Context:
- Read dev-log.md
- Read solo-project-standards.md and quality-gates.md

Next: [Task]
```

### Step 2: Verify Context

```
Confirm you understand:
- What I accomplished last session
- Patterns we established
- What we're working on next
```

### Step 3: Break Down Task

```
Break down "[next task]" into small tasks.
Use TodoWrite to track.
```

## Git as Documentation

Your frequent commits are also documentation:

```bash
git log --oneline -10  # See recent work
git diff HEAD~5..HEAD  # See changes
```

Tell Claude: `Run git log --oneline -10 to see last session progress.`

## Examples

### Balance - End Session

```bash
# Create notes
code .claude/sessions/2025-11-26-login.md
# Document: done, next, patterns, questions
# Commit
git add .claude/sessions/2025-11-26-login.md
git commit -m "Session notes: login progress"
git push
```

### Balance - Start Fresh

```markdown
Continuing Balance login feature.

Context:
- Read .claude/sessions/2025-11-26-login.md
- Read pm-who-codes.md, quality-gates.md
- Team project with senior engineers

Next: Add error handling to login form

Confirm understanding, then break down into small tasks.
```

### Solo - End Session

```bash
# Append to log
echo "## Nov 26 - Auth
- Basic auth flow done
- Tests passing
- Next: Error handling
" >> dev-log.md

git add dev-log.md
git commit -m "Dev log: auth progress"
```

### Solo - Start Fresh

```markdown
Continuing [project].

Context:
- Read dev-log.md
- Read solo-project-standards.md, quality-gates.md

Next: Add error handling to auth

Break into small tasks.
```

## Quick Reference

**When to restart:**
- After 2-3 major features
- When quality drops
- When Claude forgets context

**Before restarting:**
1. Document what you did
2. Document what's next
3. Save in project
4. Commit and push

**Starting fresh:**
1. Tell Claude to read session notes
2. Tell Claude to read memory system files
3. Verify Claude has context
4. Break down next task

**Team vs Solo:**
- **Team:** Detailed notes, questions for team, commit notes file
- **Solo:** Simpler dev-log.md, focus on done/next

---

**Goal:** Enough context to pick up where you left off with fresh Claude that knows what you're doing.
