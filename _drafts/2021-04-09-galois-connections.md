---
layout: post
title: "An Economical Guide to Galois Connections"
---



# An Economical Guide to Galois Connections

Of course, I half-heartedly apologize for the double entendre, but *really* it is my hope that this post will be both (i) be of help to economists who want to learn some basics of order theory, and (ii) a short and easy introduction to the theory of Galois connections using human preferences and choices as a springboard. Here we go!

### Modeling human preferences with relations

Nobel Memorial laureate Paul Samuelson is quoted that "economics is a choice between *alternatives* *all the time*." As a mathematician I might caricature the entire field of economics---hopefully not to the offense of actual economists---as the **study of dynamical systems supported on spaces of choices.** Mathematically (again doing disservice to those who actually study dynamics), a dynamical system is a set of states with maybe a map specifying how to get to the next state. A **choice space** is a set of **alternatives** (that is, things to choose from) $X$ and a collection of feasible sets $D(X) \subseteq 2^X$ where $2^X$ is the powerset (or, set of all subsets) of $X$. 

A choice function $C: D(X) \to 2^X$ assigns a feasible set $A$ to one or more choices $C(A) \subseteq A$ . Under certain assumptions---such as that $D(X)$ is *down-closed* (meaning if $A \in D(X)$ and $B \subseteq A$ , then $B$ in $D(X)$)---we can say $C$ is a map $C: D(X) \to D(X)$.

A **preference profile** is a set of alternatives $X$ with a binary relation $R \subseteq X \times X$. It is convenient to interpret preferences as either *strong* (often denoted $P$) or *weak* (often denoted $W$). For example, $x~W~y$ might mean that $x$ is at least as good as $y$. A strong relation $x~P~y$ might mean that $x$ (strongly) preferred over $y$. (We can write either $(x,y) \in R$ or $x~R~y$ depending on context.)

Given a choice space $(X, D(X))$ and choice function $C: D(X) \to D(X)$ we can construct a natural weak preference: we say that $a~W~b$ (*$a$ is weakly preferred to $b$*) if there is a feasible set $A \in D(X)$ such that $a \in C(A)$ and $b \in A$. Likewise, there is a natural strict preference: $a~P~b$ (*$a$ is strictly preferred to $b$*) if there is a feasible set $A \in D(X)$ such that $a \in C(A)$ and $b \in A \setminus C(A)$. Conversely, given a weak (or strict) preference $W \in X \times X$ , we can construct an  "optimal" choice function,
$$
C(A) = \{a \in A~\vert~\forall~b \in A,~a~W~b  \}.
$$
Note, however, an assignment of a choice function to a preference profile is not unique. One takeaway is that it is fruitful to think about preferences both as relations and as choice functions.

Economists are known to put stringent requirements on what properties relations ought to---morally or empirically---satisfy. Here are some examples:

1. Reflexivity: $(x,x) \in R$ .
2. Anti-symmetry: if $(x,y) \in R$ and $(y,x) \in R$, then $x = y$.
3. Transitivity: $(x,y) \in R,~(y,z) \in R~\Rightarrow~(x,z) \in R$.
4. Symmetry: if $(x,y) \in R$, then $(y,x) \in R$.
5. Comparability: (or *completeness* to economists): for all $x, y \in X$ with $x \neq y$, $(x,y) \in R$ or $(y,x) \in R$.

Mathematicians, in their disparate idiosyncrasies, have special names for relations satisfying any number of these properties:

* A *poset* or partially-ordered set satisfies 1, 2, & 3.
* A *total order* satisfies 2, 5, & 3.
* A *preorder* satisfies 1 & 3.
* An *equivalence relation* satisfies 1, 4, & 3.

We may collect the various types of relations satisfying various requirements in a table.  In fact, any relation $R \subseteq X \times Y$  you can represent as a table with one row for each $x \in X$ and one column for each $y \in Y$. (Here, at the risk of mass confusion we have a relation describing various classes of relations). We'll come back to this table later.

|                      | Reflexivity | Anti-symmetry | Transitivity | Symmetry | Comparability |
| -------------------- | ----------- | ------------- | ------------ | -------- | ------------- |
| Graph                | True        |               |              |          |               |
| Digraph              |             |               |              |          |               |
| Preorder             | True        |               | True         |          |               |
| Equivalence Relation | True        |               |              |          |               |
| Poset                | True        | True          | True         |          |               |
| Total Order          | True        | True          | True         |          | True          |

Of all possible relations, a *preorder* might actually the most sensible to model *weak* human preferences. Recall, a preorder satisfies (i) reflexivity and (ii) transitivity. Reflexivity embodies the notion of a weak preference as opposed to a strong preference; it is not so important in it's own right 

Transitivity is a curious assumption that is nearly ubiquitous in economics. Phycologists and behavioral economists have debated for several decades whether human preferences are intrinsically transitive or rather if the assumption of transitivity is too convenient to abandon. Of note is seminal work (Tversky, 1969) that demonstrated conditions under which individuals behave in an intransitive manner; moreover, their behavior is both predictable and consistent. However, even as there has been recent critique of the 1969 paper, there is earlier competing evidence (MacCrimmon, 1965) that individuals modify their preferences to be transitive, perhaps an early example in which *dynamics on a space meta-preferences play a role at forming preferences.* 

A grave economic consequence of intransitive preferences is the so-called *money pump* phenomenon in which, through a series of  exchanges, an individual can *rationally* obtain the alternative she originally possessed, yet spend a sum of money in exchanging alternatives. Preordered sets are particularly nice from the mathematical perspective because that are equivalent to the notion of *thin categories* (here, we are referring to the mathematical field of Category Theory): transitivity corresponds to composing arrows, reflexivity corresponds to the identity arrow. In some sense, a category is the least restrictive place where it is possible to "do mathematics." But why not impose additional structure?

Total orders are more popular among economists, the principle reason being that the requirement of comparability guarantees that there is a (non-unique) utility function $u: X \to \mathbb{R}$ such that $u(x) \geq u(y)$ if and only if $x~W~y$. In essence, the structure of a total order eliminates any careful study of a preference relation: all information is contained in the usual order on the real line. 

From a data science perspective, total orders are problematic as well. Preferences truly only exist when they are revealed. This is not ideal for a few reasons. You could ask user to submit a survey of their preferences on a set $n$ different alternatives, but this would require on the order $\mathcal{O}(2^n)$ survey questions. For example, if $n = 40$, then a survey would require the user to vote on the order of 1 trillion times! Even when taking into account the comparability of every pair of alternatives, reflexivity, and transitivity, it is not much better. Another reason, alternatives that are "far" from each other in a relation will, likely, never be compared. What ice cream truck will sell haggis, after all? Furthermore, alternatives in different categories may never be compared. Imagine going to brunch and deciding between a juicy burger and a stack of blueberry pancakes: what you order for brunch will not have so much to do with your preference of pancakes over burgers, but your preference of breakfast over lunch. 

Finally, a word on posets. Posets (a.k.a. partially ordered sets) are much more popular in mathematics (esp. in combinatorics) than preorders, but the additional axiom of *anti-symmetry* may be too stringent to model human preferences. This axiom says that if $x~W~y$ and $y~W~x$, then $x$ and $y$ are equal. It is absurd to regard alternatives about which an agent is indifferent over as *equal.* This *de facto* is negating the possibility of indifference. Indifference is notably different that incomparability. That an agents reveals (weak) preference of $x$ over $y$ and vise versa in *not* equivalent to not revealing any preference at all.

### Lattices and Galois connections

Galois connections 

