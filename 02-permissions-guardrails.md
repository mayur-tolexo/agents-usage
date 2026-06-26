# 02 — Permissions and guardrails

The agent should be free to do the cheap, reversible things and blocked from the
expensive, hard-to-undo ones — without you having to watch every step. You get
that by configuring permissions and hooks once, in the repo, so the rules travel
with the project.

Settings live in `settings.json` (checked into the repo, shared with the team)
and `settings.local.json` (your machine, gitignored). Project settings sit under
`.claude/` in the repo root.

## Allow / ask / deny

Permissions match tool calls by pattern and put each into one of three buckets:

- **allow** — runs without prompting
- **ask** — prompts you each time
- **deny** — never runs

A pattern looks like `Bash(git push:*)` or `Read(./src/**)`. Deny wins over
allow, so you can allow broadly and carve out the dangerous cases.

## Recipe: "allow PR review only"

Say you want the agent to be able to *review* pull requests and read code, but
not change anything, commit, push, or open PRs itself. Encode exactly that:

```jsonc
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Read(./**)",
      "Bash(gh pr view:*)",
      "Bash(gh pr diff:*)",
      "Bash(gh pr list:*)",
      "Bash(gh pr checks:*)",
      "Bash(gh api repos/:*)",
      "Bash(git log:*)",
      "Bash(git diff:*)",
      "Bash(git show:*)"
    ],
    "deny": [
      "Edit(./**)",
      "Write(./**)",
      "Bash(git commit:*)",
      "Bash(git push:*)",
      "Bash(gh pr create:*)",
      "Bash(gh pr merge:*)",
      "Bash(gh pr comment:*)"
    ]
  }
}
```

Now the agent can pull a PR's diff, read the surrounding code, and write its
review *as a chat message to you* — but it physically cannot edit files, commit,
push, or post anything to GitHub. If you later want it to post the review as a
comment, move `Bash(gh pr comment:*)` from `deny` to `ask` so each post needs a
click.

Two things to know:
- Patterns are matched, not magic. Test them — ask the agent to try a denied
  command and confirm it's blocked.
- Read-only by permissions is stronger than read-only by instruction. A line in a
  prompt is a request; a `deny` rule is a wall.

## Reduce the prompts you actually want

The flip side of guardrails is friction. If you're approving the same harmless
read-only commands twenty times a day, add them to `allow`. A good loop: every
so often, look at what you've been approving, and promote the safe, repetitive
ones into the allowlist. Keep `git push`, deploys, and deletes on `ask` or
`deny`; promote `git status`, `ls`, test runs, and the like.

## Hooks: rules that run code, not just match patterns

Permissions answer "may this tool run?" Hooks let you run your *own* command at
defined moments — before a tool call, after one, when the agent stops — and act
on the result. That's how you enforce behavior the model can't be trusted to
remember every time.

Examples worth having:

- **Block commits to the main branch.** A pre-tool hook on `git commit` that
  checks the current branch and refuses if it's `main`/`master`, nudging the
  agent to branch first.
- **Run the formatter after every edit.** A post-edit hook that runs your
  formatter so the working tree never drifts out of style.
- **Forbid a path.** A hook that rejects writes under `vendor/`, `dist/`, or a
  generated directory.

The important property of a hook is that *the harness runs it*, not the model.
"From now on, always do X before Y" is a hook, not a polite instruction —
because the model will eventually forget and the hook won't.

## How to think about it

Draw the line between reversible and not-reversible. Everything reversible:
allow. Everything not: ask or deny, plus a hook if it needs logic. Encode it in
the repo so a new teammate (or a fresh session) inherits the same guardrails on
day one without being told.
