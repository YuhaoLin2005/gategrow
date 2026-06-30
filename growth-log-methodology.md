# Growth Log Methodology

> How to write learning entries that compound across sessions — not diary entries that rot.

## The Core Idea

A **growth-log entry** is a compressed unit of learning. It captures a pattern you recognized, a mistake you made, or an insight you had — written so your future self can actually use it.

This is different from:
- **A diary** — "Today I fixed a bug in the payment module" (what happened, not what to learn)
- **A log** — "2026-07-01 14:23: fixed NULL pointer in PaymentService.java" (timestamp, no pattern)
- **Documentation** — "The PaymentService class handles payment processing" (what the code does, not what you learned)

A real growth-log entry answers: **"Next time I face a similar situation, what do I do differently?"**

## Entry Template

```markdown
## [Pattern name, not event name]

### Context
- What was I trying to do?
- What went wrong / what worked surprisingly well?

### Root Cause / Core Insight
- The underlying mechanism, not just the symptom

### The Pattern (transferable)
- Next time [similar situation], I will [specific action].
- Signal to recognize: [what observable tells me this pattern is active?]

### Related
- [link to related entries]
```

### Example: Good Entry

```markdown
## Configuration inheritance ≠ behavioral inheritance

### Context
- Session continued from a previous one. Same repo, same task.
- Assumed all previous rules were still active.

### Root Cause
- `settings.json` autoCompactWindow was 300 from an old experiment.
- Configuration persists across sessions even when the reasoning behind it doesn't.

### The Pattern
- Next time I continue a task across sessions, I will re-verify all config values before acting.
- Signal to recognize: any session that starts with "continuing from previous"

### Related
- [[session-context-is-not-persistent]]
- [[verify-assumptions-on-session-start]]
```

### Example: Bad Entry (Diary)

```markdown
## Fixed the payment bug

Today I debugged a payment issue. The NULL pointer was in PaymentService.java.
Took 2 hours. Finally found it by adding print statements.
```

This is useless next month. No pattern. No transferable action. Just narration.

## Three Rules

### 1. Failures > Achievements

One bug that took 2 hours teaches more than 3 features that worked first try. Failures are nutritionally denser — they reveal edge cases, broken assumptions, and missing checks. Achievements confirm what you already know.

**Rule of thumb**: If a session was smooth sailing, you might not need an entry. If you hit a wall, you definitely do.

### 2. The Bole Principle (伯乐原则)

Before writing a new entry, ask: *"Is this fundamentally the same root cause as something I already recorded?"*

- **Same root, different symptom** → Merge into the existing entry. Add the new symptom as a signal.
- **New root** → New entry.

This prevents the growth-log from becoming a graveyard of duplicate lessons. The goal is a **pattern library**, not a chronological archive.

### 3. Must Be Transferable

Every entry must contain a sentence that starts with **"Next time I will…"** or **"Next time I face…"** .

If you can't write that sentence, you haven't extracted the pattern yet. Go deeper. Ask:
- What was the earliest signal I missed?
- What assumption did I make that turned out wrong?
- What check could have caught this 10 minutes in instead of 2 hours in?

## Quality Checklist

Before finalizing an entry, verify:

- [ ] Title names the **pattern**, not the event ("Configuration inheritance ≠ behavioral inheritance" not "Session continuation bug")
- [ ] There's a "Next time I will…" sentence
- [ ] The "signal to recognize" is specific enough to trigger (not "be more careful")
- [ ] Searched existing entries for duplicates (Bole Principle)
- [ ] Root cause is distinguished from symptom ("NULL pointer" is symptom; "assumed config state persists" is root cause)
- [ ] Entry is 4–8 sentences (shorter = too shallow; longer = narrating events)

## Anti-Patterns

| Anti-Pattern | Why it fails | Fix |
|-------------|-------------|-----|
| "Today I learned…" | Narration, not pattern extraction | Name the pattern |
| "Be more careful next time" | Vague, not actionable | Specify the check or signal |
| Lists every bug from the session | Quantity over quality | Merge same-root bugs; skip one-offs you already understand |
| Copy-pastes error messages | Symptom, not insight | Extract what the error *revealed about your assumptions* |
| Writes entries for every session | Noise dilutes signal | Only write when you learned something genuinely new |

## Review Cadence

Growth-log entries compound when you review them:

| Cadence | Action |
|---------|--------|
| **Daily** (session end) | Write one entry if the session was complex or surprising |
| **Weekly** | Skim this week's entries. Any patterns repeating? If yes → merge or escalate |
| **Monthly** | Full review. Which patterns have you successfully applied? Which keep recurring despite entries? The recurring ones need a **system change** (checklist, hook, linter rule), not another entry |
| **Quarterly** | Archive stale entries. Patterns you've fully internalized can move to an "integrated" section |

## Tool-Agnostic Setup

The methodology works with any system:

- **Markdown files** — `~/notes/learning/2026-07-01.md`. Simplest. Searchable.
- **Notion/Obsidian/Logseq** — Use the template as a page template. Links between entries become backlinks.
- **Physical notebook** — One entry per page. Review by flipping through. The friction is the point.

## Why This Works

The framework addresses the two reasons learning capture fails:

1. **We forget** → The gate reminds you (mechanical, not willpower-based)
2. **We write useless entries** → The methodology teaches you what a useful entry looks like

Together they close the loop: gate enforces the habit, methodology ensures the content is worth capturing.
