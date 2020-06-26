---
layout: post
title: The Halting Problem
---

You’re sat at your desk, watching a progress bar stuck at 99%, wondering if it will ever finish. This is exactly the question that the halting problem asks.

*<center>Given an input, will a computer program run forever, or eventually halt?</center>*

For example, the simple program

```
while (true) {
    print("This one goes forever.");
}
```

would loop forever. Whereas the program

```
print("This one doesn't.");
```

would halt.

More specifically, our problem asks if we can construct a function that can explicitly determine if a program will terminate or not? In 1963, Alan Turing proved that such a function does **not** exist. The proof goes a bit like this:

Assume such a function h does exist. It takes a program $$P$$ and input $$i$$ and determines if the program halts for that particular input. Note that it does not matter how it determines this.

```
function h(P, i) {
     if ( P(i) halts) {
         return "Halts."
     }
     else {
         return "Doesn't halt.";
     }
 }
```

In theory, this is the function that would determine whether or not a program terminates, thereby solving the halting problem. Now, by assuming that $$h$$ does exist, we will proceed to show that no such a function can exist.

First, consider the function $$g$$, similar to $$h$$, defined as follows:

```
function g(P, i) {
     if( P(i) halts) {
         loop forever;
     }
     else {
         return "Doesn't halt.";
     }
 }
```

Now, what happens if we run $$g(g,g)$$, feeding $$g$$ into itself[^1]? 
There are two cases:

 If $$g$$ *does halt*, $$g$$ will “loop forever” and therefore not halt.
If $$g$$ *doesn’t halt*, then $$g$$ should halt.
Clearly, we have reached a contradiction, so such a function cannot exist.

Of course, in reality all computers have finite memory and will therefore halt at some point. So why is this result important?

In practical terms, many problems actually reduce to the halting problem at their essence.

For example, say you are trying to optimise a program, and you want to know if a particular line will ever be executed. If you replace that line with the `HALT` instruction, this problem becomes equivalent to the halting problem. Hence, it is impossible to optimise a program perfectly (for all inputs). There are many (many) such examples, including uses in programming language design (parsers, type-checkers) and security.

It is also closely linked with Gödel’s incompleteness theorems, in that the undecidable nature of the halting problem tells us that we are unable to determine whether or not a mathematical formula is a theorem or not. If you were given a list of all axioms and inference rules then you could deduce a list of every theorem. Then, compute a function $$h$$ that when given a theorem $$i$$ traverses the enumeration of all the theorems and halts (see where this is going) when it reaches that particular theorem, thereby showing that such a theorem exists. The halting problem shows that we cannot.

Really, what it boils down to is this: You have an infinite search space, you’re searching for a particular object, if it doesn’t exists you will never know.

No, quantum computers cannot solve the halting problem.

[^1]: If you don't understand recursion, it goes a bit like [this](https://sonjoonho.github.io/2017/12/28/the-halting-problem.html).
