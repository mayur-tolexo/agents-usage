# Workshop kit

A facilitator's kit for running a hands-on Claude Code session with your team.
It's built to be run live in about 2.5 hours, with everyone working in **their
own repository** — the practice is real, on code they care about, and there's no
sample project to set up or maintain.

## What's here

| File | For | Use it |
|------|-----|--------|
| `README.md` | You, before the session | What to send attendees; what you prepare |
| `facilitator-guide.md` | You, during the session | The minute-by-minute run-sheet — talking points, demos, exercises, debriefs |
| `exercises.md` | Attendees | Standalone exercise cards you hand out as you reach each module |
| `handout.md` | Attendees, after | A one-page cheat-sheet they keep |

The guide assumes the team has read — or will read — the chapters in the repo
root. The workshop drills the seven highest-leverage ones; the rest are
follow-up reading (the handout lists them).

## Who it's for

People who already write code and have Claude Code installed, but haven't built
the *habits* — they're using it as a code typer, not as a thinking-and-building
partner with guardrails. Group size: works for 3–12. Beyond that, split into
pods and have a co-facilitator per pod for the exercises.

## Send this to attendees beforehand

> **Before the workshop — 15 minutes of setup.** Please come with:
>
> 1. **Claude Code installed and authenticated.** Confirm it runs and you can
>    start a session.
> 2. **A real repo you can experiment in.** Your own, or a fork — somewhere you
>    can freely create branches and commits without disrupting anyone. Make sure
>    it builds and its tests pass *before* you arrive, so a red build during an
>    exercise is something you caused, not pre-existing.
> 3. **`git` and the GitHub CLI (`gh`) working**, authenticated to wherever your
>    repo lives.
> 4. Skim `00-principles.md` and `09-claude-code-playbook.md` in the guide repo.
>
> If any of step 1–3 fails, ping me before the session — we won't have time to
> debug installs live.

## What you (the facilitator) prepare

- **Run through every demo yourself first**, on your own repo, the day before.
  Live demos fail in small ways; you want to have hit those already. Each module
  in the guide has a demo script — rehearse it.
- **Pick your own repo for demos** — one with a bit of real history, a test
  suite, and a remote. The guardrails and PR modules need a remote to be
  convincing.
- **Decide your permission-demo sandbox.** Module 3 has people add `deny` rules.
  Make sure attendees know they're editing project-local settings in their
  practice repo, not their global config.
- **Have the handout ready to share** at the end (link or print).
- **Timekeeping.** The agenda is tight. Put the per-module times somewhere you
  can see them. It's fine to cut an exercise short and move on — the debrief
  matters more than everyone finishing.

## The shape of the session

```
00  Intro + the five principles        15m
01  Context hygiene                     25m
02  Understand -> brainstorm -> design  30m
    break                               10m
03  Guardrails (permissions + hook)     25m
04  Clean code + self-verification      25m
05  A clean draft PR                    20m
06  Plugins + wrap-up                   20m
                                  total ~2h50 with buffer
```

Aim to start on time and protect the break. If you're running long, the plugin
walk-through in Module 6 is the safest thing to compress.
