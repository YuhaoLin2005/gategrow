# gategrow

> **Gate the habit. Grow the content.** — A lightweight framework for closing the learning loop in knowledge work.

## The Problem

Code review checks your code. CI checks your build. Linters check your style.

But nobody checks whether **you** captured what you learned.

After a complex debugging session, after an architecture decision with tradeoffs you'll forget next month, after a surprising insight — the default is silence. The session ends. The learning evaporates.

Over months of "ship and forget," the human hasn't grown. The codebase improved. The engineer didn't.

## What gategrow Does

gategrow pairs two simple ideas into a closed loop:

| Component | What it checks | How it works |
|-----------|---------------|-------------|
| **delivery-gate** | Did you capture something? | Mechanical check at session end — file timestamps, disk space. No AI, no config. |
| **growth-log** | Did you capture the *right* thing? | Methodology for extracting reusable patterns from experience — not diary entries. |

**Gate** enforces the habit. **Grow** teaches the content. Each is independently useful. Together they close the loop.

```
You work → session ends → gate fires:
  → "Did you touch a learning file today?"
    → No (complex task) → BLOCKED: "What did you learn?"
    → Yes → pass

When blocked → growth-log methodology kicks in:
  → Pre-check: do your learning files exist?
  → Teach: how to write entries that compound across sessions
  → Three rules: Failures > Achievements · Bole Principle · Must be transferable
```

## Principles

### 1. Mechanical, not aspirational

The gate checks file timestamps and disk space — deterministic facts, not self-reported status. The same pattern as CI pipeline gates: automated, reproducible, zero-configuration.

### 2. Fail-open by default

If the gate can't determine a fact (platform command fails, transcript unreadable), it passes. Never block on uncertainty. Only block on verified facts.

### 3. Methodology over diary

A growth log entry that says "fixed a bug in payment module" is a diary entry — useless next month. A real entry extracts the **pattern**: what signal to recognize, what root cause was, what to do differently next time.

### 4. Language and platform agnostic

The concepts work with any note-taking system (Markdown files, Notion, Obsidian, plain text) and any work context (software engineering, research, design, management). The reference implementation targets Claude Code, but the ideas are universal.

## The Growth Log Methodology

### Three Rules

1. **Failures > Achievements** — One bug that took 2 hours teaches more than 3 features that worked first try. Failures are nutritionally denser.

2. **The Bole Principle (伯乐原则)** — Before writing a new entry, ask: *"Is this fundamentally the same root cause as something I already recorded?"* Same root, different symptom → merge. New root → new entry.

3. **Must Be Transferable** — Every entry must answer: *"Next time I face a similar situation, what do I do differently?"* If you can't write that sentence, you haven't extracted the pattern yet.

### Entry Template

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

### Quality Checklist

- [ ] Title names the *pattern*, not the event
- [ ] There's a "Next time I will…" sentence
- [ ] The "signal to recognize" is specific enough to trigger
- [ ] Searched existing entries for duplicates (Bole Principle)
- [ ] Root cause is distinguished from symptom
- [ ] Entry is 4–8 sentences (shorter = too shallow; longer = narrating events)

## Reference Implementation

The concepts originated in [Everything Claude Code (ECC)](https://github.com/affaan-m/ECC) as `delivery-gate` (a Stop hook) and `growth-log` (a skill). This repository is the independent, generalized community space for these ideas.

- **delivery-gate.js** — ~340 lines, Node.js, zero npm dependencies. Checks disk space + learning library freshness via filesystem timestamps. Fail-open throughout.
- **growth-log SKILL.md** — Methodology documentation with pre-check, entry template, anti-patterns, and quality checklist.

## Getting Started

### For Claude Code users
Install ECC with the `workflow-quality` module — delivery-gate auto-registers as a Stop hook, growth-log is available immediately. Zero configuration.

### For everyone else
The ideas are tool-agnostic:
1. Create a directory for learning entries (e.g., `~/notes/learning/`)
2. After complex work, write one entry following the template above
3. Use a recurring reminder (calendar, cron, shell prompt) to check: "Did I capture something today?"
4. Review your entries monthly — patterns that repeat are signals to build systems around

## Why "gategrow"

**Gate** = the mechanical check. The habit enforcer. The thing that says "you're not done until you've captured something."

**Grow** = the methodology. The content quality. The difference between a timestamp touch and a genuinely useful learning artifact.

One without the other fails: enforcement without methodology → empty entries. Methodology without enforcement → forgotten captures.

## License

MIT

## Community

This is an independent community space. Contributions, adaptations, and translations welcome. The ideas are meant to spread — implementation details are secondary.
