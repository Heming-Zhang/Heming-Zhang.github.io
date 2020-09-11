---
layout: notes
section-type: notes
title: Application on Machine Learning
category: ml
---

* TOC
{:toc}
---

## 1. Neural Networks
### 1.1 Combining Perceptrons

A simple and direct idea of **Neural Networks** is to combine perceptrons to approach the target function.

<center>
<img class="center large" src=".//ml_pictures/ml099.png" height="50%" width="80%">
</center>

Following is a figure of Multi-Layer Perceptrion (MLP).

<center>
<img class="center large" src=".//ml_pictures/ml100.png" height="50%" width="100%">
</center>

The **architecture** of an MLP is the vector $\vec{d}=[d^{(0)}, d^{(1)},\cdots, d^{(L)}]$.  
And the weights between layer $l-1$ and layer $l$ are a matrix: $W^{(l)} \in {\mathbb{R}^{(d^{(l-1)}+1)\times{d^{(l)}}}}$.

<center>
<img class="center large" src=".//ml_pictures/ml101.png" height="50%" width="100%">
</center>

To make clear the **Signal and Output** for MLP, following figure will demonstrate how each node contributes to the node of next layer.

<center>
<img class="center large" src=".//ml_pictures/ml102.png" height="50%" width="80%">
</center>

Then we can make **Forward Propagation for Predictions**:

<center>
<img class="center large" src=".//ml_pictures/ml103.png" height="50%" width="80%">
</center>

### 1.2 Backpropagation

The most important and interesting part of neural network is about backpropagation. To minimize the error function of the huge neural network with forward propagation of predictinos, we need to **Compute Gradients**:

<center>
<img class="center large" src=".//ml_pictures/ml104.png" height="50%" width="80%">
</center>

Then we need to **Computing Partial Derivatives With Chain Rule**:

<center>
<img class="center large" src=".//ml_pictures/ml105.png" height="50%" width="80%">
</center>

<center>
<img class="center large" src=".//ml_pictures/ml106.png" height="50%" width="80%">
</center>

At last, we can check the following for details of whole process of **Back Propagation**:

<center>
<img class="center large" src=".//ml_pictures/ml107.png" height="50%" width="90%">
</center>

### 1.3 Computing Gradients with Feed Forward and Back Propagation

<center>
<img class="center large" src=".//ml_pictures/ml108.png" height="50%" width="90%">
</center>

### 12.5 Mini-batch Gradient Descent
<center>
<img class="center large" src=".//ml_pictures/ml109.png" height="50%" width="90%">
</center>

### 12.6 Regulation
<center>
<img class="center large" src=".//ml_pictures/ml110.png" height="50%" width="70%">
</center>

### 12.7 Dropout Regulation
<center>
<img class="center large" src=".//ml_pictures/ml111.png" height="50%" width="70%">
</center>

### 12.8 MLP as Universal Approximators
<center>
<img class="center large" src=".//ml_pictures/ml112.png" height="50%" width="70%">
</center>