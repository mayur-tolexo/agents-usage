# agents-usage

A practical guide to using Claude Code (and coding agents in general) the way a
disciplined team uses them: prepare before you generate, keep context small,
guard the dangerous actions, and verify everything.

This is not a feature tour. It is a set of working habits. Most of the quality
you get out of a coding agent comes from how you set it up and how you drive it,
not from the model. The chapters below are the habits, one topic each.

## How to read this

If you're new, read `00-principles.md` first, then `09-claude-code-playbook.md`.
Those two give you the mindset and the daily moves. Everything else you can read
on demand when you hit that topic.

If you're setting up a repo for a team, start with `02-permissions-guardrails.md`
and `03-memory-and-skills.md` — that's where you encode the rules so the agent
follows them without being reminded.

## Chapters

| # | File | What it covers |
|---|------|----------------|
| — | `00-principles.md` | The core mindset: small context, prep before code, verify everything |
| 1 | `01-tools-and-context.md` | The tools an agent uses, and how to keep its context small |
| 2 | `02-permissions-guardrails.md` | Permissions and hooks — e.g. "allow PR review only" |
| 3 | `03-memory-and-skills.md` | Memory files and custom skills to encode and enforce rules |
| 4 | `04-pull-requests.md` | Opening a PR with a real, hand-written description |
| 5 | `05-clean-code-and-comments.md` | Precise comments, tests, and a green build before "done" |
| 6 | `06-brainstorming-and-design-loops.md` | Brainstorm, propose options, iterate, then build |
| 7 | `07-evaluating-open-source.md` | Find alternatives, compare on a rubric, verify, adopt |
| 8 | `08-understand-before-design.md` | Understand the real problem and use-cases before designing |
| 9 | `09-claude-code-playbook.md` | The daily tips, condensed |
| 10 | `10-plugins-and-extensions.md` | Plugins, skills, and MCP servers worth adopting |

## The whole thing in five lines

1. Context is like milk — fresh and condensed beats large and stale.
2. Don't jump to code. Understand, then design, then build.
3. Encode your rules once (permissions, hooks, memory, skills) so you stop repeating them.
4. Make the agent verify its own work, and verify it yourself in a second way.
5. Keep the risky actions (push, deploy, delete) behind a human.
