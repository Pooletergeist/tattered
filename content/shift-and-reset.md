+++
title = "Shift and Reset"
date = 2023-11-20
draft = true

[taxonomies]
categories = ["Computer Science", "Functional Programming"]
tags = ["placeholder posts", "tag1"]
+++

hello, world!

Shift and Reset are control oeprators for delimited continuations.
What's a delimited continuation? Why, thank you for asking!
A continuation is "the rest of the computation". Or, "all the bits
the program will do once it's done the bit it's doing now".

A delimited continuation is "some of the rest of the computation". Or, "some
of the bits it'll do once it's done the bit it's doing now".

We denote the bit it's doing now by a "hole" `[.]`
Two ways of thinking about the continuation.

1. What's left of the computation
2. What'll get discarded if an `abort` happens during the hole

```
6+5*3+1
```

Say it's running the `5*3` in good pemdas fashion.

```
6+[.]+1
```

is the continuation.


## For Partial Evaluation

Say you're partially evaluating (aka. specializing) a let-block in your program.
`let x = y in z`. You want to specialize y, substitute y into z, and
specialize z. 

Further, you're written in CPS, so everything takes a continuation `k` and
never returns.

```
def specialize_...(<thing-we-specialize>, <env>, <continuation>):

specialize_let(let_block, env, k):
    get formal from let_block
    get actual from let_block
    get body from let_block

    specialize(actual, env, lambda v: k( v
                                        body: body, extended_env, k))
```

When specialize(actual...) finishes, it calls lambda v:..., giving the 
specialized value of v to the continuing computation so that
body can be specialized with the most-specific value for the actual param: `v`.

Note lambda v: applies k to it's args (presumably that will involve specializing
body) but all we really know is that computation will continue via that k apply
with this `v` in the new environment.

*processing the body with the same continuation k is important since..*

`+ 1 (let ([x D]) 3))`

There's a problem where when `D` is dynamic, you can't get rid of `let ([x D]).`
But, normally, you should just be able to do `+1 (3)`, even if you need to 
reconstruct `let ([x D])` so it can be run dynamically, in-case the programmer
is counting on side effects from it or smth.

If you propagate the result of specialize 3 to the continuation of the let expn,
you can do `+1 (3)` at specialization time. The reason this wouldn't happen if
you returned the value 3 to the reconstructor the let expression is that it 
would just rebuild `let ([x D]) 3` whole-cloth.

## when is something a tail call? - final action of procedure
specialize calls are not tail calls in body for let and case branches, even tho
they're last calls, because the Let-Block is the result. It gets evalated to a
value, after specialize does.
## why do I care? - not in CPS

References:
[Asai, Oleg, 2011 Tutorial](http://pllab.is.ocha.ac.jp/~asai/cw2011tutorial/main-e.pdf)
