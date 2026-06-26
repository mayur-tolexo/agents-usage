# 00 — Principles

Five ideas sit underneath everything else in this guide. If you only remember
these, you'll already be ahead of most people using a coding agent.

## 1. Context is like milk: best fresh and condensed

The more you put in front of the model, the worse it does. A long conversation
that has wandered through three unrelated problems is worse at the fourth than a
clean one would be. So:

- Start a fresh conversation whenever you switch topics.
- Don't paste a whole file when the relevant part is twenty lines.
- A two-pass move works well: in the first conversation, find *which* files you
  need to touch. In a second, fresh conversation, work out *how* to change them.

Treat context as a budget you're spending, not a free resource.

## 2. Work in small steps

Agents are good at long tasks but not perfect, and a task that's too big is where
they go wrong — they lose the thread, make a change that breaks an earlier one,
or quietly drop a requirement. Break the problem down. If a step is still too big
to do in one shot, break it down again. Small steps are easier to verify, easier
to undo, and easier for the agent to hold in its head.

## 3. Don't jump straight to code

Coding agents get a bad reputation for low-quality code, mostly because people
only ever ask them to write code. They are just as good — often more useful — at
*understanding* a codebase, researching options, talking through architecture,
and pressure-testing a design. The teams that get clean code out of an agent are
the ones that do the thinking first. Code is the last step, not the first.

## 4. Verify everything, in more than one way

Never take "done" at face value. Verification is a habit with several tools:

- Have the agent write tests, then run them and read the output.
- Ask it to re-check its own work: "double-check every claim you just made and
  give me a table of what you could and couldn't verify."
- For anything user-facing, drive the real thing (a browser, the CLI) and watch
  it behave, rather than trusting a description.
- Look at the diff yourself before it ships.

If you didn't see evidence, it isn't verified.

## 5. Keep the risky actions behind a human

Some actions are cheap to undo (a local edit, a commit on a branch). Some are
not (a force-push, a deploy, a delete, sending something to an external service).
Let the agent do the cheap-to-undo things freely, and put a human approval in
front of the expensive ones. Most of "using an agent safely" is just drawing
that line clearly — chapter 02 shows how to encode it so you don't rely on
remembering.

---

The rest of the guide is these five principles applied to specific situations.
Keep coming back to them; almost every "how do I…" question resolves into one of
the five.
