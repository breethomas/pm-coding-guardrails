# Solo Project Standards

Standards for Bree's solo coding projects to ensure maintainability and quality.

## Goal

Create projects that are:
- **Maintainable** - You (or others) can understand and modify 6 months later
- **Lean** - Simple, focused, no bloat
- **Quality** - Not slop code, even if you're moving fast

## Core Standards

### 1. Keep It Simple

**Principle:** Simple > Clever

- Use straightforward approaches over clever tricks
- Avoid premature optimization
- Don't over-engineer for hypothetical future needs
- If you're tempted to be clever, ask: "Will I understand this in 6 months?"

**Good:**
```javascript
// Clear and obvious
function getUserName(user) {
  return user.firstName + ' ' + user.lastName;
}
```

**Bad:**
```javascript
// Clever but obscure
const getName = u => [u.firstName, u.lastName].filter(Boolean).join(' ');
```

### 2. Make It Lean

**Avoid:**
- Unused dependencies
- Dead code
- Duplicated logic
- Over-abstraction

**Ask yourself:**
- "Do I really need this library or can I write 10 lines of code?"
- "Is this abstraction making things clearer or more complex?"
- "Will removing this break anything?" (If no, remove it)

### 3. Document Intent

**What to document:**
- **WHY you made a decision** - Not what the code does (that should be obvious)
- **Non-obvious trade-offs** - "Using X instead of Y because Z"
- **Future considerations** - "TODO: Will need to handle Z when we add feature X"

**Don't document:**
- What the code obviously does
- Implementation details that are self-evident

**Example:**
```javascript
// Good: Explains WHY
// Using setTimeout instead of setInterval because we need to wait
// for the API call to complete before scheduling the next one

// Bad: States the obvious
// This function fetches user data
function fetchUserData() { ... }
```

### 4. Test Enough to Be Confident

You don't need 100% coverage, but you need enough confidence to ship.

**Minimum viable testing:**
- **Happy path works** - Core functionality does what it's supposed to
- **Common edge cases handled** - Empty states, errors, boundary conditions
- **Manual testing done** - You've actually used it in a realistic scenario

**Write automated tests when:**
- Logic is complex or has edge cases
- You'll forget how it works
- It's critical functionality
- It will change frequently

**Skip automated tests when:**
- It's purely presentational
- It's a throwaway prototype
- Manual testing is sufficient

### 5. Make Future Changes Easy

**Think about:**
- "If I need to change X in 6 months, how hard will it be?"
- "Can I understand what this does without running it?"
- "Are the important files easy to find?"

**Good practices:**
- Consistent file organization
- Clear naming (longer names that are obvious > short names that are cryptic)
- Extract reusable pieces (but don't over-abstract)
- Keep functions focused (one thing well)

## Development Best Practices

### Work in Small Chunks

Even on solo projects, break work into small tasks:
- Commit after each working piece
- Use TodoWrite to track progress
- Restart Claude sessions after 2-3 major features (context rot applies to solo work too)

**Why:** Smaller tasks = better code quality, even when you're the only one who will see it.

### Checkpoint Frequently

**Pattern:**
- Get one thing working → commit
- Add one test → commit
- Fix one bug → commit

You'll thank yourself when you need to revert a change or figure out when something broke.

## Pre-Ship Checklist

Before considering a solo project "done":

- [ ] **Code is maintainable** - Future you will understand it
- [ ] **No obvious bloat** - Removed unused code, unnecessary dependencies
- [ ] **Core functionality tested** - Confident it works
- [ ] **Basic documentation exists** - README explains what/why/how to run it
- [ ] **You'd want to use this** - Would you actually use this yourself?

## The 6-Month Test

**Ask yourself:**
"If I had to modify this in 6 months with no memory of writing it, would I be annoyed?"

If yes → **refactor before shipping**

## Red Flags

**Stop and refactor if:**
- You're copy-pasting the same code in multiple places
- You can't explain what a function does in one sentence
- File names like `utils.js` or `helpers.js` are growing out of control
- You're adding dependencies for trivial functionality
- You're writing code you don't understand (AI-generated without comprehension)

## Success Metrics

Your solo project is good when:
- ✅ You can explain what any part does without looking at it
- ✅ Core features work reliably
- ✅ No obvious tech debt
- ✅ Someone else could pick it up and modify it
- ✅ You're proud to show it to someone

---

*The goal: Build things you're proud of, not just things that work*
