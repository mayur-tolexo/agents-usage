# 09 — The daily playbook

The earlier chapters are the principles. This one is the field-tested moves —
small habits that compound. None of them is clever on its own; together they're
most of what separates a smooth day from a frustrating one.

## Context

- **Fresh conversation per topic.** The single biggest lever. New problem, new
  session. (Chapter 01 covers this in depth.)
- **Two-pass for hard changes.** First session finds the files; second, fresh
  session edits them. The exploration doesn't pollute the work.
- **Hand off, don't just compact.** When context fills, ask for a `HANDOFF.md`
  capturing what was tried, what worked, what didn't — then start fresh with only
  that file. You decide what survives, not an auto-summary.

## Working the problem

- **Small steps.** Too-big tasks are where it goes wrong. Break down, then break
  down again.
- **Think before code.** Use it to understand the codebase, research, and argue
  through architecture — not just to type. The prep is where quality comes from.
- **Decompose big asks.** If a request is really four projects, say so and take
  them one at a time.

## Git and GitHub

- **Let it run git and `gh`.** Commits, branches, pulls, PRs — all good
  delegations. Skim the commit messages it writes; don't type them yourself.
- **Allow pull, gate push.** Pull is safe; push changes shared state. Auto-allow
  the first, prompt on the second. (Chapter 02 for the config.)
- **`git bisect` is a real tool here.** Give it a test script and it'll find the
  commit that broke something for you.

## Verifying its work

- **Tests, then run them.** Have it write tests; then actually run them and read
  the output.
- **Make it re-check itself.** A reliable prompt: *"double-check every claim you
  just made, and at the end give me a table of what you could and couldn't
  verify."*
- **Drive the real thing.** For a web app, use a browser integration so it
  confirms behavior instead of asserting it. For an interactive CLI, drive it in
  a terminal multiplexer, send input, capture output, check it.
- **Draft PRs.** Generate a draft, review the diff like a colleague's, then mark
  it ready yourself.

> A small browser tip if you wire one up: tell it to use the page's accessibility
> tree (element references) rather than screenshots and pixel coordinates. It's
> faster and more reliable, and only screenshot when you explicitly ask.

## Your environment

- **Status line.** Configure it to show model, directory, branch, uncommitted
  file count, sync state, and a context-usage bar. Keeping an eye on context
  usage is half of managing it.
- **Voice input.** You can talk faster than you type. A local transcription tool
  works well — the agent forgives transcription typos easily. Think of it as
  sending a voice note to a colleague.
- **A short alias.** Alias your launch command to something one or two letters;
  you'll start it dozens of times a day. Pair it with the "continue last
  conversation" and "resume a recent conversation" flags.

## Running several at once

- **Juggle, but cap it.** Three or four parallel tasks is plenty, especially at
  first. More than that and you stop tracking what each is doing.
- **A consistent layout.** Keep a fixed habit — e.g. newest task on one side,
  sweep across oldest-to-newest — so you always know where things are. The
  specific system matters less than being consistent.

## If you remember only three

1. Keep context small and fresh.
2. Understand and design before you code.
3. Verify everything — make it check itself, then check it yourself another way.

Everything else on this page is in service of those three.
