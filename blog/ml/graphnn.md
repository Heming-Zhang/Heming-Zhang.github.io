---
layout: notes
section-type: notes
title: Machine Learning with Graphs
category: ml
---

* TOC
{:toc}
---
* History Papers
    * A new model earning in graph domains

* Course Material
    * Course [CS 224w: Machine Learning with Graphs](http://web.stanford.edu/class/cs224w/)
    * Course [Video Link](https://www.youtube.com/watch?v=0eNQnc0eOB4&list=PL1OaWjIc3zJ4xhom40qFY5jkZfyO5EDOZ)


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
<img class = "large" src=".//graph/002.png" height="65%" width="65%">
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
<img class = "large" src=".//graph/004.png" height="65%" width="65%">
</center>

* Hence, we can analyse the similarity of those nodes in space, and we have many approaches to measure the distance like Eucliden Distance, Cos Vector etc. In this way, we can just use the 

### 7.4 Random Walk Approaches to Node Embeddings
* $z_u^{T}z_v$ probability that $v$ and $u$ co-occur on a random walk over the network

### 7.5 Unsupervised Feature Learning
<center>
<img class = "large" src=".//graph/005.png" height="65%" width="65%">
</center>

<center>
<img class = "large" src=".//graph/006.png" height="65%" width="65%">
</center>

## 8th Graph Neural Network
### [Lecture 8 video](https://www.youtube.com/watch?v=7JELX6DiUxQ)
### 8.1 Nodes Embeddings
<center>
<img class = "large" src=".//graph/007.png" height="65%" width="65%">
</center>

* Two Key Components:
    * Encoder
    * Similarity Function

### 8.2 Basics of Deep Learning for Graphs
* Idea: Neighbourhood Aggregation
<center>
<img class = "large" src=".//graph/008.png" height="65%" width="65%">
</center>

* Final layer $h^{K}_{v}$ is embedding of $\mathbf{z}_{v}$
* Train the Model
    * $\mathbf{W}_{k}$
    * $\mathbf{B}_{k}$
* Inductive Capability
* So far, the GraphNN aggregate the neighbour messages by taking their(weighted) average 

### 8.3 GraphSAGE Graph Neural Network Architecture
* Concatenece:
    * Concatenate neighbour embedding and self embedding
    * Unlike Graph Convolution with adding itself, we just concatenate itself features then activate with non-linearity function
* Aggregation:
    * Use generalized aggregation function
    * Unlike Graph Convolution with just average

<center>
<img class = "large" src=".//graph/009.png" height="65%" width="65%">
</center>

* Aggregation Variants
    * Generally, there are several ways to implement aggregate
    * Mean
    * Pool (mean or max across a coordinate)
    * LSTM (make model much deeper with LSTM)
<center>
<img class = "large" src=".//graph/010.png" height="65%" width="65%">
</center>
Hints: we can apply different pooling startegies

### 8.4 Implementation
<center>
<img class = "large" src=".//graph/011.png" height="65%" width="65%">
</center>

* Notation:
    * $D$ is degree matrix
    * $A$ is adjeacent matrix
    * $H^{k-1}$ is message matrix from previous layer

* $D^{-1}$ matrix acts as a mean function in this formula.
* $AH^{k-1}$ is aimed to sum all neighbour features

### 8.5 Graph Attention Network (GAT)
* Simple Neighbourhood Aggregation in Graph Convolution
    * Use coefficient of ${\alpha}_{vu}$
    * All neighbour $u \in {N}(v)$ are equally important to node $v$
<center>
<img class = "large" src=".//graph/012.png" height="65%" width="65%">
</center>

* Attention Mechanism
    * Use $e_{vu}$ as coefficient
    * Mechanism $a$ may achieve in different ways including Simple Single-Layer Neural Network
<center>
<img class = "large" src=".//graph/013.png" height="65%" width="65%">
</center>

<center>
<img class = "large" src=".//graph/014.png" height="65%" width="65%">
</center>

### 8.6 More on Graph Neural Networks
* Tutoiral and Overviews

    * [Relational inductive biases and graph networks (Battaglia et al., 2018)](https://arxiv.org/pdf/1806.01261.pdf)

    * [Representation learning on graphs: Methods and applications ](https://arxiv.org/pdf/1709.05584.pdf)

* Attention-based neighborhood aggregation

    
