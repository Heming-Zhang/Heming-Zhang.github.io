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
> 
> $$Pr(X,Y)=Pr(Y|X)Pr(X)$$

> Bayesian Theorem  
> 
> $$Pr(Y|X)=\frac{Pr(X|Y)Pr(Y)}{Pr(X)}=\frac{Pr(X|Y)Pr(Y)}{\sum{Pr(X|Y)Pr(Y)}}$$

Posterior: $Pr(\theta|D)$  
Prior: $Pr(\theta)$  
Likelihood: $Pr(D|\theta)$  



### 1.2 Coin Flipping

Suppose that we flip the coin $n$ times and observe $x$ "heads". Therefore, the probability of this observation, given the value of $\theta$, comes from a binomial distribution:

$$Pr(D|\theta)=Bin(x|n,\theta)=\binom{n}{x}\theta^x(1-\theta)^{n-x}$$

#### **Maximum Likelihood**  

$$
\begin{aligned}
\hat{\theta}_{MLE}
&=\arg{\max_{\theta}}{\ Pr(D|\theta)}\\
&=\arg{\max_{\theta}}{\text{ Bin}(x|n,\theta)}\\
&=\arg{\max_{\theta}}{\ \binom{n}{x}\theta^{x}{(1-\theta)^{n-x}}}\\
&=\arg{\max_{\theta}}{\ x\text{log}{\theta}+(n-x)\text{log}{(1-\theta)}}\\
&=\frac{x}{n}
\end{aligned}
$$  


#### **Maximum A Posterior Emstimation**  
Since we have formula

$$Pr(\theta|D)=\frac{Pr(D|\theta)Pr(\theta)}{Pr(D)}$$

For a fixed set of observations,

$$Pr(\theta|D) \propto Pr(D|\theta)\times{Pr(\theta)}$$  

$$\text{Posterior} \propto \text{Likelihood}\times{\text{Prior}}$$

If $\theta$ is a continuous r.v. with $\color{dodgerblue}{\text{prior p.d.f.}}$ with $\color{dodgerblue}{g(\theta)}$, then its $\color{orangered}{\text{posterior p.d.f.}}$ with $\color{orangered}{f(\theta\|D)}$ is given by

$$\color{orangered}{f(\theta|D)}=\color{b}{\frac{\color{lightgreen}{Pr(D|\theta)}\color{b}{\times}\color{dodgerblue}{g(\theta)}}{Pr(D)}}$$















Like following picture:

<center>
<img class="center large" src=".//bml/001.png" height="50%" width="70%">
</center>

* Suppose prior representing an expectation of coins biased toward more heads:

$$
\color{dodgerblue}{g(\theta)}
\color{b}{
=
\begin{cases}
    2\theta\ \ 0\leq{\theta}\leq{1} \\
    0\ \ \ \ \text{otherwise}
\end{cases}}
$$

* Using above prior, the posterior p.d.f. $f$ is given by:

$$
\begin{aligned}
\color{orangered}{f(\theta|x,n)}&\propto{\binom{n}{x}\theta^x(1-\theta)^{n-x}\times{2\theta}}\\
&\propto {{\theta^{x+1}}(1-\theta)^{n-x}}
\end{aligned}
$$

* From above formula, we will observe one more head than former belief, which is counted with **Pseudocount**

#### **Conjugate Priors**

The two example priors given here, the uniform prior on $[0,1]$ and  

$$
g(\theta)=
\begin{cases}
    2\theta\ \ 0\leq{\theta}\leq{1} \\
    0\ \ \ \ \text{otherwise}
\end{cases}
$$

are both $\color{orangered}{\textbf{conjugate priors}}$ for the bionmial likelihood function because the prior and the posterior have the same function form. Distributions with this form are called $\color{orangered}{\textbf{beta distributions}}$.

In general, a beta distribution on $\theta$ has the form  

$$\text{beta}(\theta|\alpha,\beta)=\frac{\Gamma(\alpha+\beta)}{\Gamma(\alpha)\Gamma(\beta)}\theta^{\alpha-1}(1-\theta)^{\beta-1}$$

When $n$ is a positive integer, $\Gamma(n)=(n-1)!$. Thus, when $\alpha$ and $\beta$ are positive integers,

$$\text{beta}(\theta|\alpha,\beta)=\frac{(\alpha+\beta-1)!}{(\alpha-1)!\ (\beta-1)!}\theta^{\alpha-1}(1-\theta)^{\beta-1}$$

* The p.d.f. that is uniform on $[0,1]$ and $0$ elsewhere is $\text{beta}(\theta\|\alpha=1,\beta=1)=1$
* The p.d.f. that is $2\theta$ on $[0,1]$ and $0$ elsewhere is $\text{beta}(\theta\|\alpha=2,\beta=1)=2\theta$

Therefore, when a beta prior p.d.f. with integer parameters $\alpha, \beta$, is multiplied by a binomial likelihood of $x$ heads in $n$ trials, the posterior p.d.f. on $\theta$ is

$$f(\theta|x,n,\alpha,\beta) \propto \theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}$$

for $\theta\in[0,1]$ and $0$ elsewhere. And the proportionality constant ensures that the integral of the posterior over all values of $\theta$ is $1$. Hence, the normalized posterior p.d.f. is:

$$\color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{orangered}{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}$$

> Thus, when a prior p.d.f. is a beta distribution with parameters $\alpha, \beta$ and the likelihood is binomial, the posterior p.d.f. is a beta distribution with parameters $x+a$ and $n-x+b$. For this reason, the beta family of priors is said to be conjugate to binomial likelihood functions.

Maximum Likelihood Estimation for Above Distribution

$$\theta_{MLE}=\frac{x}{n}$$

Maximum A Posterior Emstimation

$$
\begin{aligned}
\theta_{MAP}
& =\arg{\max_{\theta}}{\ Pr(\theta|D)}\\
& =\arg{\max_{\theta}}{\ Pr(D|\theta)\cdot{Pr(\theta)}}\\
& =\arg{\max_{\theta}}{\ \theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}\\
& =\frac{x+\alpha-1}{n+\alpha+\beta-2}
\end{aligned}
$$


#### **Posterior Predictive Distributions**

With a $\color{orangered}{\textbf{conjugate priors}}$ of $\color{orangered}{f(\theta\|D)}$ on parameters $\theta$ given observations $D$, we can compute a distribution on future observations that does not depend on assuming any particular parameter values.

$$Pr(X=x|D)=\int_{-\infty}^{{+\infty}}Pr(X=x|\theta)\color{orangered}{\ f{(\theta|D)}}\color{b}d\theta$$

For example:  
* When the prior on $\theta$ is $\text{beta}(\alpha,\beta)$, $X$ is a binary random variable with $Pr(X=1)=\theta$.  
* Here, $n$ Bernoulli experiments have been observed in which $X=1$ occured $x$ times, above equation becomes:

$$
\begin{aligned}
Pr(X=1|D)
& = \int_{0}^{1}\color{dodgerblue}{Pr(X=1|\theta)}\color{orangered}{\ f{(\theta|D)}}\color{b}{d\theta}\\
& = \int_{0}^{1}\color{dodgerblue}{\theta}\color{orangered}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{orangered}{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}\color{b}{d\theta}\\
& = \int_{0}^{1}\color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}{\theta^{x+\alpha}(1-\theta)^{n-x+\beta-1}}d{\theta}\\
& = \color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{violet}{\int_{0}^{1}{\theta^{x+\alpha}(1-\theta)^{n-x+\beta-1}}d{\theta}}\\
& = \color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{violet}{\text{ Beta}(\alpha,\beta)}\\
& = \color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{violet}{\frac{(x+\alpha)!(n-x+\beta-1)!}{(n+\alpha+\beta)!}}\\
& = \frac{x+\alpha}{n+\alpha+\beta}
\end{aligned}
$$

Here, we re-introduce $\color{violet}{\textbf{beta function}}$ concept.

$$ 
\begin{aligned}
\color{violet}{\textbf{beta function}}
&:\color{b}{\text{Beta}(\alpha,\beta)=\int_{0}^{1}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{d{\theta}}=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}}\\
\color{violet}{\textbf{beta distribution}}
&:\color{b}{\text{Beta}(\theta|\alpha,\beta)=\frac{1}{\text{Beta}(\alpha,\beta)}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}}
\end{aligned}
$$

#### **Multinomial Distribution**

* Here, *binomial distribution* becomes *multinomial distribution*.
* *Beta distribution* becomes *Dirichlet* prior.

Likelihood  

$$Pr(X|\theta)=\text{Mu}(x|\theta)=\prod_{j=1}^{K}{\theta_{j}^{I(x=j)}}$$

$$Pr(x|\theta)=\text{Mu}(x|\theta)=\prod_{j=1}^{K}{\theta_{j}^{x_j}}$$

$$
\begin{aligned}
Pr(D|\theta)
&=\prod_{n=1}^{N}\prod_{j=1}^{K}{\theta_{j}^{I(x_{n}=j)}}\ \ \ (D=\{x_1,x_2,\cdots,x_N \})\\
Pr(N_1,N_2,\cdots,N_k|N)
&=\text{Mu}(\theta,N)=\binom{N}{N_1,N_2,\cdots,N_k}\prod_{j=1}^{K}{\theta_{j}^{N_j}}
\end{aligned}
$$

For example,

$$Pr(x_1,x_2,x_3|\theta_1,\theta_2,\theta_3)=\frac{(x_1+x_2+x_3)!}{{x_1}!{x_2}!{x_3}!}{\ \theta_1^{x_1}}{\theta_2^{x_2}}{\theta_3^{x_3}}$$



