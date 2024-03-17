# Introduction to the Theory of Computation

## Inductive Proofs

### Induction on Integers

In order to prove a statement *S*(*n*) on an integer *n*, one common approach is proving two facts:

1 *The basis step*—we show *S*(*i*) is true for a particular integer *i*. (Usually, *i* = 0 or *i* = 1.)

2 *The inductive step*—we assume *n* ≥ *i*, where *i* is the basis integer, and show that “if *S*(*n*) then *S*(*n* + 1)”. Intuitively, the two facts could convince us that *S*(*n*) is true for all *n* ≥ *i*.

Why Induction Is Valid?

The reason comes from **the well-ordering property**:

*Every nonempty set of nonnegative integers has a least element*

**Proof** 

Suppose *S*(*n*) was false for one or more of those integers. Then, by the well-ordering property, there would have to be a smallest value of *n*, say *j*, for which *S*(*j*) is false, and yet *j* ≥ *i*.

Now *j* could not be *i*, because we prove in the basis part that *S*(*i*) is true.

Thus, *j* must be greater than *i*. We now know that *j* − 1 ≥ *i*, and *S*(*j* − 1) is true.

However, we proved in the inductive part that if *n* ≥ *i*, then *S*(*n*) implies *S*(*n* + 1). Suppose *n* = *j* − 1. Then we know from the inductive step that *S*(*j* − 1) implies *S*(*j*). Since *S*(*j* − 1) is true, we can infer *S*(*j*).

We have assumed the negation of which we wanted to prove; that is, assumed *S*(*j*) was false for some *j* ≥ *i*. In the case, we derived a contradiction. So *S*(*n*) is true for all *n* ≥ *i*. 

Thus, we proved our logical reasoning system:å

**The Induction Principle**

If we prove i) *S*(*i*) and ii) ∀*n* ≥ *i*, *S*(*n*) implies *S*(*n* + 1), then we conclude *S*(*n*) for all *n* ≥ *i*.

Sometimes an inductive proof is made possible only by using a more general scheme than the one proposed. Two important generalizations of this scheme are:

1 Use several basis cases. i.e., we prove *S*(*i*), *S*(*i* + 1), . . ., *S*(*j*) for some *j* ≥ *i*.

2 In proving *S*(*n* + 1), (*n* ≥ *j*), use the truth of all the statements *S*(*i*), *S*(*i* + 1), . . ., *S*(*n*) rather than just using *S*(*n*).

The conclusion to be made from this basis and inductive step is that *S*(*n*) is true for all *n* ≥ *i*.

### Structural Inductions

In computer science theory, there are several recursively defined structures about which we need to prove statements. The familiar notions of trees and expressions are important examples.

Like inductions, all recursive definitions have a basis case, where one or more elementary structures are defined, and an inductive step, where more complex structures are defined in terms of previously defined structures.

When we have a recursive definition, we can prove theorems about it using the following proof form, which is called structural induction. Let *S*(*X*) be a statement about the structures *X* that are defined by some particular recursive definition.

1 As a basis step, prove *S*(*X*) for the basis structure(s) *X*.

2 For the inductive step, take a structure *X* that the recursive definition says is formed from $Y_1,Y_2,. . .,Y_k$. Assume that the statements $S(Y_1),S(Y_2), . . . , S(Y_k)$ are true, and use these to prove that *S*(*X*) is true.

The conclusion is that *S*(*X*) is true for all *X*

### Mutual Inductions

Sometimes, we need to prove a group of statements$S_1(n),S_2(n), . . . ,S_k(n)$ together by induction on *n*. Automata theory provides many such situations.

In fact, proving a group of statements is not different from proving the conjunction $S_1(n) ∧ S_2(n) ∧ · · · ∧ S_k (n)$​ of all the statements. However, when there are really several independent statements to prove, it is generally less confusing to keep the statements separately and to prove them all in their own parts of the basis and inductive steps. We call this sort of proof mutual induction.

## Central Concepts of Automata Theory

### Languages

We start with a finite, nonempty set Σ of symbols, called the alphabet

Example:

Σ = {0, 1}, the binary alphabet

From the individual symbols we construct strings, which are finite sequence of symbols from the alphabet.

Example:

00011101011 is a string from the binary alphabet Σ = {0, 1}

The empty string is denoted ϵ.

The concatenation of strings *x* and *y*, denoted *xy*, is the string obtained by appending the symbols of *y* to the right end of *x*, that is, if $x = a_1a_2· · ·a_i$ , $y = b_1b_2· · ·b_j$  , then $xy = a_1a_2· · ·a_ib_1b_2· · ·b_j$

Example:

Let *x* = 01101, and *y* = 110. Then *xy* = 01101110

Notice that: For any string *w*, ϵ*w* = *w*ϵ = *w*

The length of a strings is the number of positions for symbols in the string.

The length of a string *w* is denoted |*w*|. For example, |00110| = 5, |ϵ| = 0.

The power of an alphabet is a set of strings of a certain length from an alphabet.

The set of strings of length *k*, each of whose symbols is in Σ, is denoted Σ *k* .

For example, if Σ = {0, 1}, then $Σ^0 = {ϵ}, Σ^1 = {0, 1},Σ^2 = {00, 01, 10, 11}$

The set of all strings over an alphabet Σ is denoted $Σ^∗$. For instance, $\{0, 1\}^∗ = {ϵ, 0, 1, 00, 10, 01, 11, 000, . . .}$

The set of nonempty strings from alphabet Σ is denoted $Σ^+$

$  Σ^+ = Σ^1 ∪ Σ^2 ∪ Σ^3 ∪ · · ·$

$Σ^∗ = Σ^+ ∪ {ϵ} = Σ^0 ∪ Σ^1 ∪ Σ^2 ∪ Σ^3 ∪ · · ·$

For any alphabet Σ, $Σ^∗$ is a language.

∅, the empty language, is a language over any alphabet.

{ϵ}, the language consisting of only the empty string, is also a language over any alphabet.

Notice that: $∅ \ne {ϵ}$

Since languages are sets, the union, intersection, and difference of two languages are immediately defined. Let *L* and *M* be both languages, there are other two operations on languages.

Concatenation (dot) 

*L*.*M* = {*w* | *w* = *xy*, *x* ∈ *L*, *y* ∈ *M*}

Closure (star) 

$L^∗ = \bigcup^{\infin}_{i=0}L^i$, where $L^0 = {ϵ}$, $L^1=L$, and $L^{k+1}=L.L^k(k = 1,2,...)$

### Grammars

A grammar is a 4-tuple *G* = (*V*, *T*, *P*, *S*), where

*V* is a finite set of variables,

*T* is a finite set of terminal symbols,

*P* is a finite set of productions of the form *x* → *y*, where $x ∈ (V ∪ T)^+$and $y ∈ (V ∪ T)^∗$ , *S* ∈ *V* is a designated variable called the start symbol.

### Automata

An automaton is an abstract model of a digital computer. Following figure shows a schematic representation of a general automaton

![image-20240317160220320](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317160220320.png)

This general model covers all the automata we will discuss in this course. A finite-state control will be common to all specific cases, but differences will arise from the way in which the output can be produced and the nature of the temporary storage.

It is necessary to distinguish between **deterministic automata** and **nondeterministic automata**. A deterministic automaton is one in which each move in uniquely determined by current configuration. In a nondeterministic automaton, this is not so.

