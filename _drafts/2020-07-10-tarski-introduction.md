---
layout: single
title: "Introducing the Tarski Laplacian"
tags:
  - Research
---

Robert Ghrist and I have a new paper out---"Cellular Sheaves of Lattices and the Tarski Laplacian"---available on [arXiv](https://arxiv.org/abs/2007.04099). One *caveat* I should mention is that this is a pure math paper. But for those of you in machine learning, signal processing, complex systems etc. do not be intimidated---Rob and I did our best to keep the prerequisites to the minimum: category theory basics and some intuition about why cellular sheaves are important (e.g. from the [thesis](https://arxiv.org/abs/1303.3255) of Justin Curry)...and maybe some prior exposure to lattice theory (chapter 2 of [Roman](https://www.amazon.com/Lattices-Ordered-Sets-Steven-Roman-ebook/dp/B00FB32WVG/ref=sr_1_2?dchild=1&keywords=roman+lattices&qid=1594314322&s=books&sr=1-2) and the sections on Galois connections in [Davey & Priestly](https://www.amazon.com/Introduction-Lattices-Order-B-Davey/dp/0521784514) are good).

The problem the paper tackles is actually a very subtle one. Cellular sheaves are really nice and *homologically rich* if they take values in abelian things like vector spaces or inner-product spaces. That is to say, nice objects live above vertices, edges, simplices of the base space of the sheaf (i.e. stalks are in an abelian category). As soon as we make the relaxation that stalks are just sets, we lose a lot of structure because there is no natural sheaf cohomology.

> Sheaf cohomology is a compression that collapses all the data over a topological space — or cell complex — to a minimal collection that entwines with the homological features of the base space.

These sorts of sheaves (i.e. sheaves valued in sets) are very important, for example, in the work of [Goguen](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.52.4296), but are also implicit in the theory of Reeb graphs studied in topological data analysis (TDA).

Luckily, the work of [Marco Grandis](http://www.dima.unige.it/~grandis/rec.public_grandis.html) sets the stage for a homological theory of cellular sheaves taking values in categories with more structure than plain-old sets, but less than, say, inner-product spaces. In this paper, we explore sheaves valued in lattices, i.e. partially ordered sets with meets $\wedge$ (i.e. infs) and joins $\vee$ (i.e. sups). *De facto* you only have limits here. But you can do more with the right operator that acts on cochains of the sheaf which we dub *the Laplacian*:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">here&#39;s the idea:<br>we define a Laplacian -- an endomorphism on 0-cochains (data distributions over vertices).<br>we argue that it &quot;works&quot; like a Laplcian should.<br>then we try to do harmonic flow. <br>8/</p>&mdash; ProfGhristMath (@robertghrist) <a href="https://twitter.com/robertghrist/status/1281251978170044419?ref_src=twsrc%5Etfw">July 9, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The **Tarski Laplacian** in degree $k$ is the order-preserving map, $L_k: C^k(X;\mathcal{F}) \longrightarrow C^k(X;\mathcal{F})$ acting on a $k$-cochain $\mathbf{x}$ and $k$-cell $\sigma$ via


$$
\left( L \mathbf{x} \right)_{\sigma} \triangleq \bigwedge_{\tau \in \delta \sigma } 
\mathcal{F}_{\sigma \trianglelefteq \tau}^{\tiny \bullet} 
  \left(
    \bigwedge_{\sigma' \in \partial \tau} 
    \mathcal{F}_{\tiny \bullet\: \normalsize\sigma' \trianglelefteq\tau}~x_{\sigma'}   
  \right)
$$


There is a lot to unpack here.  And everything is clearly explained in the paper. But here, we can think of the Tarski Laplacian as a diffusion operator---a combination of mixture and expansion of local states with neighbors.

We develop competing "cohomology" theories of lattice-valued sheaves in the paper, the cleanest of which is given by the fixed point theory of the Tarski Laplacian. It agrees in degree $0$ with the global sections of the sheaf:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">main theorem: for lattice-valued sheaves over a cell complex, the fixed point set of (I-L), where L is this new *Tarski Laplacian* is the global sections of the sheaf. <br>10/</p>&mdash; ProfGhristMath (@robertghrist) <a href="https://twitter.com/robertghrist/status/1281251980061614081?ref_src=twsrc%5Etfw">July 9, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

In other words, we use the Hodge Theorem


$$
\mathrm{Ker}\,L_\bullet \cong H^\bullet(C^\bullet)
$$


as a springboard to define cohomology in this non-abelian context. The work of [Jakob Hansen](https://www.math.upenn.edu/~jhansen/) expores a Hodge theory for cellular sheaves of inner-product spaces. Hodge theory of lattice-valued sheaves is...tricky. Good news: the existence of cohomology lattices is guaranteed by the Tarski Fixed Point Theorem:

> The fixed point set of an order-preserving endomorphism of a complete lattice is a complete lattice.

Henceforth, we can generalize Tarski cohomology to higher degrees:


<blockquote class="twitter-tweet"><p lang="en" dir="ltr">but the Tarski Laplacian generalizes easily to higher dimensional cochains...<br>and the fixed point set of (I-L) is a complete quasi-sublattice of the higher cochain space.<br>so...<br>let&#39;s call this the *Tarski cohomology*<br>13/</p>&mdash; ProfGhristMath (@robertghrist) <a href="https://twitter.com/robertghrist/status/1281251983169650688?ref_src=twsrc%5Etfw">July 9, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Problems arise, however, and they are discussed in detail. Two other approaches: Grandis cohomology and upper/lower Hodge cohomology solve some problems but introduce others. All in the paper.

Where are the applications? Graph signal processing (GSP) is the first place to look which relies exclusively on the spectral properties of the combinatorial graph Laplacian. There are a lot of things you can do with the combinatorial graph Laplacian, including, but limited to, consensus, flocking, image processing, distributed optimization, and graph convolutional neural networks (GCNNs). At least in theory, you can do all these things and maybe more with the Tarski Laplacian.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">new paper out with <a href="https://twitter.com/robertghrist?ref_src=twsrc%5Etfw">@robertghrist</a>: ever wondered if lattice theory and sheaf theory had a baby (and no i&#39;m not talking about topoi...) that was raised by GSP??? look no further! applications *in progress* including consensus, distributed opt., GNNs &amp; more<a href="https://t.co/U6GBvavZcQ">https://t.co/U6GBvavZcQ</a> <a href="https://t.co/fTu5OHSmEu">pic.twitter.com/fTu5OHSmEu</a></p>&mdash; Hans Riess (@hansmriess) <a href="https://twitter.com/hansmriess/status/1281258091804340234?ref_src=twsrc%5Etfw">July 9, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Please enjoy our paper, ["Cellular Sheaves of Lattices and the Tarski Laplacian,"](https://arxiv.org/abs/2007.04099) and feel free to send either myself or Rob any thoughts or suggestions by email.