# 06 — Brainstorming and design loops

This is the habit that most separates good agent output from bad: do the design
work *with* the agent, in a loop, before any code gets written. Principle 3 in
chapter 00 said "don't jump to code." This chapter is how.

## Why a loop, not a one-shot

If you say "build me X" and the agent immediately writes X, it has silently made
a dozen decisions you never saw — and the wrong ones are now baked into code
that's annoying to unwind. A design loop surfaces those decisions while they're
still cheap to change (they're just words).

The loop is simple:

```
understand → propose options → you pick / push back → refine → repeat → agree → build
```

You stay in it until the design feels right, *then* you implement. Often that's
three or four rounds of a few minutes each. It feels slower; it's much faster
end-to-end, because you're not rewriting code.

## How to run it

**1. Make it ask, not assume.** Start with intent, not a spec:

> "I want to add X. Before any code: ask me what you need to know, one question
> at a time, until you understand the goal and constraints."

One question at a time matters — a wall of ten questions gets shallow answers.
Let it dig into one thing, then the next.

**2. Demand options, not a single answer.** For any real decision:

> "Give me two or three ways to do this, with the trade-offs, and tell me which
> you'd pick and why."

Seeing the alternatives is where the thinking happens. The recommendation is
useful; the *contrast* between options is what lets you choose well.

**3. Refine in passes.** Present the design in pieces — architecture, then the
components, then error handling, then testing — and react to each. "That's right."
"No, the cache should be per-user." "What happens when the upstream is down?"
Each pass tightens it.

**4. Agree explicitly before building.** End the loop with a clear "yes, build
that." A written design you both signed off on is the contract the implementation
follows.

## Design for small, clear pieces

While you're designing, push toward a system made of small units that each do one
thing, talk through clear interfaces, and can be understood on their own. For each
piece you should be able to say: *what does it do, how do you use it, what does it
depend on?* If you can't, the boundaries are wrong and now — in words — is the
cheap time to fix them. (This also helps the agent: it reasons better about, and
edits more reliably, code it can hold in context at once.)

## Capture the design, then plan, then build

Once you agree, two more steps before code:

1. **Write the design down** — a short doc of what you settled on and why. Keep
   it where your team keeps such things. (If your convention is not to commit
   design docs into the repo, keep it local — just don't lose the reasoning.)
2. **Turn it into a plan** — an ordered list of implementable steps, each small
   enough to verify on its own (chapter 00, principle 2). Then work the plan.

Design → plan → build, with your sign-off between each. The agent can drive all
three; the gates are yours.

## The anti-pattern to watch for

"This is too simple to need design." That thought is usually wrong — the simple
tasks are exactly where an unexamined assumption wastes the most work, because
nobody slowed down to check it. The design can be three sentences for a small
thing, but say them and agree on them before building.
