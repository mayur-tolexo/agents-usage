# Persona agents

Ready-to-copy custom sub-agent definitions. Each file defines one agent with a
clear job, a restricted toolset, and a persona that bakes in the habits from this
guide — so you can hand a focused task to a focused agent instead of one
do-everything session.

| File | Persona | Use it for |
|------|---------|-----------|
| `code-reviewer.md` | Skeptical reviewer (read-only) | Reviewing a diff/PR for bugs and clean-code issues before merge |
| `brainstormer.md` | Design partner (no code) | Exploring options and trade-offs before building |
| `rfc-writer.md` | RFC author | Turning an agreed design into a precise written doc |
| `coder.md` | Disciplined implementer | Building a well-defined change with comments, tests, and a green build |

They're designed to hand off to each other: **brainstormer** → **rfc-writer** →
**coder** → **code-reviewer** is a natural pipeline from idea to merged change.

## How an agent definition works

Each file is Markdown with a frontmatter block and a system prompt:

```markdown
---
name: code-reviewer            # the id you invoke it by
description: When to use this  # how the main agent decides to delegate to it
tools: Read, Grep, Glob, Bash  # which tools it may use (omit = all tools)
model: sonnet                  # sonnet | opus | haiku | inherit (optional)
---

The system prompt — the agent's persona and rules.
```

The **description** is what lets your main session pick the right agent
automatically, so keep it action-oriented ("Use to…"). The **tools** line is a
real guardrail: the read-only agents here omit `Edit`/`Write` so they *can't*
change code, only inspect it.

## Install

**Per project** (shared with anyone who clones the repo):

```bash
mkdir -p .claude/agents
cp path/to/agents-usage/agents/*.md .claude/agents/
```

**For yourself across all projects:**

```bash
mkdir -p ~/.claude/agents
cp path/to/agents-usage/agents/*.md ~/.claude/agents/
```

Then invoke them by name when you delegate a task, or let the main session route
to them based on their descriptions. Restart your session after adding new agent
files so they're picked up.

## Adapt them

These are templates — tune them to your stack:

- Swap `model:` to match how heavy each job is (a quick review can run on a smaller
  model than a deep design exploration).
- Tighten `tools:` further if you want — e.g. drop `Bash` from the reviewer and
  rely on a pre-fetched diff.
- Add stack-specific rules to the prompt (your build/test/lint commands, your
  comment and naming conventions, your branch rules).

## A note on the reviewer and isolation

`code-reviewer` is read-only by toolset, but a sub-agent that can run `git` shares
your working tree and could in principle switch branches. For real safety when you
run review agents — especially several at once — run them with read-only
permissions or against an isolated checkout, so a review can never disturb the work
it's reviewing.
