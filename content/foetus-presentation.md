+++
title = "Termination and Dependent Types"
date = 2023-10-24

draft = true # only display if --drafts flag passed to command

[taxonomies]
categories = ["CS"]
tags = ["presentations", "tag1"]
+++

0. You can stall by loops or recursion.
1. No loops
---
2. only stall on recursion.

1. in recursion, function calls on args. (empty args)
2. args can >, <, or =
3. suppose no infinite chain of <
4. If args <, then arg must hit bottom.
5. If arg hit bottom, case must be matched.
6. If arg hits bottom, cannot > or =, f must terminate.
---
7. If arg <, f terminates.

---

You're proving a theorem in Agda, and you want to be able to leave your computer
running theorem-proving while you focus on your passion for wallpainting. 
Unfortunately, you know that termination in-general is undecidable. So your
computer might run hopelessly forever and you won't get tenure — too scary of
a thought to focus anxiety free on wallpainting, as you should.

So, you need a termination checker. You're going to be able to express fewer
programs, (your checker might not let you run programs that will come up with 
correct proofs), but that's prefereable to a nervous breakdown.

Per Agda's docs, your proof hinges on a function ack:
```
ack : Nat → Nat → Nat
ack zero    m       = suc m
ack (suc n) zero    = ack n (suc zero)
ack (suc n) (suc m) = ack n (ack (suc n) m)
```
Will it terminate?


Pythonic version
```
def ack(x,y):
    if x == 0:
        return y+1
    else:
        if y == 0:
            return ack(x-1, 1)
        else:
            return ack(x-1, ack(x,y-1))
```
Try some toy examples! 
```
ack(2, 0)
ack(4, 2) <- for all the marbles
```

Well yes, complicated case, left arg gets smaller by one, right becomes the
call where the left stays the same and the right gets smaller than one. Less
complicated cases, right can grow from 0 by one, but left shrinks. Left can 
never grow.

If instead, you add this rule ` ick zero (suc n)    = ick (suc zero) n`, bad things happen. Consider full grammar.
```
ick : Nat → Nat → Nat
ick zero    m       = suc m
ick (suc n) zero    = ick n (suc zero)
*ick zero (suc n)    = ick (suc zero) n*
ick (suc n) (suc m) = ick n (ick (suc n) m)
```
What happens if you do `ick 1 0`?
Well,
```
ick 1 0
| matches ick (suc n) zero
=> becomes ick 0 1
| matches ick zero (suc n)
=> becomes ick 1 0
```
Oops!

/*
What happens if you do `ick 1 1`.
Well, complicated case.
```
=> ick 0 (ick 1 0)`
=> ick 0 (ick 0 1)
```
*/

# what's a constructor?
- [builds new tpes from old ones.](https://en.wikipedia.org/wiki/Type_constructor)

# [Primitive Recursion, each argument one smaller each time](https://agda.readthedocs.io/en/v2.6.4/language/termination-checking.html)
Plus and NatEq can be defined so that arguments are one constructor smaller each
time. Plus (suc n) m => suc(plus n m)

# [Structural Recursion, at least one argument smaller each time, none bigger](https://agda.readthedocs.io/en/v2.6.4/language/termination-checking.html)
Ack. More calls, smaller arguments.


## Insight: no loops, just recursion. Look at the calls.
Consecutive applications become a function call. 
`((add x') y)`

1. Constructor Elimination.
*How do the paramaters on the left show up on the right?*
`( | add (suc n) m = suc (add n m))`. 
On the left, we have `(suc n)` and `m`. On the right, we still have `m`, but `suc n` shrinks to `n`. We saw that `(suc n)` is `successor` fn applied to `n`. 
So when you remove the constructor function `suc`, you get a smaller term.
In general, when `x = C(y)`, `x > y`. So shrinking `x` to `y` is good.
In the above, `succ` is the constructor `C`. The `x` is `(succ n)`, and the y
is just `n`. We call that constructor elimination because we just got rid of 
`C`.

2. Projection. - [Extracting one from a pair](https://agda.readthedocs.io/en/v2.5.3/language/record-types.html)
Any term in `y.Lpx` is as big as the whole tuple. x is as big as y is as big as
`y.Lpx`. TODO: EXAMPLE

3. Application
ex. addord.


# How do compilers use types?

# Erasure \& Accessibility Predicates
*Erasure*
Type annotation for terms that disappear at run time. Type check enforces no
computations depend on erased values.
[Agda docs, run-time irrelevance](https://agda.readthedocs.io/en/v2.6.1/language/runtime-irrelevance.html)

*Accessibility*
[Well-founded if all elements are accessible.](https://agda.github.io/agda-stdlib/Induction.WellFounded.html)

*Well-Founded*
[There's no infinite chain x > x1 > x2 > ...](https://scm.iis.sinica.edu.tw/home/2008/well-founded-recursion-and-accessibility/)

# Efficiency

# Decidability



## Termination Checker Shortcomings

[using with](https://stackoverflow.com/questions/71233632/termination-checking-failed)
[in cubical, fine in normal](https://github.com/agda/agda/issues/5953)
[moving dot](https://github.com/agda/agda/issues/4725)
## [Cubical Agda Termination:](https://lists.chalmers.se/pipermail/agda/2018/010606.html)

---

# [Memes](http://strictlypositive.org/winging-jpgs/)
