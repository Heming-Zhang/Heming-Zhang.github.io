---
layout: notes
section-type: notes
title: Bayesian Machine Learning
category: ml
---

* TOC
{:toc}
---

Courses Website
* [CSE 515T](https://www.cse.wustl.edu/~garnett/cse515t/fall_2019/)


## 1. Bayesian Inference
<hr>

### 1.1 Introduction to the Bayesian Method

The goal of probabilistic inference is to make some statements about $\theta$ given these observations.

> The Rule of Total Probability  
> 
> $$Pr(X)=\sum_{i=1}^{N}Pr(X,Y_i)$$
>
> $$p(x)=\int_{Y}p(x,y)dy$$

> Product Rule
> $$Pr(X,Y)=Pr(Y\|X)Pr(X)$$

> Bayesian Theorem
> $$Pr(Y\|X)=\frac{Pr(X\|Y)Pr(Y)}{Pr(X)}=\frac{Pr(X\|Y)Pr(Y)}{\sum{Pr(X\|Y)Pr(Y)}}$$

Posterior: $Pr(\theta\|D)$  
Prior: $Pr(\theta)$  
Likelihood: $Pr(D\|\theta)$  


### 1.2 Coin Flipping

Suppose that we flip the coin $n$ times and observe $x$ "heads". Therefore, the probability of this observation, given the value of $\theta$, comes from a binomial distribution:

$$Pr(x\|n,\theta)=\binom{n}{x}\theta^x(1-\theta)^{n-x}$$

**Maximum Likelihood**  
* $\theta_{MLE}=\underset{\theta}\text{argmax}{Pr(x\|\theta)}$  
* Here, coin flipping, $x$ heads in $n$ flips, $\theta_{MLE}=\frac{x}{n}$

**Maximum A Posterior Emstimation**  
Since we have formula

$$Pr(\theta\|D)=\frac{Pr(D\|\theta)Pr(\theta)}{Pr(D)}$$

For a fixed set of observations,

$$Pr(\theta\|D) \propto Pr(D\|\theta)Pr(\theta)$$
$$\text{Posterior} \propto \text{Likelihood}\times{\text{Prior}}$$

If $\theta$ is a continuous r.v. with prior p.d.f., $g(\theta)$ then its posterior p.d.f. $f(\theta\|D)$ is given by

$$\textcolor{yellow}{f(\theta\|D)}=\frac{Pr(D\|\theta)\times\textcolor{yellow}{g(\theta)}}{Pr(D)}$$

* Suppose prior representing an expectation of coins biased toward more heads:

$$
g(\theta)=
\begin{cases}
    2\theta\ \ 0\leq{\theta}\leq{1} \\
    0\ \ \ \ \text{otherwise}
\end{cases}
$$

* Using above prior, the posterior p.d.f. $f$ is given by:

$$
\begin{aligned}
f(\theta\|x,n)&\propto{\binom{n}{x}\theta^x(1-\theta)^{n-x}\times{2\theta}}\\
&\propto {\textcolor{yellow}{\theta^{x+1}}(1-\theta)^{n-x}}
\end{aligned}
$$

* From above formula, we will observe one more head than former belief, which is counted with **Pseudocount**

**Conjugate Priors**

The two example priors given here, the uniform prior on $[0,1]$ and  

$$
g(\theta)=
\begin{cases}
    2\theta\ \ 0\leq{\theta}\leq{1} \\
    0\ \ \ \ \text{otherwise}
\end{cases}
$$

are both $\textcolor{yellow}{\textbf{conjugate priors}}$ for the bionmial likelihood function because the prior and the posterior have the same function form. Distributions with this form are called $\textcolor{yellow}{\textbf{beta distributions}}$.

In general, a beta distribution on $\theta$ has the form  

$$\text{beta}(\theta\|a,b)=\frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}\theta^{\alpha-1}(1-\theta)^{\beta-1}$$

When $n$ is a positive integer, $\Gamma(n)=(n-1)!$. Thus, when $\alpha$ and $\beta$ are positive integers,

$$\text{beta}(\theta\|a,b)=\frac{(\alpha+\beta-1)!}{(\alpha-1)!\ (\beta-1)!}\theta^{\alpha-1}(1-\theta)^{\beta-1}$$

* The p.d.f. that is uniform on $[0,1]$ and $0$ elsewhere is $\text{beta}(\theta\|\alpha=1,\beta=1)=1$
* The p.d.f. that is $2\theta$ on $[0,1]$ and $0$ elsewhere is $\text{beta}(\theta\|\alpha=2,\beta=1)=2\theta$

Therefore, when a beta prior p.d.f. with integer parameters $\alpha, \beta$, is multiplied by a binomial likelihood of $x$ heads in $n$ trials, the posterior p.d.f. on $\theta$ is

$$f(\theta\|x,n,\alpha,\beta) \propto \theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}$$

for $\theta\in[0,1]$ and $0$ elsewhere. And the proportionality constant ensures that the integral of the posterior over all values of $\theta$ is $1$. Hence, the normalized posterior p.d.f. is:

$$\color{yellow}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{red}{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}$$

> Thus, when a prior p.d.f. is a beta distribution with parameters $\alpha, \beta$ and the likelihood is binomial, the posterior p.d.f. is a beta distribution with parameters $x+a$ and $n-x+b$. For this reason, the beta family of priors is said to be conjugate to binomial likelihood functions.

* Maximum Likelihood Estimation for Above Distribution
$$\theta_{MLE}=\frac{x}{n}$$

* Maximum A Posterior Emstimation

$$
\begin{aligned}
\theta_{MAP}&=\underset{\theta}\text{argmax}{Pr(\theta\|D)}\\
&=\underset{\theta}\text{argmax}{Pr(D\|\theta)\cdot{Pr(\theta)}}\\
&=\underset{\theta}\text{argmax }{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}\\
&=\frac{x+\alpha-1}{n+\alpha+\beta-2}
\end{aligned}
$$


**Posterior Predictive Distributions**

With a $\textbf{posterior pdf}$ $f\bf{(\theta\|D)}$ on parameters $\theta$ given observations $D$, we can compute a distribution on future observations that does not depend on assuming any particular parameter values.

$$Pr(X=x\|D)=\int_{-\infty}^{{+\infty}}Pr(X=x\|\theta)f\bf{(\theta\|D)}d\theta$$










