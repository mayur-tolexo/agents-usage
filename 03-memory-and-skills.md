# 03 — Memory and skills

Permissions (chapter 02) decide what the agent *may* do. Memory and skills shape
what it *will* do — the conventions it follows and the workflows it runs — so you
stop repeating yourself.

## Memory: write the rule down once

A memory file is project context the agent loads automatically. The repo-level
one is `CLAUDE.md` at the root (some setups also keep a per-user memory). Anything
that's a standing rule for the project belongs there, for example:

- "All code changes go on a branch, never directly on `main`."
- "Every function gets a one-line doc comment; see chapter 05."
- "PR descriptions are hand-written prose — no `## What / ## How` scaffolding."
- "Don't commit design or spec docs into the repo; keep them local."
- "Don't add an AI co-author trailer to commits."

Good memory entries share three traits:

1. **They state a rule, not a story.** "Use tabs" — not "we once had a tabs-vs-
   spaces argument."
2. **They're things the code can't already tell the agent.** Don't write down the
   directory layout; the agent can see it. Write down the *non-obvious* decision.
3. **They're short.** Memory is loaded every session and competes for context.
   One fact per line.

If you find yourself giving the same correction twice, that's the signal to add a
memory entry instead of correcting a third time.

### Memory vs. an automated behavior

Memory is *guidance the model reads*. It is not a guarantee. If you need
something to happen **every single time** — "always run the linter before a
commit", "always block writes to `dist/`" — that's a hook (chapter 02), because
the harness enforces a hook and only suggests a memory. Rule of thumb: a
*preference* is memory; a *guarantee* is a hook.

## Skills: package a workflow

A skill is a named, reusable workflow the agent can invoke — a set of
instructions (and sometimes scripts) for doing one kind of task the right way.
Instead of re-explaining "here's how we write a commit message" or "here's our
debugging process" each time, you write it once as a skill and the agent loads it
on demand.

Skills are good for anything you do repeatedly with a defined method:

- A commit-message convention.
- A code-review checklist.
- A "before you call it done" verification routine.
- A house style for comments or PRs.
- A multi-step process like brainstorm → design → plan → build.

### Anatomy of a skill

A skill is a folder with an instruction file (commonly `SKILL.md`) that has a
short description of *when to use it* and the steps to follow. The description is
what lets the agent decide the skill applies. Keep skills focused — one workflow
per skill — and keep the steps concrete enough that following them produces the
same result every time.

### Skills for restrictive actions

This is the pattern behind much of this guide: combine a skill with a hook to
both *teach* and *enforce* a restriction.

- A **skill** explains the disciplined way ("work in a worktree, branch off the
  default branch, never push without approval").
- A **hook** makes the unsafe shortcut impossible ("reject `git commit` on
  `main`").

The skill makes the agent *want* to do the right thing; the hook makes sure it
*can't* do the wrong thing even if it forgets. Use them together for anything
that matters: branch discipline, no-direct-push, no-secrets-in-commits.

## Where the three layers fit together

| Layer | Answers | Strength |
|-------|---------|----------|
| Permissions | "May this tool run at all?" | Hard wall |
| Hooks | "Run my check at this moment and act on it" | Hard, with logic |
| Memory | "What are this project's conventions?" | Guidance, every session |
| Skills | "How do we do this kind of task?" | Guidance, on demand |

Start every team repo by setting these up. It's a few minutes of work that pays
back every session afterward, because the rules stop living in your head and
start living in the project.
