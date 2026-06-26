# 08 — Understand before you design

Chapter 06 was about designing before coding. This one is a step earlier: make
sure the agent (and you) actually understand the *problem* before designing a
solution. A clean design for the wrong problem is still wrong.

## The failure this prevents

Hand an agent a one-line request and it will design something plausible — for the
problem it *imagined*, which may not be yours. The gap shows up late, in code,
when the thing technically works but doesn't fit the real use-case. The fix is to
spend the first part of any non-trivial task building shared understanding.

## Build understanding in three layers

### 1. The current state — explore the codebase
Before proposing anything, the agent should know what's already there. Ask it to
map the relevant territory:

> "Before we design: walk the parts of this codebase that touch X. How does it
> work today, what are the main pieces, and where would a change to do Y have to
> reach? Don't propose anything yet — just show me the lay of the land."

This grounds the design in reality instead of a generic best-practice the agent
recalls from elsewhere. (Tools that pre-digest a codebase into a queryable map —
chapter 10 — make this step much cheaper on a large repo.)

### 2. The real challenge — name the actual problem
Push past the surface request to the underlying need:

> "What problem is this really solving? What's painful today, who feels it, and
> what does 'fixed' look like for them?"

Often the stated request ("add a cache") is one solution to a deeper problem
("this page is too slow"), and naming the deeper problem opens better options.

### 3. The use-cases — enumerate how it'll actually be used
A design that only handles the happy path breaks on contact with reality. Get the
cases on the table first:

> "List the concrete ways this will be used — the common path, the edge cases,
> the failure cases, the unusual-but-real ones. Which must we handle now, which
> can wait?"

Now the design has a spec to satisfy, and you've decided scope *before* writing
code instead of discovering it midway.

## Only then, design

With the current state mapped, the real problem named, and the use-cases listed,
*now* run the design loop from chapter 06. The design will be better because it's
answering a real, bounded question instead of a vague one.

The order is the whole point:

```
understand the code  →  name the real problem  →  list the use-cases  →  design  →  plan  →  build
```

Each arrow is a gate where you can catch a wrong turn cheaply. The earlier you
catch it, the less it costs.

## A note on scope

While you're understanding the problem, watch for the request that's secretly
several projects ("build a platform that does A, B, C, and D"). If it is,
decompose it first: what are the independent pieces, how do they relate, what
order do they get built? Then take the first piece through understand → design →
build on its own. Trying to design four subsystems in one pass produces a shallow
design for all four.

## The principle

Slowing down to understand is not overhead — it's the cheapest place to be wrong.
Being wrong in your understanding costs a sentence to fix; being wrong in shipped
code costs a rewrite. Spend the time at the front.
