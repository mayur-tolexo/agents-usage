# Exercise cards

Hand these out as you reach each module. Every card runs on the attendee's **own
repo**, so success checks are generic ("your build is green", "the push was
blocked") rather than exact diffs. Each card is self-contained — an attendee can
follow it without the facilitator guide.

A standing rule for every exercise: **work on a branch, never on `main`.** If you
break something, you throw the branch away.

---

## Exercise 1 — The two-pass change (Module 1)

**Goal.** Feel how a fresh, scoped session beats one long one.

**Pick.** A small change you could genuinely make in your repo — rename a thing,
add a small flag, fix a tiny bug. Nothing big.

**Steps.**
1. Start a **fresh** session.
2. Ask *only*: "Which files would I need to change to do `<the change>`? Don't
   edit anything — just list the files and why each."
3. Note the answer. Then **end that session.**
4. Start a **second fresh** session. Give it just those file paths and the goal.
   Let it make the change on a branch.

**Success check.**
- The second session never had to explore — it went straight to the edit.
- The change builds. (`<your build command>` is green.)

**Common pitfalls.**
- Letting the first session start editing. Stop it — pass one is *find*, not fix.
- Picking a change too big to hold in one exercise. Smaller is better here.

---

## Exercise 2 — Run the design loop (Module 2)

**Goal.** Catch design decisions while they're still words, not code.

**Pick.** A small feature or change you've been meaning to make.

**Steps.**
1. Start a session. Prompt: "I want to `<feature>`. Before any code, ask me what
   you need to know, one question at a time, until you understand the goal and
   constraints."
2. Answer its questions. Don't rush it to the end.
3. Prompt: "Give me two or three ways to do this with trade-offs, and tell me
   which you'd pick and why."
4. Push back on at least one thing. Refine until you'd actually sign off.

**The rule.** **Do not let it write code.** The output of this exercise is a short
agreed design, not an implementation.

**Success check.**
- You can state, in two sentences, the approach you chose and *why* over the
  alternatives.
- At least one assumption surfaced that you corrected.

**Common pitfalls.**
- Accepting the first single answer. Make it give you the *contrast* of options.
- A wall of ten questions at once — tell it one at a time.

---

## Exercise 3 — Guardrails (Module 3)

**Goal.** Turn "please don't push" from a request into a wall.

**Steps.**
1. In your practice repo, open (or create) the project-local `settings.json` under
   `.claude/`. **Confirm it's the project file, not your global config.**
2. Add a `deny` rule for `Bash(git push:*)`. Optionally also deny `Edit` and
   `Write` to make it review-only.
3. Ask the agent to push something.

**Success check.**
- The push is **blocked** by the permission, not merely declined.
- If you added the edit/write denies, the agent also can't change files — confirm
  it.

**Stretch (fast finishers).** Sketch a hook that blocks `git commit` when the
current branch is `main`/`master`: what does it check, and what does it do on a
match? You don't have to wire it up — describe the check and the refusal.

**Common pitfalls.**
- Editing global settings by accident. Check the path.
- Confusing "the agent said it won't" with "the agent can't." You want the wall.

---

## Exercise 4 — Clean code and self-verification (Module 4)

**Goal.** Precise comments, a real test, and a verification you can see.

**Pick.** A messy or under-commented function in your repo.

**Steps.**
1. On a branch, have the agent add **precise, self-contained comments**: one line
   per function/method saying what it does and the one surprising thing — no
   stories, no ticket references — matching your house style.
2. Have it write a unit test for that function.
3. Have it **run** the test and paste the real output into the chat.
4. Run the self-check: "double-check every claim you just made and give me a
   table of what you could and couldn't verify."

**Success check.**
- The comments would make sense to someone with no outside context.
- The test actually ran and you saw real (not described) output.
- The build is green.

**Common pitfalls.**
- Comments that restate the code (`// increment i`). Coach for *what* and *why*,
  not *how*.
- Accepting "tests pass" without the pasted run. No evidence, not verified.

---

## Exercise 5 — A clean draft PR (Module 5)

**Goal.** A PR description that reads like a person wrote it.

**Steps.**
1. From a small branch (Exercise 1 or 4's change works), have the agent open a
   **draft** PR.
2. Require the description to be plain prose: what changed and why, the one or two
   things a reviewer should look at, and a **real pasted** test/build output.
   Explicitly: no `## What / ## How` scaffolding, no emoji headers.
3. Open the draft in the review UI and read it like it's a colleague's.

**Success check.**
- The description explains the *why*, not just the *what*.
- It contains real pasted evidence, not "tests pass."
- It's a **draft** — nothing is marked ready.

**Common pitfalls.**
- Scaffolded sections sneaking back in. Coach it into prose live.
- Marking it ready. Leave that to a human — that's the point.

---

## Exercise 6 — (optional) Wire up one extension (Module 6)

**Goal.** Adopt one extension for a concrete pain, the disciplined way.

**Steps.**
1. Name one recurring friction ("I keep coding against stale library docs", "I
   read half the repo to answer one question").
2. Pick one candidate from the shortlist in `10-plugins-and-extensions.md` that
   targets it.
3. Before installing: what access does it want, and is it actively maintained?
4. Try it on the *specific* pain in the smallest way possible.

**Success check.**
- You can state the pain it removes and the access it asked for.
- You tried it on the real problem, not a toy.

**Common pitfalls.**
- Installing five at once. One, matched to a real pain.
- Skipping the trust/access check. These run code and see your data.
