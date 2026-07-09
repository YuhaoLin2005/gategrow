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

See [growth-log-methodology.md](growth-log-methodology.md) for the full methodology — entry template, quality checklist, anti-patterns, and review cadence.

### Quick Rules

1. **Failures > Achievements** — One bug that took 2 hours teaches more than 3 features that worked first try.
2. **The Bole Principle (伯乐原则)** — Same root, different symptom → merge. New root → new entry.
3. **Must Be Transferable** — Every entry must answer: "Next time I face a similar situation, what do I do differently?"

## Reference Implementation

The concepts originated in [Everything Claude Code (ECC)](https://github.com/affaan-m/ECC) as `delivery-gate` (a Stop hook) and `growth-log` (a skill). This repository is the independent, generalized community space for these ideas.

- **delivery-gate.js** — ~490 lines, Node.js, zero npm dependencies. Checks disk space + learning library freshness via filesystem timestamps. Fail-open throughout. Supports project-scoped memory via `CLAUDE_PROJECT_DIR` and cross-platform disk checks (Windows wmic/PowerShell, GNU df -BG + POSIX df -Pk fallback). See [ECC scripts/hooks/delivery-gate.js](https://github.com/affaan-m/ECC/blob/main/scripts/hooks/delivery-gate.js).
- **growth-log SKILL.md** — Methodology documentation with pre-check, entry template, anti-patterns, and quality checklist. See [ECC skills/growth-log/SKILL.md](https://github.com/affaan-m/ECC/blob/main/skills/growth-log/SKILL.md).

## Validated: What the ECC Review Taught Us

The delivery-gate module was submitted to ECC (200K+ stars). Maintainer daltino reviewed it over 4 rounds. 9 bugs were found before merge.

Three lessons:

1. stdin-stdout contracts break silently in hook frameworks. Worked locally; failed in target. Platform integration bugs are invisible to local testing.

2. Bot review catches what manual testing misses. Python 3.8 compat, non-recursive scanning, missing exception handling — all caught by bots in seconds.

3. Mechanical checks and AI review cover different things. Mechanical is 100% consistent but narrow. AI review covers quality but is probabilistic. Use both.

The boundary between hard-block and soft-warn is remediability: can you fix this later? Learning not captured = unrecoverable = hard block.

The same 200-line Python script that passed 4 rounds of community review is the reference implementation here.

## Getting Started

### For Claude Code users
Install ECC with the `workflow-quality` module — delivery-gate auto-registers as a Stop hook, growth-log is available immediately. Zero configuration.

### For everyone else
The ideas are tool-agnostic:
1. Create a directory for learning entries (e.g., `~/notes/learning/`)
2. After complex work, write one entry following the template in [growth-log-methodology.md](growth-log-methodology.md)
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
