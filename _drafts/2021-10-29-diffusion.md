---
layout: single
title: "The Tarski Laplacian through Examples"
tags:
  - Research
  - Databases
  - Tropical Geometry
---

# The Tarski Laplacian through Examples

The purpose of this post is to provide a quick and dirty introduction to the Tarski Laplacian for a general audience interested in machine learning and data science. As much as I hate to admit it, our [paper](https://www.hansriess.com/files/tarski-laplacian) to appear in *Homotopy, Homology, and Applications* seems unmotivated without prior exposure to cellular sheaves---or at least the topological data analysis that motivates them. To be sure, our work on sheaf Laplacains is mathematically interesting in its own right because it is an attempt to generalize the Hodge complex--as well as the Hodge Laplacian of course--in the new world of lattice theory.

## Databases

For novices, a lattice is an ordered set with two distict merging operations call *join* and *meet*. If this sort of language reminds you of databases, it should. Lattice arise in a nice way from relations which are really just binary dataframes. Consider an example. Let $X$ be a set of objects (**rows** in a dataframe, say IDs of Netfix users). Let $Y$ be a set of attributes (**columns** in a dataframe, say IDs of movies). Then, the collection of subsets of $X$ and the collection of subset of  $Y$ form lattices. They are just the powersets $2^X$ and $2^Y$. If you would like, we can think of elements of $2^X$ as a number of rows of a dataframe and elements of $2^Y$ as a number of columns. If we simultaneously select and number of columns and a number of rows , we obtain a "rectangle" element of the product lattice $2^X \times 2^Y$. 

<!--INSERT FIGURE OF DATABASE HERE-->

If a dataframe is a collection of boxes, it's what we put in the boxes that matters the most. We can think of a dataframe as a function $I: X \times Y \to \{\mathtt{true},\mathtt{false}\}$  that returns $\mathtt{true}$ at entry $(x,y)$ if object $x$ has attribute $y$ and is $\mathtt{false}$ otherwise. If you would like, you may think of $I$ as a relation $I \subseteq X \times Y$. As a remark, not only binary data entries can be encoded in this way. For example, by binning, you can encode numerical data as well at various resolutions. You could encode someone's birthdate by defining an attribute for each decade.

Returning to "rectangles", what sorts of "rectangles" are special? Here is one answer. Suppose $(\sigma, \tau)$ is a rectangle, i.e. a subset of rows $\sigma$ and columns $\tau$. Then, $(\sigma, \tau)$ is distinguished if for every row $x \in \sigma$ of the rectangle, $I(x,y)$ is true for *every* column of $\tau$  and, conversely, for every column $y \in \tau$, $I(x,y)$ is true for *every* row of $\sigma$. Some notation will be helpful in the future. Let $\sigma^{\uparrow} = \{y \in Y:  I(x,y) \forall x \in \sigma\}$ and let $\tau^{\downarrow} = \{x \in X: I(x,y)\forall y \in \tau \}$. Then distinguished rectangles (called "concepts" by Wille) are **fixed points** in the sense that a distinguished rectangle $(\sigma, \tau)$ satisfies $\sigma^{\uparrow \downarrow} = \sigma$ and  $\tau^{\downarrow \uparrow} = \tau$. As a consequence of a folk theorem often associated with Alfred Tarski, the set of distinguished rectangles associated to a given relation $I$ forms a lattice.

<!--INSERT FIGURE OF DISTINGUISHED RECTANGLES HERE-->

This view of dataframes has implications in privacy. As personal data is becoming more widely available, data scientists need ways to analyze data collected on individuals (e.g. patients in a hospital) withough revealing their identities. A standard approach is to anonymize datasets in such a way that minimizes the loss of information. How do distinguished rectangles come into play? Distinguished rectangles are rectangles $(\sigma, \tau)$ for which a subgroup of individuals $\sigma$ can be *uniquely* identified by $\tau$...and vise versa. The widely-known $k$-anonymity property can be stated concisely: a dataframe $I$ has the $k$-anonymity property if for every distinguished rectangle $(\sigma, \tau)$, $\sigma$ has at most $k-1$ rows.  For those with expertise in lattice theory, this idea seems to generalize to arbitrary lattices with via a notion of rank.

Suppose, now, we no long care about a single dataframe $I: X \times Y \to \{\mathtt{true}, \mathtt{false} \}$, but we worry about an entire *database*, which is precisely a set of dataframes $\mathcal{D} = \{ I_{ij}: X_i \times X_j \to \{ \mathtt{true}, \mathtt{false} \}\}_{ij \in \mathcal{E}}$. In databases, we often share 

