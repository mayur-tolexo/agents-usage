# 12 — Claude Code: the concrete levers

The earlier chapters are principles that hold for any coding agent. This one is
the specific Claude Code commands and features that put those principles into
practice. It tracks the official best-practices guide
(`code.claude.com/docs/en/best-practices`) — read that too; this is the condensed,
cross-referenced version.

Everything below maps back to one idea from the docs: **context fills fast and
performance degrades as it fills.** Most of these levers exist to manage that.

## Explore → plan → implement → commit (plan mode)

The four-phase workflow, and the chapter-06 design loop made concrete:

1. **Explore** — enter **plan mode**; the agent reads and answers without editing.
   "Read `/src/auth` and explain how sessions and login work."
2. **Plan** — "What needs to change to add X? Make a plan." Press **`Ctrl+G`** to
   open the plan in your editor and tighten it before anything runs.
3. **Implement** — leave plan mode; "implement the plan, write tests, run the
   suite, fix failures."
4. **Commit** — "commit with a descriptive message and open a PR."

Skip the plan for one-sentence diffs (a typo, a log line, a rename). Use it when
the approach is uncertain, the change spans files, or the code is unfamiliar.

## Let it interview you → SPEC.md → fresh session

A sharp version of the design loop for larger features:

```
I want to build <X>. Interview me in detail using the AskUserQuestion tool.
Ask about implementation, UX, edge cases, and trade-offs — dig into the hard
parts I might not have considered. Keep going until we've covered everything,
then write a complete spec to SPEC.md.
```

Then **start a fresh session** to implement from `SPEC.md` — clean context, a
written spec to reference. The best specs name the files and interfaces, state
what's out of scope, and end with an end-to-end verification step.

## Give it a check it can run (verification)

The agent stops when work "looks done"; a runnable check turns that into a real
pass/fail it iterates against (chapter 00, principle 4). Make the check explicit
in the prompt — example test cases, a build to pass, a screenshot to diff. Then
choose how hard it gates:

- **In one prompt** — "run the tests and fix failures" (works today, any task).
- **Across a session** — set it as a `/goal` condition; an evaluator re-checks
  after every turn until it holds.
- **Deterministically** — a **Stop hook** runs your check as a script and blocks
  the turn from ending until it passes.
- **Second opinion** — a fresh-context review subagent (below).

Always have it **show evidence** — the command and its output — not just assert
success.

## Provide rich, specific context

- **`@path/to/file`** — reference a file; the agent reads it before responding.
- **Paste or drag images** — screenshots, designs, diagrams.
- **Pipe data in** — `cat error.log | claude` sends contents directly.
- **Give URLs** for docs; allowlist frequent domains with `/permissions`.
- Be specific: name the file, the scenario, the constraint. "Write a test for
  `foo.py` covering the logged-out edge case, avoid mocks" beats "add tests".

## Manage the session

| Lever | What it does |
|-------|--------------|
| `/clear` | Reset context between unrelated tasks — the single most-used hygiene move |
| `Esc` | Stop mid-action, keep context, redirect |
| `Esc Esc` / `/rewind` | Checkpoint menu — restore conversation, code, or both to a previous point |
| `/compact <focus>` | Summarize history, optionally focused ("…on the API changes") |
| `/btw` | Ask a side question that never enters conversation history |
| `claude --continue` / `--resume` | Pick up a past session; `/rename` them like branches |

Rule of thumb from the docs: if you've corrected the agent **more than twice on
the same issue**, the context is polluted — `/clear` and restart with a better
prompt that folds in what you learned.

## Configure the environment once

- **`/init`** — generates a starter `CLAUDE.md` from your project. Refine over
  time. (Chapter 03 is the deeper take on memory.)
- **`CLAUDE.local.md`** — personal, gitignored project notes, separate from the
  shared `CLAUDE.md`. `@path` imports pull in other files.
- The CLAUDE.md test: for each line, *"would removing this cause a mistake?"* If
  not, cut it — a bloated file gets ignored. Emphasis (`IMPORTANT`, `YOU MUST`)
  improves adherence.
- **Permissions** — allowlist safe commands via `/permissions`; or **auto mode**
  (`claude --permission-mode auto`) lets a classifier approve routine work and
  block risky escalation; or **`/sandbox`** for OS-level isolation. (Chapter 02.)
- **Hooks** — for anything that must happen every time. "Write a hook that runs
  eslint after every edit" / "…that blocks writes to the migrations folder."
- **Skills** (`.claude/skills/`), **subagents** (`.claude/agents/`, see the
  `agents/` folder here), **plugins** (`/plugin` to browse) — chapters 03 and 10.
- **`gh` and other CLIs** — the most context-efficient way to reach external
  services. Install `gh`; the agent knows how to use it.

## Scale beyond one session

- **Headless** — `claude -p "prompt"` for CI, hooks, scripts;
  `--output-format json` / `stream-json --verbose` for parsing.
- **Fan out** — loop `claude -p` over a file list for big migrations, scoping with
  `--allowedTools "Edit,Bash(git commit *)"`. Test on 2–3 files, then run at scale.
- **Writer/Reviewer** — one session implements, a **fresh** session reviews. Fresh
  context reviews better because it isn't biased toward code it just wrote.
- **Adversarial review subagent** — before "done", have a subagent review the diff
  in fresh context against the plan: "report gaps that affect correctness or the
  stated requirements, not style." The bundled `/code-review` does this for bugs.
  Caveat: a reviewer told to find gaps will find some even when the work is sound —
  don't chase every one into over-engineering.
- **Worktrees / parallel sessions** — isolated checkouts so parallel edits don't
  collide (chapter 11).

## The named failure patterns (recognize them early)

| Pattern | Fix |
|---------|-----|
| **Kitchen-sink session** — unrelated tasks pile up | `/clear` between tasks |
| **Correcting over and over** — context full of failed tries | After two failed corrections, `/clear` and re-prompt |
| **Over-specified CLAUDE.md** — rules lost in noise | Prune ruthlessly; convert "always" rules to hooks |
| **Trust-then-verify gap** — plausible code, unhandled edges | Always give a runnable check; if you can't verify, don't ship |
| **Infinite exploration** — "investigate X" reads hundreds of files | Scope it, or delegate to a subagent |

## Develop your own intuition

These are defaults, not laws. Sometimes you *should* let context accumulate
(deep in one problem), skip the plan (exploratory task), or stay vague (you want
to see how it interprets the problem). Watch what works: when output is great,
notice the prompt, the context, the mode. When it struggles, ask whether the
context was noisy, the prompt vague, or the task too big. That intuition is the
real skill — this guide just gives you the starting points.
