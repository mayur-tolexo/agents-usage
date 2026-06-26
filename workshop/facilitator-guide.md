# Facilitator guide

The run-sheet. Each module has the same four parts:

- **Say** — the talking points. Don't read them; make them yours.
- **Show** — a live demo script. Rehearse it on your own repo beforehand.
- **Do** — the exercise attendees run on their own repo (full cards in
  `exercises.md`).
- **Debrief** — the question that turns the exercise into a lesson. This is the
  part that sticks; protect time for it.

Times are targets. When you run long, cut an exercise short — never the debrief.

---

## Module 0 — Intro and the five principles · 15m

**Say.**
- The quality you get from a coding agent is mostly about *how you drive it*, not
  the model. Today is about habits, not features.
- Lay out the five principles (from `00-principles.md`), one line each:
  1. Context is like milk — fresh and condensed beats large and stale.
  2. Work in small steps.
  3. Don't jump straight to code — understand and design first.
  4. Verify everything, in more than one way.
  5. Keep the risky actions behind a human.
- Frame the day: "Every module today is one of these five, made concrete. By the
  end you'll have done each one on your own repo."

**Show.** Nothing yet — just set the frame. Optionally, show the repo's chapter
list so people know where to read more.

**Do.** A 60-second warm-up, around the room: "What's one thing that's frustrated
you about using a coding agent?" Jot the answers where everyone can see. You'll
revisit them at the end — most will map to one of the five principles.

**Debrief.** "Hold onto your frustration — let's see if today's habits address
it."

---

## Module 1 — Context hygiene · 25m

**Say.**
- The single biggest lever is keeping context small and fresh. A long session
  that's wandered through three problems is worse at the fourth.
- Three moves: fresh session per topic; two-pass for hard changes (one session
  finds the files, a fresh one edits them); hand off to a `HANDOFF.md` instead of
  hoping an auto-summary keeps the right things.

**Show** (≈6m). On your repo:
1. Start a session and ask a broad question that makes it read several files
   ("how does X work end to end?"). Point out how much it pulled in.
2. Start a **fresh** session. Ask only: "Which files would I edit to change Y?
   Don't edit anything — just list them and why." Show how little context that
   took and how sharp the answer is.
3. Mention the handoff move: "When a long task fills up, I ask for a HANDOFF.md
   and start fresh with just that file." Show the one-line prompt from the
   playbook.

**Do** (≈12m). Exercise 1 (`exercises.md`): the two-pass change. In a fresh
session, have them ask *only* "which files do I need to change to do `<small
thing>`?" — no edits. Then start a second fresh session, give it just those
files, and make the change.

**Debrief** (≈5m). "How did the two-pass change feel versus how you normally
do it? What did the second session *not* have to wade through?" Draw out: the
edit session never saw the exploration, so it stayed sharp.

---

## Module 2 — Understand, brainstorm, design · 30m

**Say.**
- The habit that most separates good output from bad: design *with* the agent,
  in a loop, before any code. Saying "build X" and letting it immediately build
  bakes a dozen unseen decisions into code that's annoying to unwind.
- Two layers: first *understand* (map the code, name the real problem, list the
  use-cases — `08`), then *design in a loop* (ask one question at a time, demand
  2–3 options with trade-offs, refine in passes, agree before building — `06`).

**Show** (≈8m). Pick a small feature you might add to your repo. On screen:
1. Prompt: "Before any code: ask me what you need to know, one question at a
   time, until you understand the goal and constraints." Answer a couple live.
2. Prompt: "Give me two or three ways to do this with trade-offs, and which you'd
   pick and why." Read the contrast aloud — that's where the thinking is.
3. Stop before code. Make the point: "We just caught design decisions while they
   were still words."

**Do** (≈15m). Exercise 2: run the loop on a real (small) feature or change in
their own repo. Rule: **they are not allowed to let it write code.** The
deliverable is a short agreed design — the options it offered, the one they
chose, and why.

**Debrief** (≈7m). "What did the agent assume that you had to correct? What
decision surfaced that you'd otherwise have found in code?" The answers are the
whole point — those corrections are bugs caught for free.

---

## Break · 10m

Protect it. Come back on time.

---

## Module 3 — Guardrails: permissions and a hook · 25m

**Say.**
- Draw the line between reversible (let the agent do it) and not-reversible (put
  a human in front). You encode that line once, in the repo, so you stop relying
  on memory or vigilance.
- Permissions answer "may this tool run?" (allow / ask / deny). Hooks run *your*
  check at a moment and can block on logic the model can't be trusted to
  remember.

**Show** (≈8m). On your practice repo:
1. Show a project `settings.json` with the "PR-review-only" recipe from `02` —
   allow read + `gh pr` reads, deny edits/commit/push/create.
2. Ask the agent to make an edit or commit. Show it get **blocked**. This is the
   moment that lands — a wall, not a polite request.
3. Briefly show the idea of a commit-blocking hook ("reject `git commit` on
   `main`"). You don't have to build it live; describe what the hook checks and
   why a hook (harness-enforced) beats a memory note (model-remembered).

**Do** (≈12m). Exercise 3: in their practice repo, add a project-local `deny`
rule for `git push` (and optionally edits), then *try* to make the agent push and
confirm it's blocked. Stretch goal for the fast finishers: sketch a hook that
blocks commits to `main`.

**Debrief** (≈5m). "Where's the line between allow / ask / deny for *your*
team's repos? What belongs on each?" Get them to name 2–3 concrete rules they'll
actually add. Reinforce: a `deny` rule is a wall; an instruction is a request.

> **Facilitator caution.** Make sure everyone is editing **project-local**
> settings in their practice repo, not their global config. Have them double-check
> the path before saving.

---

## Module 4 — Clean code and self-verification · 25m

**Say.**
- Agents produce code that runs but reads badly: no comments, or comments that
  narrate the obvious, or a function doing five things. You get clean code by
  asking for it and by encoding the standard (`05`).
- The standard: new code matches the surrounding style; every function/method
  gets a short, *self-contained* comment (no tickets, no stories); the logic is
  tested; the build is green before "done."
- Verification is a habit with teeth: have it write tests and *run them*; and
  make it check its own claims.

**Show** (≈6m). On your repo:
1. Have the agent write or refactor a small function. Point at the comment — is
   it precise and self-contained, or noise? Coach it: "one line, say what it does
   and the one surprising thing, no story."
2. Run the self-check prompt on something it claimed: "double-check every claim
   you just made and give me a table of what you could and couldn't verify."
   Show the table; note how often something downgrades from "done" to "actually,
   not sure."

**Do** (≈13m). Exercise 4: pick a messy or under-commented function in their
repo. Have the agent (a) add precise self-contained comments matching the house
style, (b) write a unit test for it, (c) **run** the test and paste the real
output. Then run the self-check prompt and read the verification table.

**Debrief** (≈6m). "Did the self-check catch anything? What did a *good* comment
here look like versus a useless one?" Land it: "done" means tests ran green and
you saw the output — not the agent saying "done."

---

## Module 5 — A clean draft PR · 20m

**Say.**
- Let the agent do the git/`gh` plumbing; keep the *description* and the *push*
  with a human. The description is where agent output gives itself away and where
  it matters most — a reviewer reads it first.
- Avoid the tells: `## What / ## How` scaffolding, emoji headers, "improved X and
  enhanced Y" filler. Aim for plain prose: what changed and why, the one or two
  things to look at, and **real pasted evidence** (the actual test run).

**Show** (≈6m). On your repo, take a small change and:
1. Have the agent open a **draft** PR with a hand-written description.
2. Read it together against the "good description" example in `04`. If it
   produced scaffolding, coach it into prose live — that contrast teaches fast.
3. Show the draft in the review UI: "nothing's ready until *I* mark it ready."

**Do** (≈10m). Exercise 5: from a small branch in their repo, have the agent open
a draft PR with a hand-written description that includes a real pasted test/build
output. They review it like a colleague's and note anything that reads
machine-generated.

**Debrief** (≈4m). "What in the description read human, and what read generated?
What would you change before marking it ready?" Reinforce: allow pull, gate push;
draft PRs are a verification tool, not a formality.

---

## Module 6 — Plugins, and wrap-up · 20m

**Say** (≈8m).
- You can extend the agent with skills/plugins, MCP servers, and CLI tools (`10`).
  Used well they remove whole frictions — stale docs, manual browser checks,
  re-explaining your workflow, reading half a repo to answer one question.
- Two costs you never skip: **trust/access** (these run code and see your data —
  vet them like a privileged dependency) and **context cost** (every connected
  tool taxes every session — keep the set lean).
- Walk the shortlist briefly: a workflow-discipline skill library, a codebase
  knowledge-graph tool, up-to-date library docs, a browser verifier, a token
  meter, a status line. Adopt for a concrete recurring pain, not for novelty.

**Show** (≈4m, optional). If you have one wired up, do a 60-second demo of the
single most useful extension for *your* team — e.g. ask a codebase-graph tool a
question it answers from a small map instead of reading many files, or show
up-to-date docs being pulled in. Keep it short; this module is the first thing to
cut if you're over time.

**Wrap-up** (≈8m).
- Revisit the frustrations from Module 0. Map each to a habit from today.
- Go around: **each person names one habit they'll adopt this week.** Concrete,
  not "use it better." ("Two-pass for big changes." "Add a no-push deny rule to
  my repo." "Always run the self-check prompt.")
- Share the handout. Point them at the chapters the workshop didn't drill —
  `03` (memory/skills deeper), `07` (evaluating open source) — as follow-up.

**Debrief / close.** "The five principles are the whole thing. Everything today
was one of them made concrete. Pick the habits that fix *your* frustration and
build those first."

---

## If you're running short on time

Cut in this order, and don't apologize for it:
1. Module 6's live demo (keep the talking points and wrap-up).
2. Module 3's hook stretch goal.
3. Shorten Module 1's exercise to just the first pass.

Never cut: the design loop (Module 2) or any debrief. Those are where the
learning is.
