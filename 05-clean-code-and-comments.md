# 05 — Clean code and precise comments

Agents will happily produce code that runs but reads badly: no comments, or
comments that narrate the obvious, or a function that does five things. You get
clean code by asking for it explicitly and by encoding the standard so you don't
have to ask every time (chapter 03).

## Match the code that's already there

The first rule in an existing codebase: new code should look like it belongs.
Same naming, same file layout, same comment density, same idioms. An agent that
writes "clever" code in a plain codebase has made the codebase worse even if the
code is correct. Tell it to follow the surrounding style, and check that it did.

## Comments: precise, one per unit, no storytelling

The standard worth holding: **every function and method gets a short comment that
says what it does**, and any non-obvious bit of logic gets a line explaining the
*why*. A reviewer should understand the code from the comment plus the code
alone.

What a good comment is **not**:

- A restatement of the code. `// increment i` above `i++` is noise.
- A story. No "we tried X, then Y, then settled on this."
- A reference to outside context. No ticket numbers, no PR links, no "see the
  RFC." The comment must stand on its own — someone reading the file in two years
  has none of that context.

What a good comment **is**:

```go
// splitHostPort separates "host:port" into its parts and defaults the port to
// 443 when the input omits it. Returns an error for a malformed host.
func splitHostPort(s string) (host string, port int, err error) {
```

One line, says what it does and the one surprising thing (the default), no
narrative. For a flow with a subtle step, add the *why* right where it happens:

```go
// Check the previous key too: a token signed just before a rotation is still
// valid until its own expiry.
for _, k := range r.validKeys() {
```

If your project already has comments, **extend them, don't rewrite them**. A diff
that touches working comments invites needless review noise. Add new precise
ones; leave the existing ones alone unless they're wrong.

## Tests come with the code, not after

"Done" includes tests. A sensible bar for new code is meaningful unit-test
coverage of the logic you added — not a coverage number for its own sake, but
enough that the behavior is pinned down. Have the agent write them, then *run
them and read the output* (chapter 00, principle 4). Tests are also your best
defense against the agent's later changes silently breaking something.

## "Done" means the build is green

Before any change is finished, the basics must pass:

- it builds / compiles
- the linter and vetter are clean
- the tests pass
- the formatter has been run

Make this explicit. "Implement X" does not imply "and leave the build broken."
A short skill or memory entry — "before calling work done, run build, vet, test,
and format; all must be green" — turns this from something you check into
something the agent checks itself. Don't accept "done" without the evidence that
these passed.

## The standard, in one line

New code reads like the code around it, every unit has a precise self-contained
comment, the logic is tested, and the build is green — *before* anyone calls it
done.
