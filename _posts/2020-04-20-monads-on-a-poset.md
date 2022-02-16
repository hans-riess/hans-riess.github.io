---

layout: single
title: "Monads on a Poset"
date: 2020-04-20
header:  
  teaser: may.jpg
tags:
  - Lattice Theory
  - Category Theory
---

In this post, I will briefly describe a pleasant observation I made this morning about monads on a poset, that is, a partially ordered set. In order to get there, I will have to say what exactly are *monads* and *posets.*

Monads are curious objects. I recently came across them while preparing a talk about the first few sections of Peter May's "Geometry of Infinite Loops Spaces." In that paper, he defines a new structure called an operad which is essentially a way to formalize tree-like compositions of maps, $f: X^{\otimes n} \rightarrow X$, for different $n$ in a some monoidal category (if you don't know what that is, think of $(\mathsf{Vect}, \otimes, \mathbf{0})$, the category of vector spaces, with the tensor product and the zero vector space). Anyways, in May's paper, he describes a 1-to-1 correspondence between *algebras over an operad* and *algebras over monads*. That correspondence isn't important here, but it is important to note that monads, for some reason, seems to creep up everywhere. I don't think they are well known amongst applied people who use a lot of fancy algebra like myself. Personally, I hadn't been exposed to them even after a few years of reading some heavy-categorical papers in applied algebraic topology, lattice theory etc. Monads seem, however, to be fairly commonplace in certain theoretical computer science communities especially those Haskellites. You know who you are.

A poset, say $P$, is set with a *anti-symmetric, reflexitive,* and *transitive* binary relation, $\preceq$. Sometimes it is easier to view a poset not as a set but as a category, $\mathsf{P}$. The objects of this category are the elements of $P$. Morphisms? Given $x, y \in \mathsf{P}$, $\mathrm{Hom}_{\mathsf{P}}(x,y)$ if $x \preceq y$ and $\emptyset$ otherwise.

This is kind of nice, because if you consider a functor,


$$
F: \mathsf{P} \rightarrow \mathsf{Q}
$$


this is just saying that $F$ is an *order-preserving* or *monotone maps* from poset $P$ to poset $Q$. It is particularly nice, when you consider an adjunction between posets,


$$
F \vdash G: \mathsf{P} \longleftrightarrow \mathsf{Q}
$$


This means, that


$$
\mathrm{Hom}_{\mathsf{Q}} \left(F x, y \right) \cong \mathrm{Hom}_{\mathsf{P}}\left(x, G y \right)
$$


But this is just,


$$
\begin{align}
F(x) \preceq y && \text{iff}&&&x \preceq G(y)
\end{align}
$$

since every arrow in a poset category is either a singleton or empty. This is called a *Galois connection* in the order theory literature, but really, it is just an adjunction. From an adjunction, we obtain two natural transformations, called the *unit*,

$$
\eta: 1_{\mathsf{P}} \Rightarrow G F
$$


and *counit*,


$$
\varepsilon: FG \Rightarrow 1_{\mathsf{Q}}
$$
These are constructed by essentially replacing $y$ with $F x$ or replacing $x$ with $G y$  in the Hom-set definition of an adjunction and a little bit of work.

Okay. So what is a monad?  Well, we already have an example, the functor $G F: \mathsf{P} \rightarrow \mathsf{P}$. Of course, we could have replaced $\mathsf{P}$ with any category and $F \vdash G$ with any adjunction. Here is the definition: a *monad* is a triple $(T, \mu, \eta)$ where $T$ is an endofunctor $T: \mathsf{C} \rightarrow \mathsf{C}$ , $\mu$ is a natural transformation, $\mu: T \circ T \Rightarrow T$, and $\eta$ is a natural transformation, $\eta: 1_{\mathsf{P}} \Rightarrow T$, such that $(T, \mu, \eta)$ satisfy a number of commutative diagrams describing an associativity property of $\mu$ and an identity property of $\eta$.

**Proposition.** Any adjunction $F \vdash G: \mathsf{C} \rightarrow \mathsf{D}$ gives rise to a monad $(G F, \eta, \mu)$.

*Proof*. $G F: \mathsf{C} \rightarrow \mathsf{C}$ is an endofunctor. The unit of the adjunction, $\eta: 1_{\mathsf{P}} \Rightarrow G F$, is also the unit of the monad. Let $\varepsilon$ bet the counit of the adjunction. Then, define $\mu$ as follows,

$$
\mu : G F G F \Rightarrow GF
$$

$$
\mu: GFGF x \mapsto G \circ \varepsilon FG (F x) = GF x
$$


$\blacksquare$

What, then, is a monad on a poset $\mathsf{P}$?  It is an endofunctor, $T: \mathsf{P} \rightarrow \mathsf{P}$, with natural transformations, $\eta: 1_{\mathsf{P}} \Rightarrow T$ and $\mu: T \circ T \Rightarrow T$. Being a functor implies $T$ is an monotone map on $P$. The transformation $\eta$ implies that $T$ is *inflationary*, that is, $T(x) \succeq x$. Finally, any such transformation $\mu$ implies there is a map


$$
T T x \xrightarrow{\mu} Tx
$$


which means that $T^2(x) \preceq T(x)$. However, $T(x) \preceq T(x')$ and $T(x) \succeq x$ implies that $T^2(x) \preceq x$. This implies that $T^2(x) = T(x)$, or $T^2 = T$. That is, $T$ is *idempotent*! Hence, we have a proposition.

**Proposition.** A monad $(T, \mu, \eta)$ on a poset $\mathsf{P}$ is that same as a monotone, inflationary, idempotent map, $T: P \rightarrow P$.

Together with our proposition about constructing a monad from an adjunction, we have the following corollary, whose proof is now trivial.

**Corollary.** Let $(F, G): P \longleftrightarrow Q$ be a Galois connection between posets $P$ and $Q$. Then, the following identities hold:

* For all $x \in P$ and $y \in Q$,


$$
\begin{align}
G F (x) \succeq x && \text{and} && F G (y) \preceq y
\end{align}
$$

* $G F GF = GF$. Furthermore, by considering the dual poset, $P^{\mathrm{op}}$, which is just *reversing the arrows*  and the corresponding Galois connection, $G^{\mathrm{op}} \vdash F^{\mathrm{op}}: Q^{\mathrm{op}} \leftrightarrow P^{\mathrm{op}}$, we have, by this dually, $FG FG = FG$.

These are the two most important identities for a Galois connection in order theory. Yet, if we view a Galois connection from a categorical lens, this result is completely formal. I thought this observation was worth sharing and I hope you did too. Until next time.