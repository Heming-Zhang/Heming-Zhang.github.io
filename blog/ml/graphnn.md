---
layout: notes
section-type: notes
title: Machine Learning with Graphs
category: ml
---

* TOC
{:toc}
---

## CNN

## RNN

## GNN
* History Papers
    * A new model earning in graph domains

* Course Material
    * Course [CS 224w: Machine Learning with Graphs](http://web.stanford.edu/class/cs224w/)


## 1st Lecture Introduction and Structure of Graphs 
### 1.1 Components of Graph
* Objects: nodes, vertices $N$
* Interactions: links, edges $E$
* System: network, graph $G(N,E)$

### 1.2 Node Degrees
* Node Degree
* Avg Degree $\bar{k}=\frac{1}{N}{\sum_{i=1}^{N}k_i}=\frac{2E}{N}$

### 1.3 Biartite Graph
* Folded/Projected Bipartite Graphs

### 1.4 Adjacency Matrix
* Undirected
* Directed

### 1.5 Edge Attributes
* Weight(e.g. frequency of communication)
* Ranking(best friend, second best friend)
* Type(friend, relative, co-worker)
* Sign(Friend vs. Foe, Trust vs. Distrust)

### 1.6 Types of Graphs
* Unweighted; Weighted
* Self-edges; Multigraph

### 1.7 Connectivity
* Connectivity of Undirected graph
* Connectivity of directed graph

## 2nd Lecture Properties of Networks and Random Graph Models 
### 2.0 Notations
* Degree Distribution: $P(k)$
* Path Length: $h$
* Clustering Coefficient: $C$
* Connected Components: $s$

### 2.1 Degree Distributionn $P(k)$
### 2.2 Paths in a Graph
* Distance in a Graph
* Network Diameter
    * Diameter: The maximum(shortest path) distance between any pair of nodes in a graph
    * Average path length: 

### 2.3 Clustering Coefficient $C_i$
* Undirected Graph Clustering Coefficient
    * How connected are $i$'s neighbours to each other?
    * Node $i$ with degree $k_i$
    * $C_i = \frac{2e_i}{k_i(k_i-1)}$, denominator show the maximum edge connections for neighbour nodes of node $i$

<center>
<img class = "large" src=".//graph/001.png" height="65%" width="65%">
</center>

### 2.4 Connectivity
* Size of largest connected component
* Largest component = Giant Component

### 2.5 Propertities of $G_{np}$
* Degree distribution: $p(k)=C_{n-1}^{k}p^k(1-p)^{n-1-k}$
* Clustering Coefficient of $G_{np}$: $C=p=\bar{k}/n$
* Averge Path Length: $O(\log{n})$


### 2.5 Small-World Model
* Can we have high clustering while also having short paths?

<center>
<img class = "large" src=".//graph/002.png" height="65%" width="85%">
</center>

### 2.6 Kronecker Graph Model


## 3rd Lecture Motifs and Structure Roles in Networks
### 3.1 Subnetwork
### 3.2 Network Motifs
* Motif: Recurring, Significant, Patterns of interconnections
* And motif occur in the real network more often than the random network.
* $Z_i$ captures the siginificance of motif i
* Network Significance Profile(SP):
    
### 3.3 Graphlets
* Graph Degree Vector
* Automorphism Orbits

### 3.4 Graph Isomophism
* Example: Are $G$ and $H$ topologically equivalent?


## 7th Lecture Graph Representation Learning
* Node Classification
* Link Prediction

### 7.1 Feature Learning in Graphs
* Feature Representation Embedding
* Task: Map each node in a network into a low-dimensional space

### 7.2 Node Embedding
* CNN for fixed-size images/grids
* RNNs or word2vec for text/sequences

### 7.3 Embedding Nodes Task
<center>
<img class = "large" src=".//graph/004.png" height="65%" width="85%">
</center>

* Hence, we can analyse the similarity of those nodes in space, and we have many approaches to measure the distance like Eucliden Distance, Cos Vector etc. In this way, we can just use the 

