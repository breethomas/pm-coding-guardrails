# Quality Gates - Pre-Commit Checklist

**These checks are non-negotiable. Don't commit code until ALL pass.**

## Universal Pre-Commit Checklist

Run this before EVERY commit, regardless of project:

### 1. Pattern Matching
- [ ] **Found similar code** - Located existing components/patterns that match what you're building
- [ ] **Studied the patterns** - Understand how they work and why they're structured that way
- [ ] **Matched exactly** - Your code follows the same spacing, naming, structure, organization

### 2. Code Quality
- [ ] **Formatters run** - Code is properly formatted (auto-fix applied)
- [ ] **Linters pass** - No linting errors (auto-fix applied where possible)
- [ ] **Type checking passes** - No TypeScript/type errors (if applicable)

### 3. Testing
- [ ] **Manual testing done** - Tested in actual environment (simulator, browser, etc.)
- [ ] **Feature works as expected** - Verified all acceptance criteria met
- [ ] **Edge cases tested** - Tried to break it, couldn't
- [ ] **Tests written** - Automated tests added per project conventions (or documented why not)
- [ ] **Tests pass** - All test suites pass locally

### 4. CI/CD Readiness
- [ ] **All local checks pass** - Everything CI will run has been run locally first
- [ ] **No failing tests** - Test suite is 100% passing
- [ ] **No linting errors** - Clean linting output
- [ ] **No type errors** - Clean type checking (if applicable)

### 5. Code Review
- [ ] **Only relevant files staged** - No accidental changes or unrelated files
- [ ] **Working directory clean** - No uncommitted experimental code
- [ ] **Changes are focused** - Commit does one thing, does it well
- [ ] **Would you want to review this?** - Be honest

## The CI/CD Blocker

**STOP if any of these are true:**
- ❌ "I haven't run the checks yet"
- ❌ "I'm not sure if tests pass"
- ❌ "I'll fix the linting errors after pushing"
- ❌ "CI will tell me if something's wrong"

**Instead:**
1. Run all checks locally
2. Fix all issues
3. Verify everything passes
4. THEN commit and push

## Prompt Engineering Checklist

**When modifying AI prompts (system prompts, agent prompts, etc.):**

### Before Making Changes
- [ ] **Load prompt-engineering skill** - Invoke the skill to have the framework available
- [ ] **Identify the failure mode clearly** - What specific behavior are you fixing?
- [ ] **Search for related edge cases** - What OTHER operations could have the same problem?
- [ ] **Check for dependent operations** - Do any mutations/actions require outputs from other actions?

### When Making Changes
- [ ] **Use hard constraints (NEVER) over soft guidance** - "Never do X" is more reliable than "Be careful about X"
- [ ] **Provide specific BAD/GOOD examples** - Concrete examples beat abstract rules
- [ ] **Add constraints in multiple locations** - Put critical rules in both hard_constraints AND relevant sections
- [ ] **Consider if LLM should self-improve** - For complex changes, use the meta-prompt from the skill

### After Making Changes
- [ ] **Define success criteria** - How will you know if this fix worked?
- [ ] **Test the failure mode** - Reproduce the original issue and verify it's fixed
- [ ] **Test related scenarios** - Check that fixing one thing didn't break another

### Dependent Operation Pattern
When an AI can call multiple tools, always check:
- Does Tool B require an ID or output from Tool A?
- Can Tool A and Tool B be called in parallel? (If yes + dependency = data loss)
- Add explicit "NEVER call X and Y in the same response" constraints

## Project-Specific Checks

Different projects have different requirements. See project CLAUDE.md for:
- Specific commands to run
- Testing requirements
- Additional quality checks
- Team conventions

## Quick Reference

**"What checks do I run?"**
→ Check the project's CLAUDE.md file or README for the exact commands

**"Can I skip tests this time?"**
→ No. Follow the project's testing philosophy, but don't skip verification

**"What if I'm not sure?"**
→ Ask before pushing. Better to ask than create work for others

## Success Pattern

**Good flow:**
1. Write code (small task)
2. Run formatters/linters immediately (after every file edit)
3. Test manually as you go
4. Write automated tests
5. Run full test suite
6. Verify all checks pass
7. **Commit immediately** (checkpoint)
8. Move to next small task

**Bad flow:**
1. Write a bunch of code
2. Commit without checking
3. Push and hope CI passes
4. Fix CI failures in subsequent commits ❌

## Checkpoint Strategy

**Commit after every small task, not just when "done":**

- ✅ Commit when a single component works
- ✅ Commit when a single test passes
- ✅ Commit when a single bug is fixed
- ❌ Wait until entire feature is complete

**Why:** You always have a last known good state to return to. If something goes wrong, you can revert one small change instead of losing hours of work.

**Pattern:**
```bash
# After each small task passes all checks:
git add .
git commit -m "Add login form component matching SignupForm pattern"

# Not:
# (work for 3 hours)
# git commit -m "Add authentication feature"
```

## Session Initialization

**Start sessions with many-shot examples** of what you want:

When starting a coding session, provide Claude with:
- **Patterns to follow:** "Match the pattern in components/auth/SignupForm.tsx"
- **Tests-first approach:** "Write tests first, then implementation"
- **Tools to use:** "Use the project's existing validation helper at utils/validate.ts"
- **Example outcomes:** Show similar PRs or components as reference

**Example session start:**
```
I need to add a password reset form.

Context:
- Match the pattern in SignupForm.tsx (components/auth/)
- Use existing validation helpers (utils/validate.ts)
- Tests required (see SignupForm.test.tsx for pattern)
- Follow the existing form submission flow

Let's start by reading SignupForm.tsx to understand the pattern,
then break this into small tasks.
```

This sets clear expectations and prevents Claude from inventing new patterns.

---

*These gates exist to prevent the #1 problem: pushing PRs that fail CI/CD*
