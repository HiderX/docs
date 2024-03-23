# Introduction to the Theory of Computation

## Inductive Proofs

### Induction on Integers

In order to prove a statement $S(n)$ on an integer $n$, one common approach is proving two facts:

1 *The basis step*—we show $S(i)$ is true for a particular integer $i$. (Usually, $i = 0$ or $i = 1$.).

2 *The inductive step*—we assume $n \ge i$, where *i* is the basis integer, and show that “if $S(n) then S(n + 1)$”. Intuitively, the two facts could convince us that $S(n)$ is true for all $n \ge i$.

Why Induction Is Valid?

The reason comes from **the well-ordering property**:

*Every nonempty set of nonnegative integers has a least element.*

**Proof** 

Suppose $S(n)$ was false for one or more of those integers. Then, by the well-ordering property, there would have to be a smallest value of $n$, say $j$, for which $S(j)$ is false, and yet $j \geq i$.

Now $j$ could not be $i$, because we prove in the basis part that $S(i)$ is true.

Thus, $j$ must be greater than $i$. We now know that $j - 1 \geq i$, and $S(j - 1)$ is true.

However, we proved in the inductive part that if $n \geq i$, then $S(n)$ implies $S(n + 1)$. Suppose $n = j - 1$. Then we know from the inductive step that $S(j - 1)$ implies $S(j)$. Since $S(j - 1)$ is true, we can infer $S(j)$.

We have assumed the negation of which we wanted to prove; that is, assumed $S(j)$ was false for some $j \geq i$. In this case, we derived a contradiction. So $S(n)$ is true for all $n \geq i$.

Thus, we proved our logical reasoning system:

**The Induction Principle**

If we prove  

i) $S(i)$ and

ii) $\forall n \geq i, S(n) \implies S(n + 1)$, 

then we conclude $S(n)$ for all $n \geq i$​.

Sometimes an inductive proof is made possible only by using a more general scheme than the one proposed. Two important generalizations of this scheme are:

1. Use several basis cases. i.e., we prove $S(i)$, $S(i + 1)$, ..., $S(j)$ for some $j \geq i$.

2. In proving $S(n + 1)$, ($n \geq j$), use the truth of all the statements $S(i)$, $S(i + 1)$, ..., $S(n)$ rather than just using $S(n)$.

The conclusion to be made from this basis and inductive step is that $S(n)$ is true for all $n \geq i$.

### Structural Inductions

In computer science theory, there are several recursively defined structures about which we need to prove statements. The familiar notions of trees and expressions are important examples.

Like inductions, all recursive definitions have a basis case, where one or more elementary structures are defined, and an inductive step, where more complex structures are defined in terms of previously defined structures.

When we have a recursive definition, we can prove theorems about it using the following proof form, which is called structural induction. Let $S(X)$ be a statement about the structures $X$ that are defined by some particular recursive definition.

1. As a basis step, prove $S(X)$ for the basis structure(s) $X$.

2. For the inductive step, take a structure $X$ that the recursive definition says is formed from $Y_1, Y_2, . . . , Y_k$. Assume that the statements $S(Y_1), S(Y_2), . . . , S(Y_k)$ are true, and use these to prove that $S(X)$ is true.

The conclusion is that $S(X)$ is true for all $X$.

### Mutual Inductions

Sometimes, we need to prove a group of statements $S_1(n), S_2(n), . . . , S_k(n)$ together by induction on $n$. Automata theory provides many such situations.

In fact, proving a group of statements is not different from proving the conjunction $S_1(n) \land S_2(n) \land \cdots \land S_k(n)$ of all the statements. However, when there are really several independent statements to prove, it is generally less confusing to keep the statements separately and to prove them all in their own parts of the basis and inductive steps. We call this sort of proof mutual induction.

## Central Concepts of Automata Theory

### Languages

Example:

Σ = {0, 1}, the binary alphabet.

From the individual symbols we construct strings, which are finite sequence of symbols from the alphabet.

Example:

00011101011 is a string from the binary alphabet Σ = {0, 1}.

The empty string is denoted ϵ.

The concatenation of strings *x* and *y*, denoted *xy*, is the string obtained by appending the symbols of *y* to the right end of *x*, that is, if $x = a_1a_2· · ·a_i$ , $y = b_1b_2· · ·b_j$  , then $xy = a_1a_2· · ·a_ib_1b_2· · ·b_j$.

**Example:**

Let $x = 01101$, and $y = 110$. Then $xy = 01101110$.

Notice that: For any string $w$, $\epsilon w = w\epsilon = w$.

The length of a string is the number of positions for symbols in the string.

The length of a string $w$ is denoted $|w|$. For example, $|00110| = 5$, $|\epsilon| = 0$.

The power of an alphabet is a set of strings of a certain length from an alphabet.

The set of strings of length $k$, each of whose symbols is in $\Sigma$, is denoted $\Sigma^k$.

For example, if $\Sigma = \{0, 1\}$, then $\Sigma^0 = \{\epsilon\}, \Sigma^1 = \{0, 1\}, \Sigma^2 = \{00, 01, 10, 11\}$.

The set of all strings over an alphabet $\Sigma$ is denoted $\Sigma^*$. For instance, $\{0, 1\}^* = \{\epsilon, 0, 1, 00, 10, 01, 11, 000, . . .\}$

The set of nonempty strings from alphabet $\Sigma$ is denoted $\Sigma^+$.

$\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \cdots$

$\Sigma^* = \Sigma^+ \cup \{\epsilon\} = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \cdots$

For any alphabet $\Sigma$, $\Sigma^*$ is a language.

$\emptyset$, the empty language, is a language over any alphabet.

$\{\epsilon\}$, the language consisting of only the empty string, is also a language over any alphabet.

Notice that: $\emptyset \ne \{\epsilon\}$.

Since languages are sets, the union, intersection, and difference of two languages are immediately defined. Let $L$ and $M$ be both languages, there are other two operations on languages.

**Concatenation (dot)**

$L.M = \{w | w = xy, x \in L, y \in M\}$

**Closure (star)**

$L^* = \bigcup^{\infty}_{i=0} L^i$, where $L^0 = \{\epsilon\}$, $L^1 = L$, and $L^{k+1} = L.L^k \quad (k = 1,2,...)$

### Grammars

A grammar is a 4-tuple $G = (V, T, P, S)$, where

- $V$ is a finite set of variables,

- $T$ is a finite set of terminal symbols,

- $P$ is a finite set of productions of the form $x \rightarrow y$, where $x \in (V \cup T)^+$ and $y \in (V \cup T)^*$, 

- $S \in V$ is a designated variable called the start symbol.

### Automata

An automaton is an abstract model of a digital computer. Following figure shows a schematic representation of a general automaton.

![image-20240317160220320](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317160220320.png)

This general model covers all the automata we will discuss in this course. A finite-state control will be common to all specific cases, but differences will arise from the way in which the output can be produced and the nature of the temporary storage.

It is necessary to distinguish between **deterministic automata** and **nondeterministic automata**. A deterministic automaton is one in which each move in uniquely determined by current configuration. In a nondeterministic automaton, this is not so.

## Deterministic Finite Automata

### Definition

A deterministic finite automaton (DFA) is a 5-tuple $A = (Q, \Sigma, \delta, q_0, F)$, where

- $Q$ is a finite set of states,

- $\Sigma$ is a finite set of input symbols (i.e., an alphabet),

- $\delta$ is a transition function from $Q \times \Sigma$ to $Q$,

- $q_0 \in Q$ is a start state,

- $F \subseteq Q$ is a set of final or accepting states.

**Example**

Let $Q = \{q_0, q_1, q_2\}$, $\Sigma = \{0, 1\}$, $q_0$ is the start state, and $F = \{q_1\}$. If the transition function $\delta : Q \times \Sigma \rightarrow Q$ is defined by

- $\delta(q_0, 0) = q_2$, $\delta(q_1, 0) = q_1$, $\delta(q_2, 0) = q_2$,

- $\delta(q_0, 1) = q_0$, $\delta(q_1, 1) = q_1$, $\delta(q_2, 1) = q_1$,

then $A1 = (\{q_0, q_1, q_2\}, \{0, 1\}, \delta, q_0, \{q_1\})$ is a DFA.

### Intuitional Descriptions for DFA

**Transition diagram** a graph in which the nodes are the states, and arcs are labeled by input symbols, indicating the transitions of that automaton.

The automaton $A1 = (\{q_0, q_1, q_2\}, {0, 1}, \delta, q_0, \{q_1\})$​  as a transition diagram:

![image-20240317183104453](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317183104453.png)

**Transition table** a tabular listing of the transition function δ, which by implication tells us the set of states and the input alphabet.

The automaton $A1 = (\{q_0, q_1, q_2\}, {0, 1}, \delta, q_0, \{q_1\})$  is represented as the transition table:

![image-20240317183212751](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317183212751.png)

### Extended Transition Function

The transition function δ can be extended to $\hat{δ}$​ that operates on states and strings (as opposed to states and symbols) by induction on the length of the input string:

**Basis step:**  $\hat{\delta}(q, \epsilon) = q$

**Inductive step:** Suppose $w = xa$, then $\hat{\delta}(q, w) = \delta(\hat{\delta}(q, x), a)$

### Language of DFA

The language of a DFA $A = (Q, \Sigma, \delta, q_0, F)$ is defined by

$L(A) = \{w | \hat{\delta}(q_0, w) \in F\}$

Note that we require that $\delta$, and consequently $\hat{\delta}$, be *total functions* (at each step, there is a unique move defined, so that we have justified in calling such an automaton deterministic).

A DFA will process *every* string in $\Sigma^*$, which will be either accepted or not.

If $L$ is a language for some DFA $A$, we say $L$ is a regular language.

To show any language is regular, all we have to do is finding a DFA for it.

### Languages defined by other condition

One may ask what if the acceptance condition

$\{w | \hat{\delta}(q_0, w) \in F\}$ is changed to $\{w | w = uv \land \hat{\delta}(q_0, w) \in F\}$,

which means we accept the string $w$ whenever some intermediate state is in $F$.

We can rephrase it as making all states in $F$ absorbing, since the successive states are irrelevant to accept or reject in the setting.

DFAs with final states being absorbing are still DFAs, which has the restriction

$(q, a) = q$ for each $q \in F$ and $a \in \Sigma$,

so the new languages in the consideration are still in the scope of regular languages.

A more interesting question is whether every regular language over alphabet $\Sigma$ can be accepted by such a special DFA.

**Unfortuniately, the answer is negative**

### Designing DFA

**Example**

Suppose $\Sigma = \{a, b\}$, design a DFA to accept all strings that start and end with \(a\), or start and end with \(b\).

![image-20240317191836601](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317191836601.png)

## Nondeterministic Finite Automata

### An Informal View of NFA

The difference between the DFA and the NFA is in the type of transition function. For the NFA, transition function takes a state and an input symbol as arguments, but returns a set of zero, one, or more states.

That means, an NFA can be in several states at once, or, viewed another way, it can “guess” which state to go to next.

![image-20240317190740442](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317190740442.png)

### Definition of NFA

A nondeterministic finite automaton (NFA) is a 5-tuple $A = (Q, \Sigma, \delta, q_0, F)$, where

- $Q$ is a finite set of states,

- $\Sigma$ is a finite set of input symbols (i.e., an alphabet),

- $\delta$ is a transition function from $Q \times \Sigma$ to the power set $2^Q$ of $Q$,

- $q_0 \in Q$ is a start state,

- $F \subseteq Q$ is a set of final or accepting states.

### Extended Transition Function

The transition function $\delta$ of an NFA can be extended to $\hat{\delta}$:

**Basis step:** $\hat{\delta}(q, \epsilon) = {q}$

**Inductive step:** Suppose $w = xa$, then

$\hat{\delta}(q,w) = \bigcup_{p \in \hat{\delta}(q,x)} \delta(p,a)$

### Language of NFA

The language of an NFA $A = (Q, \Sigma, \delta, q_0, F)$ is defined by

$L(A) = \{w | \hat{\delta}(q_0, w) \cap F \ne \emptyset\}$

### Designing NFA

**Example**

Find an NFA with a single final state that accepts the set $\{a\} \cup \{b^n | n \geq 1\}$

**Solution** 

![image-20240317191724476](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240317191724476.png)

## The equivalence of DFA and NFA

The proof that DFA’s can do whatever NFA’s can do involves an important “construction” called the subset construction.

The subset construction starts from an NFA $N = (Q_N, Σ, δ_N, q_0, F_N)$. Its goal is the description of a DFA $D = (Q_D, Σ, δ_D, \{q_0\}, F_D)$ such that

$L(D) = L(N)$

Here is the detail of the construction

- $Q_D = \{S \mid S \subseteq Q_N\}$
- $F_D = \{S \mid S \subseteq Q_N, S \cap F_N \neq \emptyset\}$

For every $S \subseteq Q_N$ and $a \in \Sigma$,

$$\delta_D(S, a) = \bigcup_{p \in S} \delta_N(p, a).$$

Note that $|Q_D| = 2^{|Q_N|}$, although most states in $Q_D$ are likely to be garbage.

**Example**

Let's construct $\delta_D$ from NFA $A_2 = (\{q_0, q_1, q_2\}, \{0, 1\}, \delta, q_0, \{q_2\})$ where $\delta$​ is the transition function.

![image-20240318085123673](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318085123673.png)

Since the state set of $N$ is $\{q_0, q_1, q_2\}$, the subset construction produces a DFA with $2^3 = 8$​ states, corresponding to all the subsets of these three states. The next slide shows the transition table for these eight states.

![image-20240318085244160](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318085244160.png)

To make the point clearer, we can invent new names for these states, e.g., $A$ for $\emptyset$, $B$ for $\{q_0\}$, and so on.

![image-20240318085423887](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318085423887.png)

Starting in the start state $B$, we can only reach states $B$, $E$, and $F$. The other five states are inaccessible from the start state and may as well not be there.

We can often avoid the exponential blow-up by constructing the transition table for DFA $D$ only for accessible states $S$ as follows (lazy evaluation):
- **Basis step:** $S = \{q_0\}$ is accessible in DFA $D$.
- **Inductive step:** If $S$ is accessible, so are the states $\delta_D(S, a)$ for any $a \in \Sigma$​.

In this way, we obtain the “subset” DFA with accessible states only.

![image-20240318085616342](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318085616342.png)

![image-20240318085641876](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318085641876.png)

**Theorem 2.1** 

Let $D = (Q_D, \Sigma, \delta_D, \{q_0\}, F_D)$ be the DFA constructed from NFA $N = (Q_N, \Sigma, \delta_N, q_0, F_N)$ by the subset construction, then $L(D) = L(N)$​.

**Theorem 2.2**

A language $L$ is accepted by some DFA if and only if $L$ is accepted by some NFA.

### Bad Case for the Subset Construction

For DFA constructed by NFA, exponential growth in the number of states is possible.

**Example**

There is an NFA $N$ with $n + 1$ states that has no equivalent DFA with fewer than $2^n$ states.

![image-20240318090112972](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240318090112972.png)

Clearly, $L(N) = \{x_1c_2c_3 \cdots c_n | x \in \{0, 1\}^*, c_i \in \{0, 1\}\}$. Intuitively, a DFA $D$ that accepts $L(N)$ must remember the last $n$ symbols it has read.

Since there are $2^n$ bit sequences $a_1a_2 \cdots a_n$, if $D$ with fewer than $2^n$ states exists, then there would be some state $q$ such that $D$ can be in state $q$ after reading two different sequences of $n$ bits, say $a_1a_2 \cdots a_n$ and $b_1b_2 \cdots b_n$.

Since the sequences are different, there is an $i$ such that $a_i \neq b_i$. Suppose (by symmetry) that $a_i = 1$ and $b_i = 0$​.

Two cases will be considered:
1. If $i = 1$, i.e., the sequences are $1a_2 \cdots a_n$ and $0b_2 \cdots b_n$, then $q$ must be both an accepting state and a nonaccepting state.
2. If $i > 1$, i.e., the sequences are $a_1 \cdots a_{i-1}1a_{i+1} \cdots a_n$ and $a_1 \cdots a_{i-1}0b_{i+1} \cdots b_n$, then consider the state $p$ that $D$ enters after reading $a_1 \cdots a_{i-1}1a_{i+1} \cdots a_nc_1 \cdots c_{i-1}$ and $a_1 \cdots a_{i-1}0b_{i+1} \cdots b_nc_1 \cdots c_{i-1}$. Then $p$ must be both accepting and nonaccepting.

The claim follows by contradiction.

## Finite Automata with ϵ-Transition

### Use of ϵ-Transition

In order to add “programming convenience”, we will extend NFA to ϵ-NFA.

In transition diagrams of such NFA, the empty string ϵ is allowed as a label.

However, this new capability does not expand the class of language that can be accepted by finite automata.

**Example**

Design an automaton *A*3 accepting decimal numbers consisting of (1) an optional + or − sign, (2) a string of digits, (3) a decimal point, and (4) another strings of digits. One of the strings (2) and (4) is optional, but not both empty.

![image-20240323152040307](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240323152040307.png)

### Definition of ϵ-NFA

A nondeterministic finite automaton with $\epsilon$-transition is a 5-tuple $(Q, \Sigma, \delta, q_0, F)$, where:
- $Q$ is a finite set of states,
- $\Sigma$ is a finite set of input symbols (an alphabet),
- $\delta$ is a transition function from $Q \times (\Sigma \cup \{\epsilon\})$ to the powerset of $Q$,
- $q_0 \in Q$ is a start state,
- $F \subseteq Q$ is a set of final or accepting states.

### ϵ-Closures

Informally, the $\epsilon$-closures of a state $q$ is the set consisting of $q$ itself and all other states that can be reached by following transitions out of $q$ that are labeled with $\epsilon$. The recursive definition of the $\epsilon$-closures, denoted as $ECLOSE(q)$, is given below.

**Basis step:** $q \in ECLOSE(q)$.

**Inductive step:** If $p \in ECLOSE(q)$, then $\delta(p, \epsilon) \subseteq ECLOSE(q)$.

### Extended Transition Function

The transition function $\delta$ of an $\epsilon$-NFA can be extended to $\hat{\delta}$:

**Basis step:** $\hat{\delta}(q, \epsilon) = ECLOSE(q)$.

**Inductive step:** Suppose $w = xa$, then

$\hat{\delta}(q, w) = \bigcup_{r \in \delta(\hat{\delta}(q,x),a)} ECLOSE(r)$

where $\delta(S, a) = \bigcup_{p \in S} \delta(p, a)$​.

### Language of ϵ-NFA

The language of an $\epsilon$-NFA $A = (Q, \Sigma, \delta, q_0, F)$ is defined by

$L(A) = \{w | \hat{\delta}(q_0, w) \cap F \neq \emptyset\}$​

### Equivalence of DFA and ϵ-NFA

Given any $\epsilon$-NFA $E$, we can find a DFA $D$ that accepts the same language as $E$. The construction is very close to the subset construction, as the states of $D$ are subsets of the states of $E$.

Let $\epsilon$-NFA $E = (Q_E, \Sigma, \delta_E, q_0, F_E)$, we will construct an equivalent DFA $D = (Q_D, \Sigma, \delta_D, q_D, F_D)$.

Here is the detail of the construction:

- $Q_D = \{S | S \subseteq Q_E, S = ECLOSE(S)\}$
- $q_D = ECLOSE(q_0)$
- $F_D = \{S | S \in Q_D, S \cap F_E \neq \emptyset\}$
- For every $S \in Q_D$ and $a \in \Sigma$, $\delta_D(S, a) = \bigcup_{r \in \delta_E(S,a)} ECLOSE(r)$

where $\delta_E(S, a) = \bigcup_{p \in S} \delta_E(p, a)$.

**Theorem 2.3** 

A language $L$ is accepted by some $\epsilon$-NFA if and only if $L$​ is accepted by some DFA.

**Proof (if):** This direction is straightforward. Suppose $L = L(D)$ for some DFA $D$. Convert $D$ into an $\epsilon$-NFA $E$ by adding the transition $\delta_E(q, \epsilon) = \emptyset$ for all states $q$ in $D$.

**Proof (only-if):** Let $E = (Q_E, \Sigma, \delta_E, q_0, F_E)$ be an $\epsilon$-NFA. Apply the modified subset construction to produce the DFA $D = (Q_D, \Sigma, \delta_D, q_D, F_D)$. We show $\hat{\delta}_E(q_0, w) = \hat{\delta}_D(q_D, w)$ by induction on $|w|$.

**Basis step:** $\hat{\delta}_E(q_0, \epsilon) = ECLOSE(q_0) = q_D = \hat{\delta}_D(q_D, \epsilon)$.

**Inductive step:**
$$\hat{\delta}_E(q_0, xa) = \bigcup_{p \in \delta_E(\hat{\delta}_E(q_0,x),a)} ECLOSE(p) \quad (\text{definition of } \hat{\delta}_E)$$
$$= \bigcup_{p \in \delta_E(\hat{\delta}_D (q_D ,x),a)} ECLOSE(p) \quad (\text{induction hypothesis})$$
$$= \delta_D(\hat{\delta}_D(q_D, x), a) \quad (\text{modified subset construction})$$
$$= \hat{\delta}_D(q_D, xa) \quad (\text{definition of } \hat{\delta}_D)$$

## Regular Expressions

### Building Regular Expressions

**Inductive definition of regular expression (RE) and its language:**

**Basis step:**
- $\epsilon$ and $\emptyset$ are regular expressions.

  $L(\epsilon) = \{\epsilon\}$, $L(\emptyset) = \emptyset$.

- If $a \in \Sigma$, then $a$ is a regular expression.

  $L(a) = \{a\}$.

**Inductive step:**

- If $E$ is a regular expression, then $(E)$ is a regular expression. $L((E)) = L(E)$.

- If $E$ and $F$ are regular expressions, then $E + F$ is a regular expression. $L(E + F) = L(E) \cup L(F)$.

- If $E$ and $F$ are regular expressions, then $E.F$ is a regular expression. $L(E.F) = L(E) \cdot L(F)$.

- If $E$ is a regular expression, then $E^*$ is a regular expression. $L(E^*) = (L(E))^*$.

### Precedence of Regular Expression Operators

1. The star operator is of highest precedence.
2. Next in precedence comes the concatenation or dot operator.
3. Finally, all unions or plus operators are grouped with their operands.

### Languages Associated with Regular Expressions

**Example**

Write a regular expression for the set of strings that consist of alternating 0’s and 1’s.

$(\epsilon + 1)(01)^*(\epsilon + 0)$.

Find a regular expression for the language $L = \{w \in {0, 1}^* | w \text{ has no pair of consecutive zeros}\}$.

$(1 + 01)^*(0 + \epsilon)$
