---
layout: notes
section-type: notes
title: Application on Machine Learning
category: ml
---

* TOC
{:toc}
---

## Environment on Mac
### Install python version
* Can install [uninstall] python 3.7.6 through
```
$ brew install python
$ brew uninstall python
```
* Find out that Mac come up with python 2.7 and python 3.7.3 itselfs
```
$ python --version
$ python3 --version
```
* Switch python version and make it comfortable
```
$ python
$ python3 (default python 3.7.3 in macbook)
$ python3.6 (default python 3.6.8 with installation)

$ alias python=python3.6 (make python command be python 3.6)
$ alias python=python (to switch back python to be python 2.7.16)
```

## Lecture 1 Structural Risk Minimization
### 1 Introduction
#### 1.1 Machine Learning Problem
* Minimize expected risk
* Use emprical risk instead

#### 1.2 Structural Risk Minimization
The goal of structural risk minimization is to balance **fitting the training data** against **model complexity**. Training means then to learn the model parameters by solving the following optimization problem:

$$\min_{\mathbf{w}}{\mathcal{L}(\mathbf{w}})=\min_{\mathbf{w}}\ {\frac{1}{n}}\sum_{i=1}^{n}{l(h_{\mathbf{w}}(\mathbf{x}_i),y_i)}\ +\ \lambda\ r(\mathbf{w})$$

The first part is loss function and the second part is regularizer.

### 2 Loss Functions
#### 2.1 Commonly Used Binary Classification Loss Functions
>* Zero-One Loss
>
>* Hinge-Loss: for SVM ($p=1$)
>
>$$\max{[1-f_{\mathbf{w}}(\mathbf{x}_i)y_i, 0]^{p}}$$
>
>* Log-Loss: logistic regression
>
>$$\log(1+e^{-f_{\mathbf{w}}(\mathbf{x}_i)y_i})$$

And from CSE 417T course, we know that cross-entropy loss is 

$$E_{in}(\mathbf{w})=\frac{1}{n}{\ln(1+e^{-y_i{\mathbf{w}^{\text{T}}}\mathbf{x}_i})}$$

And its hypothesis function is 

$$h(\mathbf{x})=\theta(\mathbf{w}^{\text{T}}\mathbf{x})=\frac{1}{1+e^{-\mathbf{w}^{\text{T}}\mathbf{x}}}\in[0,1]$$

>* Exponential Loss:
>
>$$e^{-f_{\mathbf{w}}(\mathbf{x}_i)y_i}$$

Since we know that AdaBoost will get the aggregated hypothesis which is 

$$g_{T}(\mathbf{x})=\text{sign}(H_{T}(\mathbf{x}))=\text{sign}\big(\sum_{t=1}^{T}\alpha_th_{t}(\mathbf{x})\big)$$

If $y=+1$ and the more $h(\mathbf{x})$ agree with $y$, the smaller loss is. (CSE 417T Lecture 16 Slide25)

#### 2.2 Commonly Used Regression Loss Function
> * Squared Loss
> * Absollute loss
> * Huber Loss
> * Log-Cosh Loss
> * $\epsilon$-Insensitive Loss

### 3 Regularizers
* $l_2$-regularizer: $r(\mathbf{w})=\mathbf{w}^{\text{T}}\mathbf{w}$

* $l_1$-regularizer: $r(\mathbf{w})=\|\mathbf{w}\|_{1}$

* $l_p$-Norm, often $0<p<1$: $\|\mathbf{w}\|_{p}=\big(\sum_{i=1}^{d}{|\mathbf{w}|^{p}}\big)^{\frac{1}{p}}$

* Elastic Net

### 4 Famous SRM Models
* Ordinary Least Squares
* Ridge Regression: $\min_{\mathbf{w}}{\frac{1}{n}}\sum_{i=1}^{n}{(\mathbf{w}^{\text{T}}\mathbf{x}_i-y_i)^2}\ +\ \lambda\ \|\mathbf{w}\|_{2}^{2}$
* Lasso: $\min_{\mathbf{w}}\ {\frac{1}{n}}\sum_{i=1}^{n}{(\mathbf{w}^{\text{T}}\mathbf{x}_i-y_i)^2}\ +\ \lambda\|\mathbf{w}\|_1$
* Logistic Regression: $\log(1+e^{-y_i(\mathbf{w}^{\text{T}}\mathbf{x}_i)})$
* SVM 

## Optimization for Machine Learning
### 1 Recap
* For **Linear Regression**, we can get unique global minimum.

 ### 2 Gradient Descent
 Get detail about it in [Convex Optimization](https://heming-zhang.github.io/blog/math/convexoptimization.html).  
 Assuming that $l(\mathbf{w})$ is convex, continuous, and differentiate(once or twice), there exists a **global minimum**.  
 With Taylor approximation:

 $$l(\mathbf{w+s})=l(\mathbf{w})+\nabla{l(\mathbf{w})}^{\text{T}}\mathbf{s}+\frac{1}{2}{\mathbf{s}^{\text{T}}\mathbf{H(w)s}}+o(\|\mathbf{s}\|)$$

 ### 3 Newton Method
Can see detail in Note: [Convex Optimization](https://heming-zhang.github.io/blog/math/convexoptimization.html).
 #### 3.1 Avoid Divergence of Newton's Method

 #### 3.2 Quasi-Newton Methods
 * Note that computing $\mathbf{H}(\mathbf{x})^{-1}$ is expensive $O(d^3)$

 ### 4 Best Practice

 #### 4.1 Momentum Method
 * Local Momentum + Previous Momentum
 #### 4.2 Stochastic Gradient Method
 * Use one training point at a time
 * Use mini-batches
 #### 4.3 Note: Random Restarts for Non-Convex Functions
