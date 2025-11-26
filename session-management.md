# Session Management Guide

Practical guidance for managing Claude Code sessions to avoid context rot while maintaining continuity.

## Why This Matters

**Context rot is real.** After 2-3 big tasks in a session, Claude's output quality degrades. You'll notice:
- Suggestions get vaguer
- Claude forgets patterns you established earlier
- Code quality drops
- More errors creep in

**The solution:** Document your work, restart your session, load from documentation.

## When to Restart Your Session

### Signs It's Time to Restart

**After 2-3 major features/tasks**, or when you notice:
- ❌ Claude suggesting patterns different from what you established
- ❌ Having to re-explain things you covered earlier
- ❌ Code quality feels lower than the start of session
- ❌ More back-and-forth to get what you want

### Before Restarting: Document Your Work

**Don't just close and restart.** That loses all your progress context. Document first.

## Session Documentation: What to Capture

Create a session notes file documenting:

### 1. What You Accomplished
- Features completed
- Tests written
- Bugs fixed
- Files changed

### 2. Current State
- What's working now
- What's tested
- What's deployed/merged

### 3. What's Next
- Immediate next steps
- Known issues to address
- Questions for the team (if applicable)

### 4. Context for Fresh Session
- Patterns you established
- Decisions you made and why
- Things Claude should know when you restart

## Where to Save Session Notes

### For Team Projects (like Balance)

**Option A: Project .claude directory**
```bash
# Create if doesn't exist
mkdir -p .claude/sessions

# Save with date
.claude/sessions/2025-11-26-login-feature.md
```

**Option B: Project docs directory**
```bash
# If team has a docs structure
docs/dev-sessions/2025-11-26-bree-login.md
```

**Option C: Running dev log**
```bash
# Single file you append to
.claude/dev-log.md
```

**Why in the project?**
- Version controlled with git
- Other engineers can see your progress
- Persists across computers
- Easy for Claude to find when you restart

### For Solo Projects

**Option A: Project .claude directory** (same as team)
```bash
.claude/sessions/2025-11-26.md
```

**Option B: Simple dev-log.md**
```bash
# Keep it simple for solo work
dev-log.md  # Lives in project root
```

**Why in the project?**
- Future you needs to remember what you did
- Version controlled
- Easy to pick up after weeks away

## Session Notes Template

### For Team Projects

```markdown
# Dev Session - [Date]

## Context
Working on: [Feature name]
Related to: [Linear issue, PR, etc.]

## What I Accomplished
- [Completed task 1]
- [Completed task 2]
- [Completed task 3]

## Files Changed
- path/to/file1.tsx (added login form component)
- path/to/file2.test.tsx (added tests)
- path/to/file3.ts (updated validation helpers)

## Current State
- ✅ [What's working and tested]
- ⚠️  [What's partially done]
- ❌ [What's not started yet]

## What's Next
1. [Immediate next task]
2. [Following task]
3. [After that]

## Patterns Established
- Matching SignupForm.tsx pattern for auth components
- Using utils/validation.ts helpers (not reinventing)
- Tests follow AuthForm.test.tsx structure

## Questions/Blockers
- [ ] @engineer-name: Question about error handling approach
- [ ] Need design review on error states

## Commits
- abc123: Add login form component
- def456: Add login form tests
- ghi789: Update validation helpers
```

### For Solo Projects

```markdown
# [Date] - [Feature]

## Done
- [Task 1]
- [Task 2]
- [Task 3]

## Working
- [Feature] works for happy path
- Tests passing
- Ready to add error handling

## Next
1. [Next task]
2. [After that]

## Notes
- Using [pattern] approach because [reason]
- Files: [list of main files touched]
```

## Starting a Fresh Session

### Step 1: Tell Claude to Load Context

**For team projects (Balance):**
```markdown
I'm continuing work on [feature name].

Context:
- Read .claude/sessions/2025-11-26-login-feature.md
- Read pm-who-codes.md for working philosophy
- Read quality-gates.md for commit checklist

Current task: [What you're working on next]
```

**For solo projects:**
```markdown
Continuing work on [project name].

Context:
- Read dev-log.md for what I did last session
- Read solo-project-standards.md for approach
- Read quality-gates.md for commit checklist

Next: [What you're working on]
```

### Step 2: Verify Claude Has Context

Ask Claude to confirm what it knows:
```
Before we start, confirm you understand:
- What I accomplished last session
- What patterns we established
- What we're working on next
```

If Claude's summary is accurate, proceed. If not, clarify before coding.

### Step 3: Break Down Next Task

Even though you have session notes, still break down the next task:
```
Let's break down "add error handling to login form" into small tasks.
Use TodoWrite to track them.
```

## Practical Examples

### Example: Balance Coding Session

**End of Session:**
```bash
# After completing login form, tests, and validation updates
# Create session notes
code .claude/sessions/2025-11-26-login-feature.md

# Document: what I did, what's next, patterns, questions
# Commit the session notes
git add .claude/sessions/2025-11-26-login-feature.md
git commit -m "Session notes: login feature progress"

# Push so it's backed up
git push
```

**Next Day - Fresh Session:**
```markdown
Continuing work on login feature for Balance.

Context:
- Read .claude/sessions/2025-11-26-login-feature.md
- Read pm-who-codes.md and quality-gates.md
- This is a team project with senior engineers

Next task: Add error state handling to login form

Let's start by confirming you understand where we left off,
then break down the error handling into small tasks.
```

### Example: Solo Project Session

**End of Session:**
```bash
# Append to dev-log.md
echo "## Nov 26 - User Auth
- Added basic auth flow
- Tests passing for happy path
- Next: Add error handling
" >> dev-log.md

# Commit
git add dev-log.md
git commit -m "Update dev log: auth progress"
```

**Next Session:**
```markdown
Continuing my solo project [name].

Context:
- Read dev-log.md for recent progress
- Read solo-project-standards.md for approach
- Read quality-gates.md for commit checklist

Next: Add error handling to auth flow

Let's break this down into small tasks and get started.
```

## Using Git History as Documentation

Since you commit after every small task, your git history is also documentation:

```bash
# See what you did in last session
git log --oneline -10

# See what changed
git diff HEAD~5..HEAD

# Start fresh session with this context
```

Tell Claude:
```
Run git log --oneline -10 to see what I accomplished last session.
Let's continue from there.
```

## Quick Reference

### When to restart:
- After 2-3 major features
- When quality feels lower
- When Claude forgets context

### Before restarting:
1. Document what you did
2. Document what's next
3. Save in project (.claude/sessions/ or dev-log.md)
4. Commit and push

### Starting fresh:
1. Tell Claude to read session notes
2. Tell Claude to read memory system files
3. Verify Claude has context
4. Break down next task
5. Start coding

### Team vs Solo:
- **Team:** More detailed session notes, questions for team, commit notes file
- **Solo:** Simpler dev-log.md, focus on what you did and what's next

---

**Remember:** The goal isn't perfect documentation. The goal is enough context to pick up where you left off with a fresh Claude session that knows what you're doing.
