# Handout — keep this

One page to keep after the workshop. The whole guide is in the repo; this is the
distilled version you'll actually reuse.

## The five principles

1. **Context is like milk** — fresh and condensed beats large and stale.
2. **Small steps** — break it down, then break it down again.
3. **Don't jump to code** — understand, then design, then build.
4. **Verify everything** — make it check itself, then check it yourself another way.
5. **Risky actions behind a human** — push, deploy, delete are not the agent's call.

## Moves that pay off every day

- **Fresh session per topic.** New problem, new conversation.
- **Two-pass for hard changes.** One session finds the files; a fresh one edits them.
- **Hand off, don't just compact.** "Write the rest to HANDOFF.md — what you
  tried, what worked, what didn't — so a fresh session can finish from that file
  alone."
- **Allow pull, gate push.** Auto the safe thing, prompt the risky one.
- **Draft PRs** to review before anything's "ready".

## Prompts worth memorizing

**Scope before editing:**
> "Which files would I need to change to do X? Don't edit anything — just list
> them and why."

**Design before code:**
> "Before any code, ask me what you need to know, one question at a time, until
> you understand the goal and constraints."

> "Give me two or three ways to do this with trade-offs, and which you'd pick and
> why."

**Make it verify itself:**
> "Double-check every claim you just made, and give me a table of what you could
> and couldn't verify."

**Hand off:**
> "Write the rest of the plan to HANDOFF.md so a fresh session can load only that
> file and finish."

## Guardrails to set in a team repo

- A project `settings.json` that **denies** `git push` (and `commit`, and edits,
  if you want review-only) — a wall, not a request.
- A **hook** that blocks commits to `main` — harness-enforced, so it can't be
  forgotten.
- **Memory** (`CLAUDE.md`) for the standing conventions: branch first, precise
  comments, hand-written PRs, no AI co-author trailer.
- A **skill** for any workflow you repeat: commit style, review checklist,
  "before done: build + vet + test + format must be green."

## The "done" bar

New code reads like the code around it · every function has a precise,
self-contained comment · the logic is tested · the build, linter, and formatter
are green — **before** anyone says done. And you saw the evidence, not just the word.

## A good PR description

Plain prose: what changed and **why** · the one or two things to look at closely ·
**real pasted** test/build output. No `## What / ## How` scaffolding, no emoji
headers, no "improved and enhanced" filler.

## Read next

The workshop drilled context, design, guardrails, clean code, PRs, and plugins.
Still worth reading in the repo:
- `03-memory-and-skills.md` — deeper on encoding your rules
- `07-evaluating-open-source.md` — find, compare, verify, adopt
- `10-plugins-and-extensions.md` — the full extension shortlist

## Your commitment

Write down the **one habit** you said you'd adopt this week:

> ________________________________________________

Build that one first. The rest follow.
