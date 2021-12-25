---
layout: single
title: "An Economical Guide to Galois Connections via Meta-Preferences"
date: 2021-04-09
header:  
  teaser: galois.jpg
tags:
  - Lattice Theory
  - Economics
---

Of course, I half-heartedly apologize for the double entendre, but *really* it is my hope that this post will be both a relatively cheap introduction to Galois connections and be of help, especially, to economists.

### Preference Relations

Nobel Memorial laureate Paul Samuelson is quoted that "economics is a choice between *alternatives* *all the time*." As a mathematician I might caricature the entire field of economics---hopefully not to the offense of actual economists---as the **study of dynamical systems supported on spaces of choices.** Mathematically (again doing disservice to those who actually study dynamics), a dynamical system is a set of states with maybe a map specifying how to get to the next state. A **choice space** is a set of **alternatives** (that is, things to choose from) $X$ and a collection of feasible sets $D(X) \subseteq 2^X$ where $2^X$ is the powerset (or, set of all subsets) of $X$. 

A choice function $C: D(X) \to 2^X$ assigns to a feasible set $A$ , one or more choices $C(A) \subseteq A$ . Under certain assumptions---such as that $D(X)$ being *down-closed* (meaning if $A \in D(X)$ and $B \subseteq A$ , then $B$ in $D(X)$)---we can say $C$ is a map $C: D(X) \to D(X)$.

A **preference profile** is a set of alternatives $X$ with a binary relation $R \subseteq X \times X$. It is convenient to interpret preferences as either *strong* (often denoted $P$) or *weak* (often denoted $W$). For example, $x~W~y$ might mean that $x$ is at least as good as $y$. A strong relation $x~P~y$ might mean that $x$ (strongly) preferred over $y$. (We can write either $(x,y) \in R$ or $x~R~y$ depending on context.)

Given a choice space $(X, D(X))$ and choice function $C: D(X) \to D(X)$ we can construct a natural weak preference: we say that $a~W~b$ (*$a$ is weakly preferred to $b$*) if there is a feasible set $A \in D(X)$ such that $a \in C(A)$ and $b \in A$. Likewise, there is a natural strict preference: $a~P~b$ (*$a$ is strictly preferred to $b$*) if there is a feasible set $A \in D(X)$ such that $a \in C(A)$ and $b \in A \setminus C(A)$. Conversely, given a weak (or strict) preference $W \in X \times X$ , we can construct an  "optimal" choice function,
$$
C(A) = \{a \in A~\vert~\forall~b \in A,~a~W~b  \}.
$$
Note, however, an assignment of a choice function to a preference profile is not unique. One takeaway is that it is fruitful to think about preferences both as relations and as choice functions.

Economists are known to put  requirements on what properties relations ought to---morally or empirically---satisfy. Here are some examples:

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

Of all possible relations, a *preorder* might actually the most sensible to model *weak* human preferences. Recall, a preorder satisfies (i) reflexivity and (ii) transitivity. Reflexivity embodies the notion of a weak preference as opposed to a strong preference; it is not so important in it's own right 

Transitivity is a curious assumption that is nearly ubiquitous in economics. Phycologists and behavioral economists have debated for several decades whether human preferences are intrinsically transitive or rather if the assumption of transitivity is too convenient to abandon. Of note is seminal work ([Tversky, 1969](https://psycnet.apa.org/record/1969-06371-001)) that demonstrated conditions under which individuals behave in an intransitive manner; moreover, their behavior is both predictable and consistent. However, even as there has been recent critique of the 1969 paper, there is earlier competing evidence (dissertation of MacCrimmon, 1965) that individuals modify their preferences to be transitive, perhaps an early example in which *dynamics on a space meta-preferences play a role at forming preferences.* More on meta-preferences later.

A grave economic consequence of intransitive preferences is the so-called *money pump* phenomenon in which, through a series of  exchanges, an individual can *rationally* obtain the alternative she originally possessed, yet spend a sum of money in exchanging alternatives. Preordered sets are particularly nice from the mathematical perspective because that are equivalent to the notion of *thin categories* (here, we are referring to the mathematical field of [Category Theory](https://en.wikipedia.org/wiki/Category_theory)): transitivity corresponds to composing arrows, reflexivity corresponds to the identity arrow. In some sense, a category is the least restrictive place where it is possible to "do mathematics." But why not impose the sort additional structure you get from a total order or poset?

Total orders are traditionally more popular among economists, the principle reason being that the requirement of comparability guarantees that there is a (non-unique) utility function $u: X \to \mathbb{R}$ such that $u(x) \geq u(y)$ if and only if $x~W~y$. In essence, the structure of a total order eliminates any careful study of a preference relation: all information is contained in the usual order on the real line. 

From a data science perspective, total orders are problematic as well. Preferences truly only exist when they are revealed. This is not ideal for a few reasons. You could ask user to submit a survey of their preferences on a set $n$ different alternatives, but this would require on the order $\sim 2^n$ survey questions. For example, if $n = 40$, then a survey would require the user to vote on the order of 1 trillion times! Even when taking into account the comparability of every pair of alternatives, reflexivity, and transitivity, it is not much better. Another reason, alternatives that are "far" from each other in a relation will, likely, never be compared. What ice cream truck will sell [tripe](https://en.wikipedia.org/wiki/Tripe), after all? Furthermore, alternatives in different categories may never be compared. Imagine going to brunch and deciding between a juicy burger and a stack of blueberry pancakes: what you order for brunch will not have so much to do with your preference of pancakes over burgers, but your preference of breakfast over lunch. We will come back to this example later.

Finally, a word on posets. In a poset, the additional axiom of *anti-symmetry* may be too stringent to model human preferences. This axiom says that if $x~W~y$ and $y~W~x$, then $x$ and $y$ are equal. It is absurd to regard alternatives about which an agent is indifferent over as *equal.* This *de facto* is negating the possibility of indifference. Indifference is notably different that incomparability. That an agents reveals (weak) preference of $x$ over $y$ and vise versa in *not* equivalent to not revealing any preference at all.

### Lattices

**Lattices** are posets (partially ordered sets) such that for any two elements $x, y \in L$ there are unique elements $x \vee y, x \wedge y \in L$ such that $x \vee y$ is the least upper bound of $x$ and $y$ and $x \wedge y$ is the greatest lower bound; the symbol $\vee$ is called **join**, the symbol $\wedge$ is called **meet**. Often the greatest and least elements of a lattice are written as $\top$ and $\bot$ respectively. There are many familiar examples of lattices: given any set, its powerset forms a lattice with the lattice operations comprising of union ($\cup$) and intersection ($\cap$). There are richer classes of lattices living inside powersets: for example, any subset $L \subseteq 2^X$ is a lattice, or sometimes called a *lattice family*, if for any $A, B \subseteq L$ there is a smallest (dually greatest) set $A \vee B$ (dually $A \wedge B$) such that $A \vee B \supseteq A, B$ (dually $A \wedge B \subseteq A, B$). Additional examples we can draw from combinatorics, linear algebra, logic, and even topology.

<img src="\images\lattice.png" alt="lattice" style="zoom:50%;" />

Lattices apt structures for modeling hierarchies. Furthermore, they are convenient because you can combine lattice elements in two different ways that are dual to one another (whereas, in general you cannot "add" preference relations). Lattices are the right tool for modeling preference that are hierarchical in nature. Now you might be saying, "Wait! You just told me that preorders are the right relation to model human preferences!" Of course you are in the right to complain. But there might be a case that *lattices are the canonical structure for modeling meta-preferences*.

Put plainly, **meta-preferences** are preferences about preferences. Going back to our example about changing preferences to be transitive: this example suggests that baked in our sense of what our preferences ought to be is that they should be transitive. A meta-preference is in essence a moral code which may govern not only what I want to want for myself, but what I want others to want. So one definition of a **meta-preference profile** is a binary relation on the set $\mathrm{Rel}(X)$ of all binary relations on a set of alternatives $X$; explicitly,
$$
Q \subseteq \mathrm{Rel}(X) \times \mathrm{Rel}(X).
$$
Another definition of meta-preferences goes back to the brunch example. I may have a preference of Eggs Benedickt over French Toast, and a preference of a Cobb Salad over a Cheeseburger, but I can have a meta-preference of $\{ \text{Benedikt, French}\}$ over $\{ \text{Salad}, \text{Burger} \}$. As pointed out earlier, I could have a meta-preference of breakfast over lunch without having a preference of, say French toast over a burger. So a second definition of a **meta-preference profile** is a binary relation on the choice spaces $D(X)$ of a set of alternatives $X$; explicitly,
$$
Q \subseteq D(X) \times D(X).
$$

### Galois Connections

Historically speaking, it may have been Richard Dedekind who wrote the first paper explicitly on lattices around the turn of the 20th century. However, perhaps the most important construction in lattice theory, the [*Galois connection*](https://ncatlab.org/nlab/show/Galois+connection), was essentially invented by Évariste Galois in 1830. Galois also is often credited at inventing group theory (the abstract study of symmetries) at the same time. Both groups and Galois connections were invented as abstract tools to reason about polynomials.

Consider posets $(P, \leq)$ and $(Q,\sqsubseteq)$. An an order-reversing map is a map $\varphi: P \to Q$ such that if $x \leq y$, then $\varphi(X) \sqsupseteq \varphi(y)$. A Galois connection between two posets $(P, \leq)$ and $(Q,\sqsubseteq)$  is a pair $(f_\ast, f^\ast)$ of order-reversing  maps,

$$
f_\ast: P \leftrightarrows Q: f^\ast
$$
such that $f_\ast (p) \sqsupseteq q$ if and only if $f^\ast(q) \geq p$ .

In 1982, a mathematician Rudolph Wille presented a [paper](https://link.springer.com/book/10.1007/978-94-009-7798-3), "Restructuring Lattice Theory: An Approach Based on Hierarchies of Concepts," connecting Galois connections to binary relations. He is often credited for first "applying lattice theory" because of course binary relations are everywhere (e.g. databases, systems theory, linguistics etc...). Given a binary relation $R \subseteq X \times Y$, Wille constructs a lattice he calls the **concept lattice** describing hierarchies of concepts (i.e. subsets of $X$ or $Y$ ) within a relation.

A concept lattice comes from a Galois connection,
$$
R_\ast: 2^X \leftrightarrows 2^T: R^\ast
$$
given by $R_\ast(A) = \{y \in Y: (x,y) \in R~\text{for all}~x \in A \}$ and $R^\ast(B) = \{x \in X: (x,y) \in R~\text{for all}~y \in B \}$. We can interpret $R_\ast( -)$ as  *intent* and $R^\ast(-)$ as *extent*. A **concept** is a pair $(A,B)$ where $A$ is a subset of $X$ and $B$ is a subset of $Y$ such that
$$
R_\ast(A) = B~\text{if and only if}~A = R^\ast(B)
$$
The set of all concepts associated to a relation,
$$
\mathrm{Concept}(R) = \{ (A,B): R_\ast(A) = B,~R^\ast(B) = A \}
$$
form a lattice (this is non-obvious, something you need to prove) called the **concept lattice**. 

Let's look at an example. Suppose we have a relation, say of NBA basketball players and facts about them, $R \subseteq X \times Y$. We can represent this relation by a table:

<img src="\images\nba-table.png" alt="nba-table" style="zoom:48%;" />

Now we may calculate the fixed points $\mathrm{Fix}(R^\ast R_\ast) = \{A: R^\ast R_\ast (A) = A \}$ which form the concept lattice. (I might have cheated a bit, but you can show that the definition of the concept lattice above is equivalent to $\mathrm{Fix}(R^\ast R_\ast)$.) There are software packages out there to do this somewhat automatically (e.g. the python package [concepts](https://github.com/xflr6/concepts)). We obtain the following concept lattice:

<img src="\images\nba-concepts-obj.svg" style="zoom: 150%;" />

How do we interpret this lattice? If we take the meet ($\wedge$) of, say $A$ and $B$, this is equivalent to taking the union of rows A and B (why union, not intersection?...because the $R^\ast$, $R_\ast$ maps are order-reversing). If we take the join ($\vee$) of A and B, this is equivalent to take the intersection of rows A and B which corresponds to the attribute "forward" i.e. the concept Antetokounmpo, Butler and Durrant.

Now, back to preference relations. As we have seen earlier, a choice function $C: D(X) \to 2^X$ begets a unique weak preference relation. In a similar vein, any preference relation $W \subseteq X \times X$ begets a *unique meta-preference relation*, $\mathrm{Concept}(W)$ which is a  *lattice* that can be viewed also as a binary relation $\mathrm{Concept}(W) \subseteq  2^X \times 2^X$. This is significant because we have put a *lattice structure on meta-preferences*. In particular, individuals can exchange meta-preferences to find their meet or join i.e. their *least common denominator*--what they have in common--or form a *compromise*--the effective feasible sum of their meta-preferences.

So maybe this is the very beginning of a argument that *lattices are the canonical structure for modeling meta-preferences*. 

