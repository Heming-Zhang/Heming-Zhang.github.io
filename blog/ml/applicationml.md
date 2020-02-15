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

## Lecture2 Optimization for Machine Learning
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

## Lecture 3 Estimating Probabilities from Data
### 1 Introduction
#### 1.1 Noise
#### 1.2 Basic Problem: Tossing a Coin

### 2 Maximum Likelihood Estimation
* Let $p(y=H)=\theta$, where $\theta$ is the unknown parameter, and all we have is $D$. So, the goal is to choose $\theta$ such taht observed data $D$ is most like likely.
* Formally(MLE principle), Find $\hat{\theta}$ that maximizes the likelihood of the data $p(D|\theta)$.
* **Goal**

$$\hat{\theta}_{MLE}=\arg{\max_{\theta}} {P(D|\theta)}$$

* Example: Coin Flipping

$$
\begin{aligned}
\hat{\theta}_{MLE}&=\arg{\max_{\theta}} {P(D|\theta)}\\
&=\arg{\max_{\theta}}{C_{n}^{n_{H}}\theta^{n_{H}}(1-\theta)^{n-n_{H}}}\\
&<=> \arg{\max_{\theta}}\ {\log{C_{n}^{n_{H}}} + n_{H}\log{\theta} + (n-n_{H})\log(1-\theta)}
\end{aligned}
$$

Take derivative for above formula, we can get

$$\hat{\theta}_{MLE}=\frac{n_{H}}{n}$$




### 3 Baysian Way and Maximum a-posterior Estimation
* To avoid the randomness of data, you may want to use baysian way to estimate $\theta$.
* Baysian Way - Maximum A Posterior(MAP) 
    * Model $\theta$ as a random variable
    * Where $\theta$ is a drown from a distribution
    * New, we look at $p(\theta|D)$

$$P(\theta|D) = \frac{P(D|\theta)P(\theta)}{P(D)}{\propto}{P(D|\theta)P(\theta)}$$

* Tips for notation:  
$P(D|\theta)$ : **likelihood** of the data given the parameters $\theta$  
$P(\theta)$ : **prior** distribution over the parameters $\theta$  
$P(\theta|D)$ : **posterior** distribution over the parameters $\theta$

* A useful prior distribution  
Beta distribution: $P(\theta)=Beta{(\theta|\alpha, \beta) }= \frac{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{b(\alpha, \beta)}$, where $b(\alpha, \beta)=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$, and note that  

$$P(\theta|D)=Beta(n_{H}+\alpha, n_{T}+\beta)$$  


* **Goal**: Maximize the posterior distribution $P(\theta|D)$

$$
\begin{aligned}
\hat{\theta}_{MAP}&=\arg \max_{\theta}\ {P(\theta|D)}\\
&=\arg \max_{\theta}\ \frac{P(D|\theta)P(\theta)}{P(D)}\\
&=\arg \max_{\theta}\ P(D|\theta)P(\theta)\\
\end{aligned}
$$

* Example: Coin Flipping
Since we know that $P(D|\theta)$ is Binomial Distribution, and we have prior distribution for $P(\theta)$

$$
\begin{aligned}
\hat{\theta}_{MAP}&=\arg \max_{\theta}\ {P(\theta|D)}\\
&=\arg \max_{\theta} {\log}{P(D|\theta)} + \log{P(\theta)}\\
&=\arg \max_{\theta} n_{H}\log{\theta} + (n-n_{H})\log(1-\theta)\\
&+ (\alpha-1)\log{\theta} + (\beta-1)\log{(1-\theta)}
\end{aligned}
$$

Hence,

$$\hat{\theta}_{MAP}=\frac{n_{H}+\alpha-1}{n+\alpha+\beta-2}$$

* Advantages:
    * as $n\rightarrow{\infty}$, $\hat{\theta}_{MAP}\rightarrow\hat{\theta}_{MLE}$
    * MAP is a great estimator if prior belief exists and is accurate
* Disadvantages:
    * If $n$ is small, it can be very wrong if prior belief is wrong
    * Also we have to choose a reasonable prior


### 4 "True" Bayesian Approach
Note that MAP is only one way to get an estimator for $\theta$. There is much more information in $P(\theta|D)$.

#### 4.1 Posterior Mean
So, instead of the maximum as we did with MAP, we can use the posterior mean (and even its variance).

$$\hat{\theta}_{\text{MEAN}}=E[\theta, D]=\int_{\theta}\theta{p(\theta|D)}d\theta$$

#### 4.2 Posterior Predictive
So far, we talked about modeling and estimating parameters. But in machine learning, we actually interested in predictions. To directly estimate label $y$ from the given data, we can use the posterior predictive distribution. 

In our coin tossing example, this is given by: (since we know that $p(y=H|\theta,D)=\theta$ in the coin flipping)

$$
\begin{aligned}
p(y=H|D)&=\int_{\theta}p(y=H, \theta |D)d\theta\\
&=\int_{\theta}p(y=H|\theta,D)p(\theta|D)d\theta\\
&=\int_{\theta}\theta{p(\theta|D)}d\theta
\end{aligned}
$$

In general, the posterior predictive distribution is ($\mathbf{x}$ is test input, and $\theta$ means the $\mathbf{w}$ or the parameters in model)

$$
\begin{aligned}
p(y|D,\mathbf{x})&=\int_{\theta}p(y,\theta|D,\mathbf{x})d\theta\\
&=\int_{\theta}p(y|D, \mathbf{x}, \theta)\cdot{p(\theta|D,\mathbf{x})}d\theta\\
&=\int_{\theta}p(y|D, \mathbf{x}, \theta)\cdot{p(\theta|D)}d\theta
\end{aligned}
$$


## Lecture 4 MLE and MAP for discrimitive supervised learning
### 1 Introduction
Usually, there are two assumptions in discrimitive supervised learning:  
(1) $\mathbf{x}_i$ are known, => $\mathbf{x}_i$ independant of the model parameters $\mathbf{w}$, hence $p(X|\mathbf{w})=p(X)$ and $p(\mathbf{w}|X)=p(\mathbf{w})$  
(2) $y_i$ are independent ghven the input features $\mathbf{x}_i$ and $\mathbf{w}$  
 **Goal:** Estimate $\mathbf{w}$ directly from $D=\{(\mathbf{x}, y_i)\}^{n}_{i=1}$ using the joint conditional likelihood $p(\mathbf{y}|X,\mathbf{w})$

#### 1.1 Maximum Likelihood Estimation
 Choose $\mathbf{w}$ to maximize the conditional likelihood. (use two assumptions above)

 $$
 \begin{aligned}
 \hat{\mathbf{w}}_{\text{MLE}}&=\arg \max_{\mathbf{w}} {p(D|\mathbf{w})}\\
&= \arg \max_{\mathbf{w}} {p(\mathbf{y}|X,\mathbf{w})}\\
&= \arg \max_{\mathbf{w}} {\prod_{i=1}^{n}p(y_i|\mathbf{x}_i, \mathbf{w})}\\
&= \arg \max_{\mathbf{w}} {\sum_{i=1}^{n} \log{p(y_i|\mathbf{x}_i, \mathbf{w})}  }
 \end{aligned}
 $$

#### 1.2 Bayesian way to Maximum-a-posterior Estimation
Model $\mathbf{w}$ as a random variable from $p(\mathbf{w})$ and use $p(\mathbf{w}|D)$. Choose $\mathbf{w}$ to maximize the posterior $p(\mathbf{w}|X,\mathbf{y})$ over $\mathbf{w}$.

$$
\begin{aligned}
\hat{\mathbf{w}}_{\text{MAP}}&=\arg \max_{\mathbf{w}} {p(\mathbf{w}|X, \mathbf{y})}\\
&=\arg \max_{\mathbf{w}} {p( X,\mathbf{y}|\mathbf{w})\cdot{p(\mathbf{w})}}\\
&= \arg \max_{\mathbf{w}} {p(\mathbf{y}|X,\mathbf{w})\cdot{p(\mathbf{w})}}\\
&= \arg \max_{\mathbf{w}} {\prod_{i=1}^{n}p(y_i|\mathbf{x}_i, \mathbf{w})\cdot{p(\mathbf{w})}}\\
&= \arg \max_{\mathbf{w}} {\sum_{i=1}^{n} \log{p(y_i|\mathbf{x}_i, \mathbf{w})} + \log{p(\mathbf{w})} }
\end{aligned}
$$

### 2 Example: Linear Regression
Model Assumption: $y_i = \mathbf{w}^{\text{T}}\mathbf{x}_i+\epsilon_i \in \mathbb{R}$, where we use the Gussian distribution to model the noise $\epsilon_i \sim N(0,\sigma^2)$

$$p(y_i|\mathbf{x}_i, \mathbf{w})=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(\mathbf{w}^{\text{T}}\mathbf{x}-y_i)^2}{2\sigma^2}}$$

MLE: it is like OLS/squared loss  

MAP: Additional Model Assumption, prior distribution (ensure for yourself that the following is a conjuate prior to our likelihood). Then it is like l2-regularization


## Lecture 6 Naive Bayes Classifier
### 1 Introduction
**Thought**: Can we model $p(y|\mathbf{x})$ without model assumptions, e.g. Gussian/Bernoulli distribution etc.?

**Idea**: Estimate $p(y|\mathbf{x})$ from the data directly, then use the Bayes classifier.

Let $y$ be discrete,

$$p(y|\mathbf{x})=\frac{\sum_{i=1}^{n}I(\mathbf{x}_i=\mathbf{x}\cap{y_i=y})}{\sum_{i=1}^{n}(\mathbf{x}_i=\mathbf{x})}$$

Using MLE estimate is only good if there are many training vectors with the **same identical** features as $\mathbf{x}$. This never happens for high-dimensional or continuous feature spaces.

**Solution:** Bayes Rule.

$$p(y|\mathbf{x})=\frac{p(\mathbf{x}|y)p(y)}{p(\mathbf{x})}$$

In this way, let's estimate $p(\mathbf{x}|y)$ and $p(y)$ instead.

### 2 Naive Bayes
We have a discrete lable space $C$ that can either be binary $\{-1,+1\}$ or multi-class $\{1,...,K\}$

#### 2.1 Estimate $p(y)$

#### 2.2 Estimate $p(\mathbf{x}|y)$


## Lecture 7 Performance Evaluation for ML Methods
### 1 Introduction

### 2 Assessing Performance

### 3 Statistical Tests
#### 3.1 Parametric Tests

#### 3.2 Non-parametric Tests
* degree of freedom (review on stastics book)
