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

$L^∗ = \bigcup^{\infty}_{i=0}L^i$, where $L^0 = {ϵ}$, $L^1=L$, and $L^{k+1}=L.L^k(k = 1,2,...)$

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

## Deterministic Finite Automata

### Definition

A deterministic finite automaton (DFA) is a 5-tuple *A* = (*Q*, Σ, δ, *q*0, *F*), where

*Q* is a finite set of states,

Σ is a finite set of input symbols (i.e. an alphabet),

δ is a transition function from *Q* × Σ to *Q*,

*q*0 ∈ *Q* is a start state,

*F* ⊆ *Q* is a set of final or accepting states

**Example**

Let *Q* = {$q_0, q_1, q_2$}, Σ = {0, 1}, *q*0 is the start state, and *F* = {$q_1$}. If transition function δ : *Q* × Σ → *Q* is defined by

δ($q_0$, 0) = $q_2$, δ($q_1$, 0) = q_1, δ($q_2$, 0) = $q_2$,

δ($q_0$, 1) = $q_0$, δ($q_1$, 1) = $q_1$, δ($q_2$, 1) = $q_1$,

then $A1 = (\{q_0, q_1, q_2\}, {0, 1}, δ, q_0, \{q_1\})$​ is a DFA

### Intuitional Descriptions for DFA

**Transition diagram** a graph in which the nodes are the states, and arcs are labeled by input symbols, indicating the transitions of that automaton.

The automaton $A1 = (\{q_0, q_1, q_2\}, {0, 1}, δ, q_0, \{q_1\})$​  as a transition diagram:

![image-20240317183104453](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317183104453.png)

**Transition table** a tabular listing of the transition function δ, which by implication tells us the set of states and the input alphabet.

The automaton $A1 = (\{q_0, q_1, q_2\}, {0, 1}, δ, q_0, \{q_1\})$  is represented as the transition table:

![image-20240317183212751](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317183212751.png)

### Extended Transition Function

The transition function δ can be extended to $\hat{δ}$​ that operates on states and strings (as opposed to states and symbols) by induction on the length of the input string:

*Basis step*:  $\hat{δ}$(*q*, ϵ) = *q*

*Inductive step*: Suppose *w* = *xa*, then $\hat{δ}$(*q*, *w*) = δ($\hat{δ}$​(*q*, *x*), *a*)

### Language of DFA

The language of a DFA *A* = (*Q*, Σ, δ, *q*0, *F*) is defined by

*L*(*A*) = {*w* | $\hat{δ}(q_0, w)$ ∈ *F*}

Note that we require that δ, and consequently $\hat{δ}$, be *total functions* (at each step, there is a unique move is defined, so that we have justified in calling such an automaton deterministic).

A DFA will process *every* string in $Σ^∗$​ , which will be either accepted or not.

If *L* is a language for some DFA A, we say *L* is a regular language.

To show any language is regular, all we have to do is finding a DFA for it

### Languages defined by other condition

One may ask what if the acceptance condition

{*w* | $\hat{δ}(q_0, w)$ ∈ *F*} is changed to {*w* | *w* = *uv* ∧ $\hat{δ}(q_0, w)$ ∈ *F*},

which means we accept this string *w* whenever some intermediate state is in *F*.

We can rephrase it as making all states in *F* absorbing, since the successive states are irrevalent to accept or reject in the setting

DFAs with final states being absorbing are still DFAs, which has the restriction

(*q*, *a*) = *q* for each *q* ∈ *F* and *a* ∈ Σ,

so the new languages in the consideration are still in the scope of regular

languages.

A more interesting question is whether every regular language over alphabet Σ can be accepted by such a special DFA.

**Unfortuniately, the answer is negative**

### Designing DFA

**Example**

Suppose Σ = {*a*, *b*}, design a DFA to accept all strings that start and end with *a*, or start and end with *b*.

![image-20240317191836601](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317191836601.png)

## Nondeterministic Finite Automata

### An Informal View of NFA

The difference between the DFA and the NFA is in the type of transition function. For the NFA, transition function takes a state and an input symbol as arguments, but returns a set of zero, one, or more states.

That means, an NFA can be in several states at once, or, viewed another way, it can “guess” which state to go to next.

![image-20240317190740442](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317190740442.png)

### Definition of NFA

A nondeterministic finite automata (NFA) is a 5-tuple *A* = (*Q*, Σ, δ, *q*0, *F*), where

*Q* is a finite set of states,

Σ is a finite set of input symbols (i.e. an alphabet),

δ is a transition function from *Q* × Σ to the powerset $2^Q$ of *Q*,

$q_0$ ∈ *Q* is a start state,

*F* ⊆ *Q* is a set of final or accepting states

### Extended Transition Function

The transition function δ of an NFA can be extended to $\hat{δ}$ :

Basis step: $\hat{δ}$(*q*, ϵ) = {*q*}

Inductive step: Suppose *w* = *xa*, then

$\hatδ(q,w) = \bigcup_{p∈\hatδ(q,x)}δ(p,a)$

### Language of NFA

The language of an NFA *A* = (*Q*, Σ, δ, *q*0, *F*) is defined by

*L*(*A*) = {*w* | $\hat{δ}(q_0, w) ∩ F \ne ∅$}

### Designing NFA

**Example**

Find an NFA with a single final state that accepts the set {*a*} ∪ {$b^n$ | *n* ≥ 1}

**Solution** 

![image-20240317191724476](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317191724476.png)
