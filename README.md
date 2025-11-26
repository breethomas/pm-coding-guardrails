# PM Coding Guardrails

Coding standards and quality gates for product managers working with AI assistants in shared codebases.

## The Problem

PMs using AI to code face a unique challenge: shipping value quickly while not creating cleanup work for engineering teams. AI-assisted coding can be incredibly productive, but without guardrails, it often results in:

- PRs that fail CI/CD
- Code that doesn't match team patterns
- Tech debt that slows down the team
- Frustrated engineers cleaning up after you

## The Solution

A set of practical guidelines for PMs to code responsibly with AI assistance, whether working solo or in shared codebases with senior engineers.

## What's Inside

**[pm-who-codes.md](pm-who-codes.md)** - Core philosophy and principles
- Role clarity: PM who codes vs. software engineer
- Working in shared codebases respectfully
- Session management and context window best practices
- When to ask vs. when to ship

**[quality-gates.md](quality-gates.md)** - Pre-commit checklist
- What to check before every commit
- Checkpoint strategy for frequent commits
- How to initialize coding sessions with AI
- CI/CD readiness standards

**[solo-project-standards.md](solo-project-standards.md)** - Standards for solo projects
- Keep it simple, lean, and maintainable
- The 6-month test (will future you understand this?)
- When to test, when to document
- Pre-ship checklist

## Who This Is For

- **PMs learning to code** with AI assistance
- **PMs working in shared codebases** with engineering teams
- **Product builders** who need to ship features without creating tech debt
- **Anyone using AI to code** who wants to maintain quality and respect team conventions

## How to Use

### Option 1: Integrate with Claude Code Memory System

Add these files to your Claude Code memory system:

```bash
# Copy to your Claude Code llm-context
cp *.md ~/.claude/llm-context/coding/
```

Then reference them in your project-specific CLAUDE.md:

```markdown
## Coding Standards

When working on code:
- Read pm-who-codes.md for philosophy and approach
- Follow quality-gates.md checklist before every commit
- Apply solo-project-standards.md for personal projects
```

### Option 2: Use as Reference

Keep these files open while coding and review before commits:
- Before starting: Read pm-who-codes.md
- Before committing: Check quality-gates.md
- For solo projects: Follow solo-project-standards.md

### Option 3: Customize for Your Team

Fork this repo and adapt the guidelines to your team's:
- Specific tools and workflows
- Testing requirements
- Code review processes
- Architectural patterns

## Core Principles

1. **Consistency > Personal Preference** - Match existing patterns exactly
2. **CI Must Pass Locally First** - Never push code that fails checks
3. **Value > Speed** - Shipping tech debt isn't shipping value
4. **Test Before Ship** - Untested code is broken code
5. **Know When to Ask** - Better to ask than create cleanup work

## Key Practices from Engineering Teams

These guidelines incorporate best practices from experienced engineers working with AI:

- **Tiny task breakdown** - Keep AI laser-focused on small, discrete tasks
- **Frequent checkpoints** - Commit after every small task passes
- **Context window management** - Restart sessions after 2-3 big tasks
- **Documentation first** - Write markdown docs before coding
- **Many-shot examples** - Initialize sessions with patterns to follow

## Philosophy

This isn't about being a perfect engineer. It's about being a responsible one.

The goal: Ship features that create value without creating work for others.

## Integration Examples

### Starting a New Feature

```markdown
I need to add user authentication to the dashboard.

Context:
- Match existing patterns in components/auth/
- Follow quality-gates.md checklist
- Break into small tasks per pm-who-codes.md
- Commit after each task passes checks

Let's start by reading similar components and breaking this down.
```

### Working in a Shared Codebase

```markdown
I'm a PM working in a codebase with senior engineers.

Important:
- Study similar code first, match patterns exactly (pm-who-codes.md)
- Run all CI checks locally before committing (quality-gates.md)
- Ask before deviating from established conventions
- Commit frequently after small, working changes

Let's ensure I don't create cleanup work for the team.
```

## Contributing

Found these helpful? Have improvements? PRs welcome.

## Acknowledgments

These guidelines synthesize practices from experienced product managers and engineers:
- Core philosophy developed through hands-on PM coding work
- Best practices incorporate feedback from senior engineers working with AI
- Checkpoint and session management strategies adapted from production engineering teams

## License

CC BY-NC-SA 4.0 - Free to use for personal and internal business use with attribution.

---

Built for PMs who want to code responsibly with AI. Ship value, not tech debt.
