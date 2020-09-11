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
### 1.1 Introduction
#### 1.1.1 Machine Learning Problem
> (1) Minimize expected risk  
> (2) Use emprical risk instead: However, this tends to overfit to the training data, and typically a simpler model is preferred (Occam's Razor).

#### 1.1.2 Structural Risk Minimization
> The goal of structural risk minimization is to balance **fitting the training data** against **model complexity**. Training means then to learn the model parameters by solving the following optimization problem:
>
> $$\min_{\mathbf{w}}{\mathcal{L}(\mathbf{w}})=\min_{\mathbf{w}}\ {\frac{1}{n}}\sum_{i=1}^{n}{l(h_{\mathbf{w}}(\mathbf{x}_i),y_i)}\ +\ \lambda\ r(\mathbf{w})$$
>
> The first part is loss function and the second part is regularizer.

### 1.2 Loss Functions
#### 1.2.1 Commonly Used Binary Classification Loss Functions
> For binary classification we naturally want to minimize the zero-one loss $l(h_{\mathbf{w}}(\mathbf{x}), y)$ also called true classification error. However, due to its non-continuity it is impractical to optimize and we resort to using various surrogate loss functions $l(f_{\mathbf{w}}(\mathbf{x}),y)$. 
> 
> (1) Zero-One Loss  
> (2) Hinge-Loss: for SVM ($p=1$) $\max{[1-f_{\mathbf{w}}(\mathbf{x}_i)y_i, 0]^{p}}$  
> (3) Log-Loss: logistic regression
>
> $$\log(1+e^{-f_{\mathbf{w}}(\mathbf{x}_i)y_i})$$
>
>And from CSE 417T course, we know that cross-entropy loss is 
>
> $$E_{in}(\mathbf{w})=\frac{1}{n}{\ln(1+e^{-y_i{\mathbf{w}^{\text{T}}}\mathbf{x}_i})}$$
> 
> And its hypothesis function is $h(\mathbf{x})=\theta(\mathbf{w}^{\text{T}}\mathbf{x})=\frac{1}{1+e^{-\mathbf{w}^{\text{T}}\mathbf{x}}}\in[0,1]$
>
> (4) Exponential Loss:  $e^{-f_{\mathbf{w}}(\mathbf{x}_i)y_i}$
>
> Since we know that AdaBoost will get the aggregated hypothesis which is 
> 
> $$g_{T}(\mathbf{x})=\text{sign}(H_{T}(\mathbf{x}))=\text{sign}\big(\sum_{t=1}^{T}\alpha_th_{t}(\mathbf{x})\big)$$
> 
> If $y=+1$ and the more $h(\mathbf{x})$ agree with $y$, the smaller loss is. (CSE 417T Lecture 16 Slide25). Therefore, the exponential loss is very aggressive and thus sensitive to label noise.

#### 1.2.2 Commonly Used Regression Loss Function
> * Squared Loss: $(f_{\mathbf{w}}(\mathbf{x}_i)-y_i)^2$    
> * Absollute loss:  $\text{abs.}(f_{\mathbf{w}}(\mathbf{x}_i)-y_i)$  
> * Huber Loss  
> * Log-Cosh Loss  
> * $\epsilon$-Insensitive Loss  

### 1.3 Regularizers
> (1) $l_2$-regularizer: $r(\mathbf{w})=\mathbf{w}^{\text{T}}\mathbf{w}$  
> (2) $l_1$-regularizer   
> (3) $l_p$-Norm, often $0<p<1$   
> (4) Elastic Net

### 1.4 Famous SRM Models
> (1) Ordinary Least Squares (OLS)  
> (2) Ridge Regression: $\min_{\mathbf{w}}{\frac{1}{n}}\sum_{i=1}^{n}{(\mathbf{w}^{\text{T}}\mathbf{x}_i-y_i)^2}\ +\ \lambda\ \mathbf{w}^{\text{T}}\mathbf{w}$  
> (3) Lasso  
> (4) Logistic Regression: $\log(1+e^{-y_i(\mathbf{w}^{\text{T}}\mathbf{x}_i)})$  
> (5) SVM 

## Lecture2 Optimization for Machine Learning
### 2.1 Recap
For **Linear Regression**, we can get unique global minimum.

### 2.2 Gradient Descent
Get detail about it in [Convex Optimization](https://heming-zhang.github.io/blog/math/convexoptimization.html).  

> Assuming that $l(\mathbf{w})$ is convex, continuous, and differentiate(once or twice), there exists a **global minimum**.  
With Taylor approximation:
>
> $$l(\mathbf{w+s})=l(\mathbf{w})+\nabla{l(\mathbf{w})}^{\text{T}}\mathbf{s}+\frac{1}{2}{\mathbf{s}^{\text{T}}\mathbf{H(w)s}}+o(\|\mathbf{s}\|)$$  
> 
> where the $\nabla{l(\mathbf{w})}^{\text{T}}$ is the first order approximation and $\nabla^{2}{l(\mathbf{w})}$ is the second order
approximation. And the Gradient descent use the first order approxximation.

> * Some choices of the learning rate $\alpha$
> * A safe choice: $\alpha_t = \frac{1}{t}$
> * Linear Search
> * Heuristic/ ad-hoc choice:
> 
> $$\alpha_{t+1} = 
\begin{cases}
1.01\alpha_t,\ \text{if}\ \ l(\mathbf{w}_{t+1})\leq{l(\mathbf{w}_{t})}\\
0.5\alpha_t,\ \text{if}\ \ l(\mathbf{w}_{t+1})>{l(\mathbf{w}_{t})}
\end{cases}
$$



### 2.3 Newton Method
Can see detail in Note: [Convex Optimization](https://heming-zhang.github.io/blog/math/convexoptimization.html).

#### 2.3.1 Avoid Divergence of Newton's Method

#### 2.3.2 Quasi-Newton Methods
Note that computing $\mathbf{H}(\mathbf{x})^{-1}$ is expensive $O(d^3)$

### 2.4 Best Practice

#### 2.4.1 Momentum Method
Local Momentum + Previous Momentum

#### 2.4.2 Stochastic Gradient Method
> (1) Use one training point at a time  
> (2) Use mini-batches

#### 4.3 Note: Random Restarts for Non-Convex Functions




## Lecture 6 Naive Bayes Classifier
### 6.1 Introduction
> (1) **Thought**: Can we model 
> $$p(y|\mathbf{x})$$
> without model assumptions, e.g. Gussian/Bernoulli distribution etc.?
> 
> (2) **Idea**: Estimate 
> $$p(y|\mathbf{x})$$
 from the data directly, then use the Bayes classifier.
> 
> Let $y$ be discrete,
> 
> $$p(y|\mathbf{x})=\frac{\sum_{i=1}^{n}I(\mathbf{x}_i=\mathbf{x}\cap{y_i=y})}{\sum_{i=1}^{n}(\mathbf{x}_i=\mathbf{x})}$$
> 
> Using MLE estimate is only good if there are many training vectors with the **same identical** features as $\mathbf{x}$. This never happens for high-dimensional or continuous feature spaces.
> 
> **Solution:** Bayes Rule.
> 
> $$p(y|\mathbf{x})=\frac{p(\mathbf{x}|y)p(y)}{p(\mathbf{x})}$$
> 
> In this way, let's estimate 
> $$p(\mathbf{x}|y)$$ 
> and 
> $$p(y)$$ instead.

### 6.2 Naive Bayes
We have a discrete lable space $C$ that can either be binary ${-1,+1}$ or multi-class ${1,...,K}$

#### 6.2.1 Estimate $p(y)$
(1) Binary classification  
(2) Multiclass classification

#### 6.2.2 Estimate $p(\mathbf{x}|y)$
> **Naive Bayes Assumption**: The features are independent given the > label,
> 
> $$p(\mathbf{x}|y)=\prod_{\alpha=1}^{d}p([\mathbf{x}]_{\alpha}|y)$$
> 
> And estimating 
> $$p([\mathbf{x}]_{\alpha}|y)$$
> is relatively easy since we only need to consider one dimension.
> 
> (1) Case1: Categorical Features  
> (2) Case2: Multinomial Features  
> (3) Case3: Continuous Features(Gussian Naive Bayes)