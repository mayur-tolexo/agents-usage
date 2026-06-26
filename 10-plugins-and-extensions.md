# 10 — Plugins and extensions

You can extend a coding agent well beyond its built-in tools. Used well, the right
extensions remove whole categories of friction — stale library docs, manual
browser checking, re-explaining your workflow every session, reading half a
codebase to answer one question. Used carelessly, they add noise, latency, and —
for anything that runs code or sees your data — real risk. This chapter is how to
choose, and a starter shortlist.

## Three kinds of extension

| Kind | What it is | Examples |
|------|-----------|----------|
| **Skills / plugins** | Packaged workflows and instructions the agent loads (chapter 03) | a brainstorming workflow, a TDD loop, a house code-review |
| **MCP servers** | External services the agent talks to over a standard protocol; they add *tools* (fetch a doc, drive a browser, query a DB) | docs lookup, browser automation, database access |
| **CLI tools** | Plain command-line programs the agent runs via the shell | a code-graph builder, a token-usage meter |

They're not exclusive — a code-graph tool can be both a CLI and an MCP server, for
instance. What matters is what it *gives* you and what it *costs* you.

## How to find them

- Curated lists. Search for "awesome" lists for your agent and for MCP servers —
  they're the fastest survey of what exists and what's actively used.
- The plugin marketplace / registry your agent ships with, if it has one.
- The communities around the tool. Word-of-mouth surfaces the ones people
  actually keep using, which is a better signal than star count.

## How to vet one — the same rubric as chapter 07, plus security

Run every candidate through the open-source rubric (fit, maintenance, adoption,
license, dependencies, surface, exit cost). Extensions add **two more criteria**
you cannot skip:

- **Trust and access.** An MCP server or plugin can run code on your machine and
  see whatever you point it at — your files, your tokens, your codebase. Treat
  installing one like adding a dependency *with privileges*. Prefer well-known,
  open, actively-maintained sources; read what it asks for; give it the narrowest
  access that does the job. Be especially wary of anything that wants secrets or
  broad filesystem/network reach.
- **Context cost.** Every connected tool advertises itself into the agent's
  context. Ten MCP servers you rarely use is ten standing taxes on every session
  (chapter 01). Connect what you use; disconnect the rest. More is not better.

## A starter shortlist

These are widely-used, genuinely-useful candidates as of writing. Treat this as a
*starting point for your own evaluation*, not a verified endorsement — run each
through the rubric above and check its current state before you adopt it (that's
the chapter 07 discipline, and it applies to this list too).

### Workflow discipline
- **Superpowers** (`github.com/obra/Superpowers`) — a library of disciplined
  skills: brainstorm-before-build, test-driven development, systematic debugging,
  writing and executing plans, code review. If your team struggles with
  *process* — jumping to code, skipping verification — this encodes the habits
  this whole guide preaches. High value for a team standardizing on a workflow.

### Understanding a codebase / context reduction
- **graphify** (`github.com/safishamsi/graphify`) — builds a queryable knowledge
  graph of a codebase (and docs). You ask questions against a compact map instead
  of making the agent read many files, which both speeds answers and cuts context
  use sharply on large repos. Pairs directly with chapters 01 and 08.
- **Serena** — semantic code navigation and editing through language servers, so
  the agent works at the level of symbols (find this function's callers, rename
  this) rather than raw text search. Useful on large, strongly-typed codebases.

### Current, correct library docs
- **Context7** — injects up-to-date documentation for libraries and frameworks on
  demand, so the agent stops coding against an API it half-remembers from
  training. One of the highest-value MCP servers for day-to-day coding.

### Verification
- **Playwright (browser) integration** — lets the agent drive a real browser to
  confirm a web change works, instead of asserting that it does (chapter 00,
  principle 4; chapter 09). If you build anything with a UI, this closes the
  verification loop.

### Cost and visibility
- **A token-usage meter** (e.g. `ccusage`) — reads your local logs and reports how
  many tokens and how much spend each session is costing. Useful for noticing
  which habits are expensive, and for keeping the "small context" discipline
  honest.
- **A configurable status line** — shows model, branch, uncommitted files, sync
  state, and context usage at a glance (chapter 09). Cheap to set up, paid back
  every session.

## How to wire them up (briefly)

- **Skills / plugins** install into your agent's skills or plugins directory;
  scope them to a project or to your user profile depending on whether the whole
  team should get them.
- **MCP servers** are configured in your settings as a command or URL the agent
  connects to. Keep the list short and project-relevant; disconnect what you
  don't use.
- **CLI tools** just need to be on your PATH and (usually) allowed in permissions
  (chapter 02) so the agent can run them without a prompt each time.

## The rule for adopting extensions

Adopt for a concrete, recurring pain — "I keep coding against stale docs", "I
keep reading half the repo to answer one question", "the team keeps skipping
design". Match the tool to the pain, vet it (rubric + trust + context cost), try
it small, and keep the standing set lean. An extension you connected once and
forgot is pure cost; an extension that removes a daily friction pays for itself
every session.
