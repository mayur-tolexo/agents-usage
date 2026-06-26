# 07 — Evaluating open-source options

Before you build something, check whether it already exists. An agent is very
good at this — finding candidates, comparing them, and reading their source — but
only if you make it compare honestly instead of grabbing the first result.

## Step 1 — search wide, on purpose

Ask for several candidates, not one:

> "I need to do X. Find the leading open-source options — at least three or four —
> across package registries and GitHub. For each: what it is, how popular and how
> maintained it is, and its license."

Searching wide matters because the first hit is often not the best fit; it's just
the best-marketed. You want the field, then a choice.

## Step 2 — compare on a fixed rubric

Don't accept "library A is nice." Make the comparison a table against the same
criteria for every candidate, so the choice is grounded:

| Criterion | Why it matters |
|-----------|----------------|
| **Fit** | Does it actually do what you need, or 60% of it? |
| **Maintenance** | Recent commits, releases, open-vs-closed issues — is it alive? |
| **Adoption** | Downloads / stars / who uses it — a proxy for "battle-tested" |
| **License** | Is it compatible with your use? (a real blocker, check it early) |
| **Dependencies** | What does it drag in? Heavy or risky transitive deps? |
| **Surface** | Is the API small and clear, or a sprawling framework you'll fight? |
| **Exit cost** | If it goes unmaintained, how hard is it to replace or vendor? |

Have the agent fill this in for each candidate, then recommend one *with reasons
tied to the rubric*.

## Step 3 — verify the claims before you trust them

This is where the discipline pays off. Models will state a library's features and
limitations confidently and sometimes wrongly. So make it check:

> "Double-check every claim in that comparison against the actual repos — the
> README, the source, the latest release. Then give me a table of what you could
> verify and what you couldn't."

That one prompt catches a surprising number of "it supports X" claims that turn
out to be "it supported X in a beta two years ago." If a feature is load-bearing
for your decision, confirm it exists *in the code*, not just in a blog post.

## Step 4 — try it small before you commit

Once you've chosen, prove it on the real problem in the smallest way possible — a
throwaway script or a tiny spike that exercises the *specific* thing you need it
for, especially the part you were unsure about. Adopting a dependency is a
decision that's annoying to reverse later; the spike is cheap insurance now.

## Step 5 — adopt deliberately

When you bring it in:

- Pin the version.
- Wrap it behind a thin interface of your own if it's central, so swapping it
  later touches one file, not fifty (the "exit cost" criterion, made real).
- Note in your design doc *why* you chose it over the alternatives — future-you
  will want the reasoning when the trade-offs shift.

## The mindset

"Should we build or borrow?" deserves a real answer, not a default in either
direction. The agent makes the *research* fast — but only the rubric and the
verification step make it *trustworthy*. Wide search, fixed criteria, verified
claims, small spike, deliberate adoption. Skip the verification and you've just
automated picking the best-marketed option.
