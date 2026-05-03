# Global Claude Configuration Setup Guide

**Purpose:** Step-by-step guide to setting up the global `~/.claude/CLAUDE.md` file on this machine, so every Cowork session automatically knows Amit's working style, problem-solving approach, and output preferences.
**Audience:** Amit Rajpurkar
**Status:** Draft
**Last updated:** 2026-04-19
**Related documents:** `../README.md`, `claude-cowork-learning-plan.md`, `../config/global-CLAUDE.md`

---

## What this setup achieves

Without a global configuration, every Cowork session starts fresh. Claude has no knowledge of:

- Who you are and what your role is
- How you want tasks approached (iterative drafts, explicit plans before execution)
- Your problem-solving stages (boundary → evidence → problem statement → decomposition → solution → ADR → documentation)
- Your output preferences (markdown primary, self-documenting naming, commit-ready artifacts)
- What you want Claude to avoid (assumptions, monolithic output, skipping the plan step)

After this setup, every session starts with that context already loaded. You never have to re-explain it.

---

## How CLAUDE.md files work

Claude reads `CLAUDE.md` files at the start of every session by walking up the directory tree from your working directory. The most important file for personal global configuration is:

```
~/.claude/CLAUDE.md
```

This file applies to every project on your machine. It is loaded in full at the start of every session before any conversation begins.

**Key properties:**
- Written in plain markdown
- Loaded as context, not enforced configuration — Claude reads it and applies it, but it is not a hard technical constraint
- The more specific and concise the instructions, the more consistently Claude follows them
- Target under 200 lines — longer files reduce adherence

---

## Setup steps

### Step 1 — Check if the directory exists

Open Terminal and run:

```bash
ls ~/.claude/
```

If the directory does not exist, create it:

```bash
mkdir -p ~/.claude
```

---

### Step 2 — Check for an existing CLAUDE.md

```bash
cat ~/.claude/CLAUDE.md
```

If a file already exists, review its contents before overwriting. You may want to merge rather than replace.

---

### Step 3 — Install the global configuration file

The ready-to-install configuration file is at:

```
selflearn_cowork/config/global-CLAUDE.md
```

Copy it to the correct location:

```bash
cp /Users/amitrajpurkar/workspace/claude_workspace/selflearn_cowork/config/global-CLAUDE.md ~/.claude/CLAUDE.md
```

Verify it was installed:

```bash
cat ~/.claude/CLAUDE.md
```

---

### Step 4 — Verify Claude reads it in a new session

Open a new Cowork session and ask:

```
What do you know about my working style and output preferences?
```

Expected response: Claude should correctly describe your iterative working style, preference for explicit plans before execution, markdown as primary output format, naming conventions, and the problem-solving stages — without you having explained any of it.

If Claude does not reference the configuration, check:
- The file is at the correct path: `~/.claude/CLAUDE.md` (not `~/.claude/claude.md` — case matters on macOS)
- The file is not empty
- You opened a genuinely new session (not a continuation of an existing one)

---

## Optional: Setting up a user-level rules directory

For more granular control, you can organise personal rules into topic files under `~/.claude/rules/`. Each file covers one topic and is loaded every session.

Example structure:

```
~/.claude/
├── CLAUDE.md                 ← main global configuration (installed above)
└── rules/
    ├── architecture-standards.md   ← TOGAF, DDD, C4 usage rules
    └── adr-conventions.md          ← when and how to write ADRs
```

To set this up:

```bash
mkdir -p ~/.claude/rules
```

Then create individual rule files as needed. Keep each file focused on one topic.

---

## Optional: Project-level configuration

For a specific project (e.g., a client engagement or a particular codebase), you can add a `CLAUDE.md` at the project root. This file applies to anyone working in that project via version control.

For personal, project-specific preferences that should not be committed, use `CLAUDE.local.md` at the project root and add it to `.gitignore`.

For this `selflearn_cowork` project, a project-level `CLAUDE.md` is appropriate if you want Claude to always update the progress tracker when completing a module.

Create it at:

```
selflearn_cowork/.claude/CLAUDE.md
```

With content such as:

```markdown
# selflearn_cowork project instructions

When completing any learning module:
1. Update tracking/learning-progress-tracker.md with the module status and a brief note
2. Identify and state the next module to tackle

Always follow the naming and output standards from the global CLAUDE.md.
```

---

## Maintaining your configuration over time

Your `~/.claude/CLAUDE.md` should evolve as you discover new preferences:

- When Claude makes the same mistake twice → add a rule
- When you find yourself typing the same correction across sessions → add a rule
- When a section becomes outdated → remove it

Review your global CLAUDE.md periodically and keep it under 200 lines. If it grows larger, move topic-specific sections to `~/.claude/rules/` files.

---

## How auto memory complements CLAUDE.md

Auto memory is a separate system where Claude saves notes for itself based on what it observes during your sessions.

- Storage location: `~/.claude/projects/<project>/memory/MEMORY.md`
- Loaded automatically at the start of every session for that project
- Contains project-specific learnings, not general preferences

**The relationship between the two:**

| System | Who writes it | Scope | What it captures |
|---|---|---|---|
| `~/.claude/CLAUDE.md` | You | All projects | Personality, style, standing rules |
| Auto memory | Claude | Per project | Project-specific learnings, corrections |

Both are loaded at session start. They are complementary. Your CLAUDE.md sets the baseline; auto memory adds project-specific refinements on top.

---

## Open questions

- [ ] Does Cowork (desktop app) read `~/.claude/CLAUDE.md` the same way Claude Code CLI does? — verify by testing after installation
- [ ] Is there a way to view which CLAUDE.md files were loaded in a given Cowork session? — in Claude Code CLI this is the `/memory` command; confirm if available in Cowork desktop
