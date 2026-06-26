# 11 — A day in the workflow

The earlier chapters are habits in isolation. This one strings them into a single
worked example: one realistic task, start to finish, the way it actually runs.
It's also the answer to "why do you do all this every day?" — each step earns its
place by killing a specific failure.

## The loop

```
fresh session  →  graph the area  →  understand + brainstorm  →  worktree
      →  implement (precise comments + tests)  →  verify  →  draft PR  →  human gates the push
```

Below, each arrow with the command or prompt that drives it. Substitute your own
tools where they differ — the *shape* is the point, not the specific tool.

## 1. Start fresh

New task, new conversation. A session that's already chewed through two unrelated
problems is worse at the third (chapter 01).

```
<launch your agent>           # a one-letter alias pays off — you do this all day
<resume-last>                 # only when you genuinely want the same context
```

**Why:** context is the budget you spend on quality. Starting clean is the
cheapest way to protect it.

## 2. Graph the area (keep context in a map, not in re-reads)

Before asking questions about an unfamiliar part of the codebase, build a
knowledge graph of *that area* once, then query the map instead of making the
agent re-read files every time (chapters 01 and 10).

```
# Build a graph of one service or package — scope it, don't graph the whole repo:
/graphify <path/to/service-or-package>

# Ask the map, don't grep:
/graphify query "how does <subsystem> work"
/graphify query "what calls <the thing I'm about to change>" --dfs

# Trace a connection or explain a node:
/graphify path "<ConceptA>" "<ConceptB>"
/graphify explain "<SomeComponent>"

# After you change code, refresh only what changed:
/graphify <path> --update
```

Open the generated `graph.html` to orient fast — the report's **god nodes** and
**community labels** tell a newcomer what the important pieces are in under a
minute.

**Why:** the same question that would cost thousands of tokens of file-reading
costs a fraction against a pre-built map. You read a small map, not a large
codebase, every time you reason about it.

## 3. Understand, then brainstorm with the skill

Don't design from a cold start. First map the territory (chapter 08):

```
Before we design: walk the parts of this code that touch <area>. How does it work
today, and where would a change to do <Y> reach? Don't propose anything yet.
```

(Do this *after* the graph build so it reasons over the map.)

Then run the **brainstorming skill** — a packaged design loop that asks one
question at a time, makes you choose between options, and *won't write code until
you approve a design* (chapters 03, 06):

```
I want to <build/change> X. Let's brainstorm it before any code.
```

It will: explore context → ask clarifying questions one at a time → propose **2–3
approaches with trade-offs** and a recommendation → present the design for your
approval → only then move to a plan.

Two things to do live: **push back on at least one option** (the contrast between
approaches is where the design is actually made), and treat the *no-code-until-
approved* gate as the feature it is, not a delay.

**Why:** a "build X" that immediately builds bakes a dozen unseen decisions into
code that's annoying to unwind. The loop surfaces them while they're still words.

## 4. Isolate the work in a worktree

Once you have an approved design, do the implementation in a dedicated worktree on
a fresh branch — never on the shared checkout, which a concurrent session can
switch out from under you.

```bash
git fetch origin
git worktree add .worktrees/<feature> -b <prefix>/<feature> origin/main
cd .worktrees/<feature>
# ... all edits, builds, tests happen in here ...
git worktree remove .worktrees/<feature>   # when merged or abandoned
```

Path discipline: every file the agent touches must resolve **inside** the
worktree, or edits land on the wrong branch.

**Why:** isolation means a broken experiment is one `worktree remove` away from
gone, and parallel work never clobbers a shared working tree.

## 5. Implement — precise comments and tests, together

```
Implement <thing>. Match the surrounding style. Give every function and method a
one-line comment saying what it does and the one surprising thing — no stories, no
ticket references. Extend existing comments rather than rewriting them.
```

```
Now write unit tests for the logic you added, run them, and paste the real output.
```

**Why:** code that runs but reads badly is a liability you'll pay for later.
Comments and tests are part of "implement", not a follow-up someone never does
(chapter 05).

## 6. Verify — make it check itself, then check it yourself

```
Double-check every claim you just made, and give me a table of what you could and
couldn't verify.
```

Then the build must actually be green — and you must see it, not be told it:

```bash
<build>      # compiles
<lint/vet>   # clean
<format>     # no diff
<test>       # the relevant package passes
```

**Why:** "done" is a claim until there's evidence. Two independent checks (its
self-review plus your green build) catch what one misses (chapter 00, principle 4).

## 7. Draft PR — agent does the plumbing, human gates the push

```
Open a draft PR. Description = plain prose: what changed and why, the one or two
things to look at closely, and a real pasted test/build output. No ## What / ## How
scaffolding, no emoji headers.
```

Then **you** review the diff in the UI and mark it ready. Allow `git pull`
automatically; keep `git push` behind a prompt.

**Why:** the description is the first thing a reviewer reads and the place agent
output most gives itself away — so it gets a human. And push changes shared state,
which is the one action that should never be fully automatic (chapters 02, 04).

## The whole day, in one breath

Fresh session, graph the area, understand and brainstorm to an approved design,
isolate in a worktree, implement with precise comments and tests, verify twice,
open a draft PR, and gate the push. Every step is one of the five principles made
into a command. Once it's muscle memory it isn't slower — it's the thing that
keeps the agent producing code you'd actually sign your name to.
