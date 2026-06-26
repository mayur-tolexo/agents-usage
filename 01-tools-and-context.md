# 01 — Tools and context

A coding agent works by calling tools: reading files, searching, editing, running
commands, spawning sub-agents. Knowing which tool fits a job — and which tool
*costs you context* — is most of driving one well.

## The tools, and when each is right

| Tool | Use it for | Watch out for |
|------|-----------|---------------|
| **Read** | Looking at a specific file or range you already know you need | Reading whole large files when you need 20 lines — pass a range |
| **Grep / search** | Finding where a symbol, string, or pattern lives | Broad patterns that match thousands of lines |
| **Edit** | A precise change to a file you've read | Editing a file you haven't read — it'll usually refuse anyway |
| **Write** | Creating a new file or fully replacing one | Overwriting something you didn't look at first |
| **Bash / shell** | Running builds, tests, git, CLIs | `cat`/`head`/`sed` to read files — use Read instead; it's cleaner |
| **Sub-agent / task** | Fan-out work whose *details* you don't need to keep | Using one for a single known lookup — just do it inline |
| **Skill** | Invoking a packaged workflow (see chapter 03) | Guessing a skill name that doesn't exist |

The general rule: prefer the dedicated tool over a shell command that does the
same thing. `Read` beats `cat`, `Grep` beats `grep | head`. The dedicated tools
give the agent cleaner, more structured results and keep your context tidier.

## The thing that actually matters: keep context small

Every file the agent reads, every command's output, every long reply — all of it
sits in the conversation and degrades later answers. Managing that is a skill.

### Move 1 — fresh sessions per topic
The single easiest win. New problem, new conversation. Don't let one session
accumulate five unrelated investigations.

### Move 2 — scout, then edit (two passes)
Big or unfamiliar change? First conversation: "Which files do I need to change to
do X? Don't edit anything, just tell me the files and why." Second, fresh
conversation: give it just those files and make the change. The expensive
exploration doesn't pollute the session that does the work.

### Move 3 — delegate the reading
When answering means sweeping many files but you only need the conclusion, send a
sub-agent. It reads in its own context and hands you back the answer, not the
file dumps. Your main context stays clean. (This is also how tools like a code
knowledge graph help — see chapter 10 — they pre-digest the codebase so you read
a small map instead of many files.)

### Move 4 — hand off before you run out
When a long task is eating context, don't `/compact` and hope. Ask for a handoff:

> "Write the rest of the plan to HANDOFF.md — what you tried, what worked, what
> didn't — so a fresh session can load only that file and finish the task."

Then start fresh and give it just that path. A deliberate handoff beats an
automatic summary because *you* decide what survives.

### Move 5 — condense what you paste
Don't paste a 500-line log when the error is 8 lines. Don't paste a whole file
when a function is the subject. You're not saving the agent effort by giving it
more — you're spending your budget for nothing.

## A quick mental model

Think of the context window as a desk. A clean desk with the three papers you
need is a productive desk. A desk buried under everything you've touched today is
not — even though "more information" is technically on it. Your job as the driver
is to keep the desk clear.
