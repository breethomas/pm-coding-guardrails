# PM Who Codes - Role Clarity & Philosophy

## Your Role as PM Who Codes

**You're a product manager who codes, not a software engineer.**

This distinction matters:
- **Goal:** Ship features quickly while respecting engineering quality
- **Strength:** Product thinking, prototyping, getting things done
- **Limitation:** Not a professional software engineer
- **Responsibility:** Don't create more work for the team than the feature is worth

## Core Principles

### 1. Consistency > Personal Preference

When working in existing codebases:
- **Study similar code first** - Find components/patterns that match what you're building
- **Match patterns exactly** - Spacing, naming, structure, everything
- **Don't innovate on architecture** - Use what's already there
- **Ask before deviating** - If you think you need a new pattern, ask first

### 2. CI Must Pass Locally First

**The #1 Problem to Solve: Pushing PRs that fail CI/CD**

Non-negotiable rule:
- Run ALL the same checks locally that CI will run
- Don't commit until everything passes
- Don't push until you've verified in the actual environment

If Claude suggests committing without passing checks → **STOP and run checks first**

### 3. Quality > Speed

Shipping fast is good. Shipping sloppy code is not.

Before pushing code, ask:
- **Is this creating more work than it saves?**
- **Will this be easy for the team to maintain?**
- **Did I follow their patterns or force my own?**

If the answer to any is "no" → **refactor before pushing**

### 4. Test Before Ship

Untested code is broken code you haven't discovered yet.

Minimum testing:
- **Manual testing:** Does it actually work in the real environment?
- **Automated tests:** Follow project conventions (some require tests, some don't)
- **Edge cases:** What breaks this? Test those scenarios

### 5. Know When to Ask

You're not expected to know everything. Ask before:
- Creating new architectural patterns
- Deviating from established conventions
- Making decisions that affect the team
- Shipping something you're not confident about

**It's better to ask than to create work for others cleaning up your code.**

## Working with Claude

Claude is your pair programmer, but you're responsible for:
- **Directing the approach** - "Match the existing pattern in X component"
- **Verifying quality** - Run checks, test thoroughly
- **Making judgment calls** - "Is this good enough or should I ask the team?"

Claude will help you write code. You ensure it's responsible code.

### Session Management

**Context rot is real.** After 2-3 big tasks, restart your session:

1. **Before restarting:** Document what you worked on (what changed, what's next)
2. **Start fresh:** New session with clean context
3. **Load documentation:** Use your docs as context, not chat history

This keeps Claude focused and prevents quality degradation from long sessions.

### Task Breakdown

**The smaller the task, the better the output.**

Break work into laser-focused chunks:
- **Bad:** "Build user authentication"
- **Good:** "Add login form component matching existing pattern in SignupForm.tsx"

Use TodoWrite to track progress. Force yourself to break tasks smaller than feels necessary. Each task should be completable in one focused session.

### Documentation First

Before coding, write documentation:
- **Context files:** What Claude needs to know about this feature/area
- **Design decisions:** Why you're taking this approach
- **Patterns to follow:** Link to similar code, note what to match

Markdown files > trying to explain everything in chat.

## When Working Solo vs. With Team

### Solo Projects
- Focus on maintainability - future you should understand this
- Keep it lean - simple > clever
- Document why, not just what
- Test enough to be confident it works

### Team Projects
- Follow their workflow religiously
- Use their tools and conventions
- Run their quality checks
- Respect their architectural decisions
- Don't create cleanup work for senior engineers

## Success Metrics

You're doing this right when:
- ✅ PRs pass CI on first push
- ✅ Code reviews focus on product decisions, not code quality issues
- ✅ Senior engineers aren't cleaning up after you
- ✅ Your code is maintainable 6 months later
- ✅ You're shipping quality code that creates value

---

*This is not about being a perfect engineer. It's about being a responsible one.*
