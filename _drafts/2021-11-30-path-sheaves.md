---
layout: single
title: "Path Sheaves: A Lattice-Theoretic Approach"
date: 2021-08-15
header:
  teaser: 
tags:
  - Lattice Theory
  - Sheaves
  - Criticism
---

In their recent paper "Path Optimization Sheaves," Moy et al. define a notion of a **path sheaf** in order to posit path-finding algorithms from a sheaf-theoretic point-of-view, such as Dijkstra's algorithm. They define a weighted version of the path sheaf which they call the **distance path sheaf**.

If you're anything like me, you probably has to google "Dijkstra's algorithm" and if you're *really* like me you realized you have used it before. Here's the setup: given a graph $G = (V,E)$​,  Dijkstra finds the shortest path between a source node $v_S \in V$​ and a target node $v_T \in V$​. If the graph is weighed i.e. $G = (V,E,W)$​​​​, then a shortest path is with respect to weights. This is one variation of the the algorithm among many. We won't worry about the details of the algorithm here.

The authors define a sheaf of sets $\mathcal{P}: G \to \mathcal{S}et$​​​​​​ in such a way that global sections correspond to path $e_0 e_1 \cdots e_{n-1}$ beginning at $v_S$ and ending at $v_T$. 

