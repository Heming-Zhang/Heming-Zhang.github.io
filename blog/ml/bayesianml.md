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

$$\color{orangered}{\text{Posterior }} \color{b}{\propto} \color{lightgreen}{\text{ Likelihood }}\color{b}{\times}\color{dodgerblue}{{\text{ Prior }}}$$

If $\theta$ is a continuous r.v. with $\color{dodgerblue}{\text{prior p.d.f.}}$ with $\color{dodgerblue}{g(\theta)}$, then its $\color{orangered}{\text{posterior p.d.f.}}$ with $\color{orangered}{f(\theta\|D)}$ is given by

$$\color{orangered}{f(\theta|D)}=\color{b}{\frac{\color{lightgreen}{Pr(D|\theta)}\color{b}{\times}\color{dodgerblue}{g(\theta)}}{Pr(D)}}$$ 

Here, for MAP, since we decide likelihood function with binomial, we can choose beta distribution as prior (details told in Conjugate Priors). Therefore, we have following induction:

$$
\begin{aligned}
\hat\theta_{MAP}
& =\arg{\max_{\theta}}{\ Pr(\theta|D)}\\
& =\arg{\max_{\theta}}{\ Pr(D|\theta)\cdot{Pr(\theta)}}\\
& =\arg{\max_{\theta}}{\ \theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}\\
& =\frac{x+\alpha-1}{n+\alpha+\beta-2}
\end{aligned}
$$

#### **Conjugate Priors**

If the posteriors and priors have the same function form, we call those priors $\color{dodgerblue}{\textbf{conjugate priors}}$. The most famous prior is $\color{dodgerblue}{\textbf{beta distributions}}$, which is a convenient prior for binonmial likelihood and has two parameters $\alpha$ and $\beta$:

$$ 
\begin{aligned}
\color{dodgerblue}{g(\theta)=\mathcal{B}(\theta|\alpha,\beta)}\color{b}{=\frac{1}{\color{violet}{\text{Beta}(\alpha,\beta)}}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}}
\end{aligned}
$$

Here, the normalizing constant $\color{violet}{\text{Beta}(\alpha,\beta)}$ is the $\color{violet}{\textbf{beta function}}$.

$$ 
\color{violet}{\text{Beta}(\alpha,\beta)=\int_{0}^{1}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}{d{\theta}}=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}}
$$

Above equation is to ensure that integral of $\color{dodgerblue}{g(\theta)\text{ or }\mathcal{B}(\theta|\alpha,\beta)}$ is one.

#### **General Cases for Posterior of Binomial Distribution**

Given our observations $D=(x,n)$, we can now compute the posterior distribution of $\theta$:

$$
\color{orangered}{f(\theta|x,n,\alpha,\beta)}
\color{b}{=\frac{\color{lightgreen}{Pr(x|n,\theta)}\color{b}{\times}\color{dodgerblue}{g(\theta|\alpha,\beta)}}
{\color{violet}{\int{Pr(x|n,\theta)g(\theta|\alpha,\beta)}d{\theta}}}}
$$

First, we can handle the normalization constant $\color{violet}{Pr(x|n,\alpha,\beta)}$:

$$
\begin{aligned}
{\color{violet}{\int{Pr(x|n,\theta)g(\theta|\alpha,\beta)}d{\theta}}}
&= {\int_{0}^{1}{\binom{n}{x}{\theta}^{x}{(1-\theta)}^{n-x}} 
\color{b}{\times\frac{1}{\text{Beta}(\alpha,\beta)}}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}d{\theta}}\\
&= \frac{\binom{n}{x}}{\text{Beta}(\alpha,\beta)}\times{\int_{0}^{1}{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}d{\theta}}\\
&= \frac{\binom{n}{x}}{\text{Beta}(\alpha,\beta)}\times{{\text{Beta}(x+\alpha,n-x+\beta)}}
\end{aligned}
$$

Second, we can expand and simplify numerator with:

$$
\begin{aligned}
\color{lightgreen}{Pr(x|n,\theta)}\color{b}{\times}\color{dodgerblue}{g(\theta|\alpha,\beta)}
&= \color{lightgreen}{\binom{n}{x}{\theta^{x}}{(1-\theta)^{n-x}}}
\color{b}{\times}
\color{dodgerblue}
{\frac{1}{\text{Beta}(\alpha,\beta)}}{\theta^{\alpha-1}(1-\theta)^{\beta-1}}\\
&= \frac{\binom{n}{x}}{\text{Beta}(\alpha,\beta)}\times{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}
\end{aligned}
$$


Hence, $\color{orangered}{f(\theta|x,n,\alpha,\beta)}$ have:

$$
\begin{aligned}
\color{orangered}{f(\theta|x,n,\alpha,\beta)}
&= \color{b}{\frac{\color{lightgreen}{Pr(x|n,\theta)}\color{b}{\times}\color{dodgerblue}{g(\theta|\alpha,\beta)}}
{\color{violet}{\int{Pr(x|n,\theta)g(\theta|\alpha,\beta)}d{\theta}}}}\\
& = \frac{\frac{\binom{n}{x}}{\text{Beta}(\alpha,\beta)}\times{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}}
{\frac{\binom{n}{x}}{\text{Beta}(\alpha,\beta)}\times{{\text{Beta}(x+\alpha,n-x+\beta)}}}\\
&= \frac{1}
{{\text{Beta}(x+\alpha,n-x+\beta)}}\times{\theta^{x+\alpha-1}(1-\theta)^{n-x+\beta-1}}\\
&= \mathcal{B}(x+\alpha, n-x+\beta)
\end{aligned}
$$

The posterior $\color{orangered}{f(\theta|x,n,\alpha,\beta)}$ is therefore another beta distribution with parameters $(x+\alpha,n-x+\beta)$. 

And we find out posterior is still beta distribution with different parameters. The interpreatation of parameters are usually considered as **pseudocount**.

Their plot are like the following picture:

<center>
<img class="center large" src=".//bml/001.png" height="50%" width="70%">
</center>

#### **Special Case for Prior**

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

<!-- #### **Posterior Predictive Distributions**

With posterior function $\color{orangered}{\textbf{(conjugate priors)}}$ of $\color{orangered}{f(\theta\|D)}$ on parameters $\theta$ given observations $D$, we can compute a distribution on future observations that does not depend on assuming any particular parameter values.

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
& = \color{b}{\frac{(n+\alpha+\beta-1)!}{(x+\alpha-1)!(n-x+\beta-1)!}}\color{violet}{\text{ Beta}(x+\alpha,n-x+\beta)}\\
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

$$Pr(x_1,x_2,x_3|\theta_1,\theta_2,\theta_3)=\frac{(x_1+x_2+x_3)!}{{x_1}!{x_2}!{x_3}!}{\ \theta_1^{x_1}}{\theta_2^{x_2}}{\theta_3^{x_3}}$$ -->



