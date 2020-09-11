---
layout: notes
section-type: notes
title: Machine Learning
category: ml
---

* TOC
{:toc}
---

## Similar Courses
* [Washu CSE 417T: Intro to Machine Learning](https://classes.cec.wustl.edu/~SEAS-SVC-CSE417T/)
* [NTU Machine Learning Foundation](https://www.csie.ntu.edu.tw/~htlin/course/ml13fall/)

## Recommended Books

* [Matrix Cookbook](http://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf)
* [Learning From Data (Color)](https://heming-zhang.github.io/course/Learning_From_Data(Color).pdf)
* [Learning From Data (2012)](https://heming-zhang.github.io/course/Learning_From_Data(2012)-Abu-Mostafa.pdf)
* [Computer Age Statistical Inference](https://heming-zhang.github.io/course/[Bradley_Efron,_Trevor_Hastie]_Computer_Age_Statis(z-lib.org).pdf)



## Chapter 1 The Learning Problem
### 1.1 Formal Setup
> * unknown target function$f:\mathcal{X}\rightarrow\mathcal{Y}$
> * training data $\mathcal{D}$
> * hypothesis set $\mathcal{H}$
> * learning algorithm $\mathcal{A}$
> * learned hypothesis $\mathcal{H}$, and $\mathcal{H}\ni g\approx{f}$
>
> $\mathcal{H,A}$ will be called as learning model, this is what we can control.

### 1.2 Perceptron
> * Input $\mathcal{X}\in\mathbb{R}^n$ ($\mathbb{R}^{n}$ is the $n$-dimensional Euclidean space)
> * Output $\mathcal{Y}\in \{+1,-1\}$
> * Give a sign function 
> 
> $$
h(\mathbf{x})=
\begin{cases}
    +1\ \ if\sum_{i=1}^{2}w_{i}x_{i}-b>0 \\
    -1\ \ otherwise
\end{cases}
$$
>
> * This can also be expressed in this way:
>
> $$
h(\mathbf{x})=sign((\sum_{i=1}^{n}w_{i}x_{i})+b)
$$
>
> To simplify the noation of the perceptron formula, we will treat the bias $b$ as a weight $w_0=b$ and merge it with the other weights into one vector $\mathbf{w}=[w_0,w_1,\cdots,w_n]^{T}$,where $^{T}$ denotes the transpose of a vector, so $\mathbf{w}$ is a column vector. We also treat $\mathbf{x}$ as a column vector and modify it to become $\mathbf{x}=[x_0,x_1,\cdots,x_n]^T(where\ x_0=1)$, therefore $\mathbf{x}=(x_1, x_2,\cdots,x_n)\in\mathbb{R}^{n}$

> * With such convention, we will have 
>
> $$\mathbf{w}^{T}\mathbf{x}=\sum_{i=0}^{d}w_ix_i$$
>
> * Tips: 
>
> $$
\mathbf{w}^T\mathbf{x}=[w_0,w_1,\cdots,w_n]
\left[
 \begin{matrix}
   x_0\\
   x_1\\
   .\\
   .\\
   .\\
   x_n
  \end{matrix}
\right]
=
w_0x_0+w_1x_1+\cdots+w_nx_n=\sum_{i=0}^{n}w_ix_i
$$
>
> * **Finally, we will get** 
>
> $$h(\mathbf{x})=sign(\mathbf{w}^T\mathbf{x})$$

<span id = "jump3"></span>

### 1.3 Perceptron Learning Algorithm(PLA)

> * This algorithm will determine what $\mathbf{w}$ should be
> * Assume data set is linearly separable, which means that there is a vector $w$ that makes formula$(1)$ achienve the correct decision $h(\mathbf{x}_n)=y_n$ on all the traing examples.
> * We will use iterative method to find $\mathbf{w}$. At iteration $t$, where $t=0,1,2,\cdots$, there is a current value of the weight vector, call it $\mathbf{w}(t)$. Then the algorithm will pick one of misclassified examples, called $(\mathbf{x}(t),y(t))$, and uses it to update $\mathbf{w}(t)$. And the update rule is
> 
> $$\mathbf{w}(t+1)=\mathbf{w}(t)+y(t)\mathbf{x}(t)$$
>
> * Tip1: $y(t)$ and $\mathbf{x}(t)$ are actully $y_{n(t)}$, $\mathbf{x}_{n(t)}$ in short.
> 
> * Tip2: $y(t)$ and $\mathbf{x}(t)$ is a point from training data set $\mathcal{D}=\{(\mathbf{x_1}, y_1), (\mathbf{x_2}, y_2),\cdots,(\mathbf{x_i}, y_i),\cdots,(\mathbf{x_n}, y_n)\}$
>
> * Intution
>    * Suppose $(\mathbf{x},y)\in\mathcal{D}$ is a misclassified training example and $y=+1$
>        * $\mathbf{w}^T\mathbf{x}$ is negative
>        * After updating $\mathbf{w}'=\mathbf{w}+y\mathbf{x}$
>        * $\mathbf{w}'^T\mathbf{x}=(\mathbf{w}+y\mathbf{x})^T\mathbf{x}=\mathbf{w}^T\mathbf{x}+y\mathbf{x}^T\mathbf{x}$ is less negative that $\mathbf{w}^T\mathbf{x}$
>    * A similar arguments holds if $y=-1$
>    * This will make $\mathbf{w}^T\mathbf{x}$ closer to 0.

* [PLA extension reading](https://www.csie.ntu.edu.tw/~htlin/course/ml13fall/doc/02_handout.pdf)

### 1.5 Is learning feasible?

> * A random sample is picked from bin of orange and green marbles. $\mu$ represents the probability of orange marbles in the bin, and $v$ represents the fraction of orange marbles in the sample. 



### 1.6 **Hoeffding Inequality**

$$\mathbb{P}[|v-\mu|<\epsilon]\leq{2e^{-2\epsilon^2n}},\  \mathbf{for\ any\ \epsilon>0}$$

> Here, the training sample play the role of a sample from the bin. If the inputs $\mathbf{x}_1, \cdots, \mathbf{x}_n$ in $\mathcal{D}$ are picked from independently according to $P$, we will get a random sample of red $(h(\mathbf{x})\neq{f(\mathbf{x})})$ and $(h(\mathbf{x}) = {f(\mathbf{x})})$ points. 

> Each point will be red with probability $\mu$ and green with probability $1-\mu$. The color of each point will be known to us since both $h(\mathbf{x}_i)$ and $f(\mathbf{x}_i)$ are known to us for $i=1,2,\cdots,n$.

### 1.7 Connection to Machine Learning

> **Probability Rescue**
>
> $$E_{out}(h)=\mathbb{P}[|h(\mathbf{x})\neq{f(\mathbf{x})}|]=\mu$$
> 
> $$E_{in}(h)=\frac{1}{n}\sum_{i=1}^{n}[|h(\mathbf{x_i})\neq{f(\mathbf{x_i})}|]=v$$
>
> **Using Hoeffding Inequality**
>
> $$\mathbb{P}[|E_{in}(h)-E_{out}(h)|>\epsilon]\leq{2e^{-2\epsilon^2n}}$$
>
> Therefore, if we can have enough data $n$, we may get close to $E_{in}(h)\approx{E_{out}(h)}$
>
> Hence, 
>
> $$\mathbb{P}_{\mathcal{D}}[\mathbf{BAD}\ \mathcal{D}\ for\ h]$$ 
>
> means 
>
> $$|E_{in}(h)-E_{out}(h)|>\epsilon$$
>
>where $\epsilon$ is very large, which is quite impossible to happen to collect a bad training data set.


> **Using union probability formula**:
>
> $$\sum_{i=1}^n{P(B_i)P(A|B_i)}$$
>
> $$\mathbb{P}_{\mathcal{D}}[\mathbf{BAD}\ \mathcal{D}] = \sum_{All\ Possible\ \mathcal{D_i \in D}}\mathbb{P}(\mathcal{D_i})\cdot\mathbb{P}_{\mathcal{D_i}}[\mathbf{BAD}\ \mathcal{D_i}]$$
>
> That is the situation for one $h\in\mathcal{H}$. Say we get many $h_i\in\mathcal{H}$, and we get the final hypothesis $g$. We can try to bound this by:
>
> $$
\begin{aligned}
\mathbb{P}[|E_{in}(g)-E_{out}(g)|\geq\epsilon]\ \leq\ \mathbb{P}[|E_{in}(h_1)-E_{out}(h_1)|\\
\mathbf{or}|E_{in}(h_2)-E_{out}(h_2)|\\
\cdots \cdots \\
\mathbf{or}|E_{in}(h_m)-E_{out}(h_m)|\\
=\sum_{i=1}^{m}\mathbb{P}[|E_{in}(h_i)-E_{out}(h_i)|\geq\epsilon]\\
= 2me^{-2\epsilon^2n}
\end{aligned}
$$


* Tips: Normal Distribution = Gussian Distribition


### 1.8 Error and Noise

<center>
<img class = "medium" src=".//ml_pictures/ml008.png" height="55%" width="55%">
</center>

> * For coupon, we can consider false positive is small error.
> * For unlock important files, we will think false negative is small error. (For safety, ourselves may not able to open it everytime.)
> 
> * For noise, target function is not determinstic. It is **stocastic**.
>* Instead of get a target function, we will have a target distribution

> Instead of 
>
> $$y=f(x),P\{y|\mathbf{x}\}$$
> 
> we will have
>
> $$y=f(\mathbf{x})+\epsilon\ ,where\ \epsilon\in{N(0,\delta^2)}$$


## Chapter2 Training Versus Testing

### 2.1 Theory of Generalization

<center>
<img class = "large" src=".//ml_pictures/ml009.png" height="65%" width="65%">
</center>


> $$\delta = 2me^{-2\epsilon^2n}$$
>
> $$\mathbb{P}[|E_{in}(g)-E_{out}(g)|\geq\epsilon]\ \leq{\delta}$$
>
> $$\mathbb{P}[|E_{in}(g)-E_{out}(g)|\leq\epsilon]\ \geq1-{\delta}\tag{*}$$
> 
> $$\mathbb{P}[E_{in}(g)-E_{out}(g)\leq\epsilon\cap{E_{out}(g)-E_{in}(g)\leq\epsilon}]\ \geq1-{\delta}\tag{**}$$
>
> Since we have:
> 
> $$P(A\cap{B})\leq{P(A)}$$
>
> $$P(A\cap{B})\leq{P(B)}$$
> 
> Therefore, continue on (**), we have
> 
> $$\mathbb{P}[E_{out}(g)\leq{E_{in}(g)+\epsilon}]\geq1-{\delta}$$
> 
> At here, we can say that 
> 
> $$E_{out}(g)\leq{E_{in}(g)+\epsilon},\ \mathbf{with\ the\ probability\ of\ {1-\delta}}$$
>
> **The Union Bound is Bad**
>    * Therefore, can we group our hypothesis in kind os that to avoid similar result to make bound bad?

### 2.2 Effective Number of Hypothesis

> * If we get 5 points, and the dichotomies generated can be only 22.
>    * we can count it by calculate the circumstances of points aside.
>    * 0 point: 1*2 (Also 5 Points)
>    * 1 point: 5*2 (Also 4 Points)
>    * 2 points: 5*2 (Also 3 Points)
>    * Add them up is: 22 which is less than $2^5=32$


> We may replace $m$ in the formula with effective$(n)$， therefore we will have
>
> $$\mathbb{P}[|E_{in}(g)-E_{out}(g)|<\epsilon]\leq{2\cdot{effective(n)}\cdot{e^{-2\epsilon^2n}}}$$
>
> At here, $effective(N)<<2^n$
>
> Let $\mathbf{x_1,x_2,\cdots,x_n}\in\mathcal{X}$. The **dichotomies** generated by $\mathcal{H}$ on these points are defined by
>
> $$\mathcal{H}(\mathbf{x_1,\cdots,x_n})=\{(h(\mathbf{x_1}),\cdots,h(\mathbf{x_n}))| h\in\mathcal{H} \}$$
>
> And we know $h(\mathbf{x_1}),\cdots,h(\mathbf{x_n})\in \{+1,-1\}^{n}$ 
> And we also know dichotomies $\mathcal{H}(\mathbf{x_1,\cdots,x_n})$ is also a set of **hypothesis** just like hypothesis $\mathcal{H}$. The difference here is: One has upper bound, and one is possibly infinite.

> The Growth Function can be defined for a hypothesis set $\mathcal{H}$ by
>
>$$m_{\mathcal{H}}(n)=\max_{\mathbf{x_1,\cdots,x_n}\in\mathcal{X}}{|\mathcal{H}(\mathbf{x_1,\cdots,x_n})|}$$
>
> In words, the $m_{\mathcal{H}}(n)$ is the maximum number of dichotomies that can be generated by $\mathcal{H}$ on any $n$ points.
>
> Therefore, if $\mathcal{X}$ is a Euclidean plane, and $\mathcal{H}$ is a two-dimensional perceptron, what are $m_{\mathcal{H}}(3)$ and $m_{\mathcal{H}}(4)$?
>    * $m_{\mathcal{H}}(3)=8$
>    * $m_{\mathcal{H}}(4)=14$
>
> For following cases:
>    * Positive Rays: $m_{\mathcal{H}}(n)=n+1$
>    * Positive Intervals: $m_{\mathcal{H}}(n)=C_{n+1}^{2}$
>    * Convex Set: $m_{\mathcal{H}}(n)=2^{n}$  
>
> **Break Point**: If no data set of size $k$ can be shattered by $\mathcal{H}$, then $k$ is said to be a break point for $\mathcal{H}$.
>
> Thus we will have $m_{\mathcal{H}}(k)=2^k$

<center>
<img class = "medium" src=".//ml_pictures/ml011.png" height="50%" width="50%">
</center>

<span id="jump"></span>

> **CONCLUSION:** If there is a break point here, we know that $m_{\mathcal{H}}(n)=O(n^{k-1})$, $k$ is the break point number, which demonstrates that $m_{\mathcal{H}}(n)$ is a polynomial instead of exponential.


### 2.4 The VC Generalization Bound

> The Vapornik-Chervonenkis(VC)-Bound
>
> $$\mathbb{P}\{|E_{in}(g)-E_{out}(g)|>\epsilon\}\leq{4m_{\mathcal{H}}(2n)e^{-\frac{1}{8}\epsilon^2{n}}}$$
>
> which is also 
>
> $$E_{in}(g)-\sqrt{\frac{8}{n}\log{\frac{4m_{\mathcal{H}}(2n)}{\delta}}}\leq{E_{out}(g)}\leq{E_{in}(g)+\sqrt{\frac{8}{n}\log{\frac{4m_{\mathcal{H}}(2n)}{\delta}}}}$$
>
> But we only care about what happened in RHS, which could tell us worst situation
>
>
> $$E_{out}(g)\leq{E_{in}(g)+\sqrt{\frac{8}{n}\log{\frac{4m_{\mathcal{H}}(2n)}{\delta}}}},\ \mathbf{with\ the\ probability\ of\ }{1-\delta}$$
>
> From the break point section, we have one more theorem that, if $k^{*}$ is the smallest break point for $\mathcal{H}$. Then
> 
> $$m_{\mathcal{H}}(n)\leq{n^{k^{*}-1}+1}$$  
>
> * $d_{VC}(\mathcal{H})=k^{*}-1$
> * $m_{\mathcal{H}}(n)\leq{n^{k^{*}-1}+1}=n^{d_{VC}}+1$

> **Then we will have following derivative**:
>
> $$E_{out}(g)\leq{E_{in}(g)+\sqrt{\frac{8}{n}\log{\frac{4m_{\mathcal{H}}(2n)}{\delta}}}}$$
>
> $$=E_{in}(g)+\sqrt{\frac{8}{n}\log{\frac{4[(2n)^{d_{VC}}+1]}{\delta}}}$$
> 
> $$=E_{in}(g)+\sqrt{\frac{8}{n}\log{\frac{4+4(2)^{d_{VC}}\cdot{n^{d_{VC}}}}{\delta}}}$$
> 
> $$=E_{in}(g)+O(\sqrt{\frac{8}{n}\log{\frac{4+4(2)^{d_{VC}}\cdot{n^{d_{VC}}}}{\delta}}})$$
> 
> $$=E_{in}(g)+O(\sqrt{\frac{1}{n}\log{\frac{n^{d_{VC}}}{\delta}}})$$
> 
> $$=E_{in}(g)+O(\sqrt{\frac{d_{VC}\log{n}}{n}})$$
>
> And if $n\rightarrow{\infty}$, then $\sqrt{\frac{8}{n}\log{\frac{4m_{\mathcal{H}}(2n)}{\delta}}}\rightarrow{0}$, ( since $\lim_{n\rightarrow{\infty}}{\frac{\log{n}}{n}}=0$)
> Therefore, $E_{out}(g)\rightarrow{E_{in}(g)}$, as $n\rightarrow{\infty}$, with the probability of $1-\delta$

### 2.5 Sample Complexity
> * How many samples do we need in out training data to say that the generalization error is less than $\epsilon$ with the probability of $1-\delta$
> 
> * Set $\sqrt{\frac{8}{n}\log{\frac{4+4(2)^{d_{VC}}\cdot{n^{d_{VC}}}}{\delta}}}\leq{\epsilon}$
>
> * We can conclude that we need $n\geq{\frac{8}{\epsilon^2}\log({\frac{4[(2n)^{d_{VC}}+1]}{\delta}}) }$
>
> * Practical Rule of Thumb: $n\geq{10d_{VC}}$

### 2.6 Approximation Generalization Tradeoff

> When you select your hypothesis set, you should balance these two conflicting goals:
>    * (1) To have some hypothesis $\mathcal{H}$ that can approximate $f$
>    * (2) To enable the data to zoom in on the right hypothesis

<span id="jump1"></span>

* VC Analysis on Generalization

<center>
<img class = "large" src=".//ml_pictures/ml014.png" height="55%" width="70%">
</center>

* VC Analysis with VC-Dimension

<center>
<img class = "large" src=".//ml_pictures/ml015.png" height="55%" width="70%">
</center>

### 2.7 Bias-Variance Tradeoff

> * We can use some squared-error measures to decompose it to bias-variance.
>
>$$E_{out}(g_{\mathcal{D}})=\mathbb{E}_{\mathbf{x}\sim\mathcal{P}}[(g_{\mathcal{D}}(\mathbf{x})-f(\mathbf{x}))^2]$$
>
>* To deal with composition, we have:
>
>$$
\begin{aligned}
\mathbb{E}_{\mathcal{D}}  [E_{out}(g_{\mathcal{D}})]
&=\mathbb{E_{\mathcal{D}}}\Big[\mathbb{E}_{\mathbf{x}}[( g_{\mathcal{D}}(\mathbf{x})-f(\mathbf{x}))^2]\Big] \\
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[( g_{\mathcal{D}}(\mathbf{x})-f(\mathbf{x}))^2]\Big]\\
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2-2g_{\mathcal{D}}(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2]\Big]\\
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2]-2\bar{g}(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2\Big]
\end{aligned}
$$
>
>$$\mathbf{where\ \ }\mathbb{E}_{\mathcal{D}}[g_{\mathcal{D}}(\mathbf{x})]=\bar{g}(\mathbf{x})\approx{\frac{1}{k}}{\sum_{i=1}^{k}}g_{\mathcal{D_i}}(\mathbf{x})$$
>
>$$
\begin{aligned}
\mathbb{E}_{\mathcal{D}}  [E_{out}(g_{\mathcal{D}})]
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2]-2\bar{g}(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2\Big]\\
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2]- \bar{g}(\mathbf{x})^2 + \bar{g}(\mathbf{x})^2 -2g(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2\Big]\\
&=\mathbb{E_{\mathbf{x}}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2- \bar{g}(\mathbf{x})^2] + \Big(\bar{g}(\mathbf{x}) -f(\mathbf{x})\Big)^2\Big]\\
&=\mathbb{E}_{\mathbf{x}}\big[\mathbf{Variance\ of\ }g_{\mathcal{D}}(\mathbf{x})+\mathbf{Bias\ of\ }\bar{g}_{\mathcal{D}}(\mathbf{x})  \big]
\end{aligned}
$$

<span id="jump2"></span>

* Bias-Variance Analysis on Function

<center>
<img class = "large" src=".//ml_pictures/ml016.png" height="55%" width="70%">
</center>

* Bias-Variance Analysis on Hypothesis Complexity

<center>
<img class = "large" src=".//ml_pictures/ml017.png" height="55%" width="70%">
</center>

> When hypothesis sets grows from 2 to 5, the bias will not change but the variance will decrease for the more complex hypothesis set
>
> At here, we form 2 important analysis approaches
>    * [VC Analysis](#jump1)
>    * [Bias-Variance Analysis](#jump2)


<center>
<img class ="medium" src=".//ml_pictures/ml018.png" height="50%" width="50%">
</center>


### 2.8 Test Sets
> Instead of bounding $E_{out}(g)$ using $E_{in}(g)$, estimate $E_{out}(g)$ using the error on some test dataset $\mathcal{D'}$
>    * $E_{test}(g)$= error on the test dataset

<center>
<img class = "medium" src=".//ml_pictures/ml019.png" height="55%" width="55%">
</center>

> Test Sets will occupy some resources of training data, therefore, basically, we will choose 70-80% training and 20-30% testing

## Chapter 3 Linear Model

### 3.1 Non-separable Data
* 

* To find a hypothesis with the minimum $E_{in}$, we need to solve the combinatorial optimaztion problem:

$$E_{in}(\mathbf{w})=
min_{\mathbf{w}\in{\mathbb{R^{d+1}}}}{\frac{1}{n} 
\sum_{i=1}^{n}[|sign(\mathbf{w^{T}x})\neq{y_i}|]}$$

* Since [PLA](#jump3) will never terminate for non-linear separable data, we may adjust that algorithm with **Pocket Algorithm**:

<center>
<img class = "large" src=".//ml_pictures/ml021.png" height="65%" width="65%">
</center>

### 3.2 Linear Regression



### 3.3 Linear Regression Algorithm

<center>
<img class = "large" src=".//ml_pictures/ml022.png" height="70%" width="70%">
</center>

### 3.4 Logistic Regression

> * We will use new sigmoid function
> 
> $$h(\mathbf{x})=\theta(\mathbf{w^Tx})$$
> 
> * $\theta$ is a function which show the probability with range [0,1]
<center>
<img class = "large" src=".//ml_pictures/ml023.png" height="60%" width="70%">
</center>

> * Predicting Probabilities
>     * Training data does not consist of probabilities
>     * Observation are still **binary**: $y_i=\pm1$
>     * Our Goal is to learn $f(\mathbf{x})=P(y=+1\|\mathbf{x})$ (This means that we need to give a probability of $\mathbf{x}$ being $+1$)
> 
> * Therefore, we can rewrite the target goal $f(\mathbf{x})=P(y=+1\|\mathbf{x})$ as
>
> $$
P(y|\mathbf{x})=   
\begin{cases}
f(\mathbf{x}), & for\ y=+1\\
1-f(\mathbf{x}), & for\ y=-1
\end{cases}
$$



### 3.10 Nonlinera Transformation

<center>
<img class="center large" src=".//ml_pictures/ml029.png" height="70%" width="70%">
</center>

> Instead of Using $h(\mathbf{x})=f(\mathbf{w^Tx})$, we will set $\tilde{h}(\mathbf{z})=f({\mathbf{\tilde{w}^Tz}})$ where $\mathbf{z}=\Phi({\mathbf{x}})$
> 
> Example for setting $\mathbf{z}$:
>
> Through viewing the data figure, we can find out that it seems like a circle here, and we can set
>
>$$
\begin{aligned}
x_1^2+x_2^2&=0.6\\
\mathbf{z}=\Phi(\mathbf{x})&=(1,x_1^2,x_2^2)\\
\end{aligned}
$$
>
> Or if we can set
>
>$$
\begin{aligned}
\mathbf{z}=\Phi(\mathbf{x})&=[1,(x_1-0.5)^2,(x_2-0.5)^2)]
\end{aligned}
$$

* Therefore, the nonlinear model is
<center>
<img class="center large" src=".//ml_pictures/ml030.png" height="50%" width="70%">
</center>

* Figures to show this procedures:

<center>
<img class="center medium" src=".//ml_pictures/ml031.png" height="50%" width="50%">
</center>

* The cost of doing kernel function is: we may extend the dimension of original data set, which can loose the bound for $E_{out}$. Especially, if $\tilde{d}\gg{d}$, then the learned hypothesis will not genralized well:

<center>
<img class="center large" src=".//ml_pictures/ml032.png" height="50%" width="70%">
</center>

### 3.11 kth-Order Transformation

* Notice that what we do above can just be suitable for circle but not for other universal quadratic conditions like Ellipses. Therefore, we need to set more general quadratic transformation

$$\mathbf{z}=\Phi_{2}(\mathbf{x})=[1,x_1,x_2,x_1^2,x_1x_2,x_2^2,]$$

* Similiarly, we have

<center>
<img class="center large" src=".//ml_pictures/ml033.png" height="50%" width="70%">
</center>

## Chapter 4 Overfitting

* Error and Generlization
<center>
<img class="center medium" src=".//ml_pictures/ml034.png" height="50%" width="50%">
</center>

* Error and Model Complexity
<center>
<img class="large" src=".//ml_pictures/ml035.png" height="50%" width="50%">
</center>

* Cause for Overfitting
    * Too complexity: High kth-Order=>High VC-dimension: drive too fast
    * Noise: bumpy road
    * Too limited data: not familiar with road conditions

### 4.1 Conditions for Overfitting (1) Noise

<center>
<img class="center medium" src=".//ml_pictures/ml036.png" height="50%" width="50%">
</center>

* Explaination: Learning Curve

<center>
<img class="center medium" src=".//ml_pictures/ml038.png" height="50%" width="50%">
</center>

The figure above shows that in the shady area, which means we have limited data samples. The complex model($\mathcal{H_{10}}$) have larger $E_{out}$ than simple model ($\mathcal{H_{2}}$).

* Data from 20 to 100 (increase learning data set)

* Less Data with 20 Points

<center>
<img class="center large" src=".//ml_pictures/ml039.png" height="50%" width="70%">
</center>

* More Data with 100 Points

<center>
<img class="center large" src=".//ml_pictures/ml040.png" height="50%" width="70%">
</center>

After increasing number of data, the complex model($\mathcal{H_{10}}$) wins.

### 4.2 Conditions for Overfitting (2) Deterministic Noise

* Deterministic Noise can be calculated.

<center>
<img class="center medium" src=".//ml_pictures/ml042.png" height="50%" width="50%">
</center>

* At here, $Q_f$ stands for the kth-Order of the function.

<center>
<img class="center large" src=".//ml_pictures/ml041.png" height="50%" width="70%">
</center>

### 4.3 Bias-Variance Analysis for Noise

> $$y=f(\mathbf{x})+\epsilon$$
> 
> * $\epsilon$ is the Gussian Distribution Noise
> 
> $$
\begin{aligned}
\mathbb{E}_{\mathcal{D}}  [E_{out}(g_{\mathcal{D}})]
&=\mathbb{E_{\mathcal{D}}}\Big[ \mathbb{E}_{\mathbf{x},y}[( g_{\mathcal{D}}(\mathbf{x})-y(\mathbf{x}))^2] \Big]\\ 
&=\mathbb{E}_{\mathbf{x},y}\Big[ \mathbb{E}_{\mathcal{D}}[( g_{\mathcal{D}}(\mathbf{x})-f(\mathbf{x})-\epsilon)^2]\Big]\\
&=\mathbb{E}_{\mathbf{x},y}\Big[\mathbb{E}_{\mathcal{D}}\big[ g_{\mathcal{D}}(\mathbf{x})^2-2g_{\mathcal{D}}(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2-2{\epsilon}\big(g_{\mathcal{D}}(\mathbf{x})-f(\mathbf{x})\big)+ {\epsilon}^2 \big]\Big]
\end{aligned}
$$

<center>
<img class="center large" src=".//ml_pictures/ml058.png" height="50%" width="70%">
</center>

> Therefore, we have
> 
> $$
\begin{aligned}
\mathbb{E}_{\mathcal{D}}[E_{out}(g_{\mathcal{D}})]
&=\mathbb{E}_{\mathbf{x},y}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2]-2\bar{g}(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2+{\epsilon}^2\Big]\\
&=\mathbb{E}_{\mathbf{x},y}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2]- \bar{g}(\mathbf{x})^2 + \bar{g}(\mathbf{x})^2 -2g(\mathbf{x})f(\mathbf{x})+f(\mathbf{x})^2+{\epsilon}^2 \Big]\\
&=\mathbb{E}_{\mathbf{x},y}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2- \bar{g}(\mathbf{x})^2] + \Big(\bar{g}(\mathbf{x}) -f(\mathbf{x})\Big)^2+{\epsilon}^2 \Big]\\
&=\mathbb{E}_{\mathbf{x}}\Bigg[\mathbb{E}_{y|\mathbf{x}}\Big[[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2- \bar{g}(\mathbf{x})^2] + \Big(\bar{g}(\mathbf{x}) -f(\mathbf{x})\Big)^2|\mathbf{x}\Big]\Bigg]+\mathbb{E}_{\mathbf{x},y}[\epsilon^2]   \\
&=\mathbb{E}_{\mathbf{x}}\Big[\mathbb{E}_{\mathcal{D}}[ g_{\mathcal{D}}(\mathbf{x})^2- \bar{g}(\mathbf{x})^2] + \Big(\bar{g}(\mathbf{x}) -f(\mathbf{x})\Big)^2\Big]+\mathbb{E}_{\mathbf{x},y}[\epsilon^2]   \\
&=\mathbb{E}_{\mathbf{x}}[\mathbf{Variance\ of}\ \bar{g}_{\mathcal{D}}(\mathbf{x})]+\mathbb{E}_{\mathbf{x}}[\mathbf{Deterministic\ noise\ of}\ \bar{g}(\mathbf{x})]   +\mathbb{E}_{\mathbf{x},y}[\epsilon^2]\\
&=\mathbb{E}_{\mathbf{x}}[\mathbf{Variance\ of}\ \bar{g}_{\mathcal{D}}(\mathbf{x})]+\mathbb{E}_{\mathbf{x}}[\mathbf{Deterministic\ noise\ of}\ \bar{g}(\mathbf{x})]+{\sigma}^2
\end{aligned}
$$

### 4.4 Solutions for Overfitting

> * Start from simple model
> * data cleaning / pruning
> * data hinting
> * regularization
> * validation


### 4.5 Regularization

> Idea: 'Step Back' from 
> $$\mathcal{H}_{10}\ to\ \mathcal{H}_{2}$$

<center>
<img class="large" src=".//ml_pictures/ml059.png" height="50%" width="50%">
</center>

> Example
> $$\mathcal{H}_{2}\ \text{is}\ \mathcal{H}_{10} \text{with certain constraint.}$$

* 10-th Polynomials
<center>
<img class="center large" src=".//ml_pictures/ml044.png" height="50%" width="70%">
</center>

* 2-nd Polynomials
<center>
<img class="center large" src=".//ml_pictures/ml045.png" height="50%" width="70%">
</center>


### 4.6 Regression with Soft Constraints

<center>
<img class="center large" src=".//ml_pictures/ml046.png" height="50%" width="70%">
</center>

We will generate a hypothesis set, which is looser than $\mathcal{H}_{2}$, but less risky than $\mathcal{H}_{10}$

<center>
<img class="center large" src=".//ml_pictures/ml047.png" height="50%" width="70%">
</center>


Solving the optimization based on a contriant
<center>
<img class="center large" src=".//ml_pictures/ml048.png" height="50%" width="70%">
</center>

Special conditions when constraint contains the solutions, we certainly will get

$$ \mathbf{w}_{reg}= \mathbf{w}_{lin}$$

Just like the picture below

<center>
<img class="center large" src=".//ml_pictures/ml049.png" height="50%" width="70%">
</center>

### 4.7 The Lagrange Multiplier
* More common conditions: using convex optimization
* At here, $X\in{\mathbb{R}^{n\times{d}}}$ and $\mathbf{w}_{d\times1}$

<center>
<img class="large" src=".//ml_pictures/ml060.png" height="50%" width="50%">
</center>

> For the condition above, $\mathbf{w}$ cannot be the optimal because $\nabla{E_{in}}(\mathbf{w})$ is not parallel to the red normal vector. Since in this condition, we can decrease $\nabla{E_{in}}(\mathbf{w})$ without violating the constraint.(Green Arrow on the figure above), and therefore, we can move closer to $\mathbf{w}$ without violating constraint.
> 
> Therefore, for the optimal solution $\mathbf{w}_{reg}$, we have
> 
> $$-\nabla{E}_{in}(\mathbf{w}_{reg})\propto{\mathbf{w}_{reg}}$$

And the figure below just show its geometric meaning

<center>
<img class="center large" src=".//ml_pictures/ml050.png" height="50%" width="70%">
</center>

To solve the last line equation above, we should transfer it into the formula below:

<center>
<img class="center large" src=".//ml_pictures/ml051.png" height="50%" width="70%">
</center>

* Ridge Regression
    * If given $\lambda_{C}$, we can get the solution $\mathbf{w}_{reg}$

<center>
<img class="center large" src=".//ml_pictures/ml052.png" height="50%" width="70%">
</center>

* Ridge Regression Example
    * When we do not know $\lambda_{C}$

<center>
<img class="center large" src=".//ml_pictures/ml053.png" height="50%" width="70%">
</center>

### 4.8 Underfitting
* Pick a small $\lambda_C$ will cause overfitting

<center>
<img class="center large" src=".//ml_pictures/ml054.png" height="50%" width="70%">
</center>

* Pick a huge $\lambda_C$ will cause underfitting

<center>
<img class="center large" src=".//ml_pictures/ml055.png" height="50%" width="70%">
</center>

* How to pick $\lambda_C$

<center>
<img class="center large" src=".//ml_pictures/ml056.png" height="50%" width="70%">
</center>

* Other Regularizers

<center>
<img class="center large" src=".//ml_pictures/ml057.png" height="50%" width="70%">
</center>

### 4.9 Understanding
* Constrain hypothesis sets to prevent them from being able to fit noise
* Learning algorithms are optimization problems and regularization imposes constraints on that optimization
* Constraints can be converted into augmented objectives

### 4.10 Validation

* Regularization Estimation

<center>
<img class="center large" src=".//ml_pictures/ml062.png" height="50%" width="70%">
</center>

* Validation Estimation

<center>
<img class="center large" src=".//ml_pictures/ml063.png" height="50%" width="70%">
</center>


* For test sets, we know that the HI will have a tight bound for it since we only have one hypothesis for $E_{test}$.

<center>
<img class="center large" src=".//ml_pictures/ml064.png" height="50%" width="70%">
</center>

* From the inequality above we can have that:

$$E_{out}(g)\leq{E_{test}(g)}+O(\frac{1}{\sqrt{k}}),\ \mathbf{with\ probability\ of\ }1-\delta$$

* For the $E_{test}$, we have following deduction:

<center>
<img class="center large" src=".//ml_pictures/ml065.png" height="50%" width="70%">
</center>

For the third line above, since $\mathbf{x}_i$ have the same distribution with $\mathbf{x}$, we have:

$$\mathbb{E}_{\mathbf{x}_i}[e(h(\mathbf{x}_i),y_i)]=\mathbb{E}_{\mathbf{x}}[e(h(\mathbf{x},y))]=E_{out}$$




## Chapter 5 Three Learning Principles

### 5.1 Occam 's Razor
> An explanation of the data should be made as simple as possible, but no simpler. ——Albert Einstein
>
> Entities must not be multiplied beyond necessity. ——William of Occam
>
> Occam's Razor for learning: The simplest model that fits the data is also the plausible.

<center>
<img class="center large" src=".//ml_pictures/ml079.png" height="50%" width="70%">
</center>




## Chapter 6 (L14): Decision Trees

### 6.1 Entropy
* How diverse the set of value is?
* Value: the lower a collection's entropy, the more pure it is

$$Entropy(S)=\sum_{v\in{V(S)}}-\frac{|S_v|}{S}{\log_2}(\frac{|S_v|}{S})$$


### 6.2 Information Gain

$$IG(x_i,y)= Entropy(y)-\sum_{v\in{V(x_i)}}(f_v)(Entropy(y_{x_i=v}))$$

* Where $x_i$ is a feature
    * $y$ is the collection of all labels
    * $V(x_i)$ is the set of unique values of $x_i$
    * $f_v$ is the fraction of inputs where $x_i=v$
    * $y_{x_i=v}$ is the collection of labels where $x_i=v$

### 6.3 The ID3 Algorithm

### 6.4 Decision Tree/ ID3 Pros and Cons
* Pros:
    * Intuitive and explainable
    * Can handle categorical and real-valued features
    * Automatically performs feature selection
    * The ID3 algorithm has a perference for shorter trees(Simpler hypotheses)

* Cons
    * The ID3 algorithm is a greedy(it selects the feature with highest information gain at every step), so no optimality guarantee.
    * Overfitting! (Achieve zero in sample error)

### 6.5 Addressing Overfitting
* Heuristics("regularization")
    * Do not split leaves past a fixed depth $\delta$
    * Do not split leaves with fewer than $c$ labels
    * Do not split leaves where the maximal information gain is less than $\tau$
    * Predict the most common label at each leaf

* Pruning("validation")
    * Evaluate each split using a validation set
    * Compare the validation error with and without that split(replacing it with most common label at that point)


## Chapter 7 (L15) Decision Tree and Bagging
### 7.1 Pruning example
> Input: a decision tree $t$, and a validation dataset, $\mathcal{D}_{val}$
> Compute the validation error of tree $t$, and get $E_{val}(t)$
> For each split $s\in{t}$
> * Compute $E_{val}(t\backslash{s})=$ the validation error of $t$ with $s$ replaced by a leaf using the most common label at $s$.
> * If exist a split $s\in{t}$, s.t. $E_{val}(t\backslash{s})\leq{E_{val}(t)}$, repeat the pruning process with $t\backslash{s^{*}}$, where $t\backslash{s^{*}}$ is the pruned tree with minimal validation error.
>
> Double check the pruned tree. If $E_{val}(t)=0$, this means that we cannot prune this tree any more.

### 7.2 Decision Tree/ ID3 Cons
* Algorithm is greedy
* Overfitting
    * Can be addressed via heuristics("regularization") or pruning("validation")
* High Variance
    * Bias will not change with 
    * More complicated model have higher variance, but with increasement of points in data set, the variance will decrease.

### 7.3 Bagging
* Short for Bootstrap aggregating
* Combine the prediction of many hypotheses to reduce variance
* If $n$ independent random variables $x_1, x_2,\cdots, x_n$ have variance $\sigma^2$, then the variance of $\frac{1}{n}\sum_{i=1}^{n}{x_i}$ is $\frac{\sigma^2}{n}$


### 7.4 Bootstrapping
* A statistical method for estimating properties of a distribution, given potentially a small number of samples from that distribution
* Rely on resampling the samples **with relacement** many, many times

    * Example: {1,2,3,4,5}
    * Without replacement {1,1,2,2,3}(Wrong)
    * With replacement {1,1,2,2,3}(Allowed)

* Bootstrapping Example:
    * Suppose you draw 8 samples from a distribution $\mathcal{D}$
    * Resample 8 values(with replacement) from $\mathcal{D}$ 1000 times
    * Meaning that you will get 1000 sets of 8 values

### 7.5 Aggregating
* Combine multiple hypotheses
    * Regression: average the predictions;
    * Classification: find the category that most hypotheses predict(plurality vote)

### 7.6 Bagging Decision Trees
> Input: $\mathcal{D}, B$
> For $b=1,2,\cdots,B$
> * Create a dataset, $\mathcal{D}_{b}$, by sampling $n$ points from $\mathcal{D}$ with replacement
> * Learn a decision tree, $t_b$, using $D_b$ and the ID3 algorithm
> Output: $\bar{t}$, the aggregated hypothesis
>
> But the problem is that predictions made by trees trained on similar datasets are highly correlated

### 7.7 Split-Feature Randomization
* To decorrelate these predictions, randomly limit features avaliable at each iteration of ID3 algorithm.
* Select $m<d$ features every time

### 7.8 Random forests
> Input: $\mathcal{D}, B, m$
> For $b=1,2,\cdots,B$
> * Create a dataset, $\mathcal{D}_{b}$, by sampling $n$ points from $\mathcal{D}$ with replacement
> * Learn a decision tree, $t_b$, using $D_b$ and the ID3 algorithm with split-feature randomization
> Output: $\bar{t}$, the aggregated hypothesis


### 7.10 Random Forests and Feature Selection
> Random forests allow for the computation of "variable importance", a way of ranking features based on how useful they are at predicting the output.
> * Initialize each feature's importance to zero
> * Each time a feature is chosen by the ID3 algorithm(with split-feature randomization), add that feature's information gain(relative to the split) to its importance.

## Chapter 8 (L16) Boosting
* Another Cons for Decision Tree is High Bias(Especially short trees, i.e. stumps) 

### 8.1 Decision Stumps
* Weak learner 
* Tend to use with boosting
* Assemble them to make up a much better learner(complex one)

### 8.2 AdaBoost

<center>
<img class="center large" src=".//ml_pictures/ml083.png" height="50%" width="70%">
</center>

* Setting $\alpha_t$
    * Intuitively, we want good hypotheses to have high weights.

* Normalizring $w_i$
    * Trying to use sum of each points' weights $\omega_i$ to normalize updated weights

<center>
<img class="center large" src=".//ml_pictures/ml084.png" height="50%" width="70%">
</center>

* Why AdaBoost?
    * Only have access to weak learner(Computational Restraints)
    * Want final hypothesis to be a weighted combination of weak learners
    * Greedily minimize exponential loss(upper bounds for binary error)

> Exponential Loss
> * $e^{-f({\mathbf{x}})h(\mathbf{x})}$
> * Used for binary classification, and the more $h(\mathbf{x})$ agrees with $f(\mathbf{x})$, the smaller the loss.
> * Also, we can claim that:
>
> $$e^{-f({\mathbf{x}})h(\mathbf{x})}\leq{[|f({\mathbf{x}})\neq{h(\mathbf{x})}|]}$$

### 8.3 Exponential Loss and Greedy Algorithm
> Final Exponentail Loss
>
> $$\frac{1}{n}\sum_{i=1}^{n}{ e^{-y({\mathbf{x}_i})H_{T}({\mathbf{x}_i}) }}= \prod_{t=1}^{T}{Z_{t}}$$
>
> Then, if we want to achieve the mimimal loss at the final loss, we want to make each $Z_t$ is minimal at each iteration with greedy algorithm.
>
> Then, we are going to prove that choosing $\alpha_t=\frac{1}{2}{ \log{ \frac{(1-{\epsilon}_t)}{\epsilon_t}}}$ will be good with regard to greedy algorithm.
>
> Therefore, the in-sample error will finally be very small, since($Z_t<1$):
>
> $$\prod_{t=1}^{T}{Z_t}=\prod_{t=1}^{T}{2\sqrt{\epsilon_t(1-\epsilon_t)}}\rightarrow0$$

### 8.4 Out-of-Sample Error
> Emprical Results indicate that increasing T does not lead to overfitting as this bound would suggest.
>
> Margins: can be interpreted as how confident $g_T$
is in its prediction: the bigger the margin, the more confident.
>
> Tips: 
> * $n$ increase, I think that the model will become more inconfident.


## Chapter 9 (L18) Nearest Neighbour

### 9.1 Similarity
* Euclidean Distance
* Cosine similarity
* Mahalanobis Distance

### 9.2 Nearest Neighbour
* Let $\mathbf{x}_{[1]}{\mathbf{x}}$ be $\mathbf{x}$'s nearest neighbour, i.e. the closest point to $\mathbf{x}$ in $\mathcal{D}$

* The nearest neighbour hypothesis
    * $g(\mathbf{x})=y_{[1]}(\mathbf{x})$
    * Require no training!
    * Always no training error!(Can always shatter points)

### 9.3 Generallization of Nearest Neighbour
> Claim: $E_{out}$ for the nearest neighbour hypothesis is not much worse than the best possible $E_{out}$
>
> Formally: under certain conditions, with high probability, $E_{out}(g)\leq{2{E}_{out}(g^{*})}$ as $n\rightarrow{\infty}$
>
> Proof:
> * Assume a binary classification problem: $\mathcal{Y}=\{-1,+1\}$
> * Assume labels are noisy:
>
> $$\pi(\mathbf{x})=P\{y=+1|\mathbf{x}\}$$
>
> * Assume $\pi(\mathbf{x})$ is continuous
> * As $n\rightarrow{\infty}$, $\mathbf{x}_{[1]}{\mathbf{x}}\rightarrow{\mathbf{x}}$
> * Therefore,
>
> $$
\begin{aligned}
E_{out}
& =\mathbb{E}_{\mathbf{x}}\big[[{g(\mathbf{x})\neq{y}}]\big]\\
& =P\{ g(\mathbf{x})=+1 \cap {y=-1}\} + P\{ g(\mathbf{x})=-1 \cap {y=+1}\} \\
& =\pi{(\mathbf{x}_{[1]}{\mathbf{x}})}(1-\pi{(\mathbf{x})}) + \big(1-\pi{(\mathbf{x}_{[1]}{\mathbf{x}})}\big)(\pi{(\mathbf{x})})\\
& = 2\pi(\mathbf{x})(1-\pi(\mathbf{x}))\\
& \leq{2min(\pi(\mathbf{x}),(1-\pi({\mathbf{x}})))}=2E_{out}(g^{*})
\end{aligned}
$$
>
> Self-Regularization: The nearest neighbour hypothesis can only be complex when there is more data.


### 9.4 k-Nearest Neighbour(kNN)
> Classify a point as the most common label among the labels of the $k$ nearest training points
>
> If we have a binary classification probelm and $k$ is odd:
>
> $$g(\mathbf{x})=sign(\sum_{i=1}^{k}{y_{[i]}(\mathbf{x})})$$
>
> Setting $k$

### 9.5 kNN Pros and Cons
> Pros
> * Intuitive/explainable
> * No training/retraining
> * Provably near-optimal in terms of $E_{out}$
>
> Cons:
> * Computationally expensive
>    * Always needs to store all data
>    * Computing $g(\mathbf{x})$ requires computing distances and sorting
 
### 9.6 Efficient $k$-Nearest Neighbours
> **Curse of Dimensionality**
> * With increment of dimensinality, the furthest point and the closest points grow closer.
> * What can we do?
>    * More data
>    * Fewer dimensions
>    * Blessing non-uniformity
>
> **Data Condensing**
> * Use fewer input data points but have same predictions out of training data set
> * be less rigid
> * Use fewer input data points but have same predictions in trainding data set


### 9.7 Condensed Nearest Neighbour(CNN)
<center>
<img class="center large" src=".//ml_pictures/ml085.png" height="50%" width="70%">
</center>

### 9.8 Organizing the inputs
* Just split the inputs into clusters, groups of points that are close to one another but far from other groups.

<center>
<img class="center large" src=".//ml_pictures/ml086.png" height="50%" width="70%">
</center>

 * The figure above shows us that if we have a point in set $i$, and the distance between $\mathbf{x}$ and it is less than $\mathbf{x}$ to set $j$'s boundary, then we do not need to search points in set $j$ any more.

 * Further more, we promote this therom to wider application

 <center>
<img class="center large" src=".//ml_pictures/ml087.png" height="50%" width="70%">
</center>

### 9.9 Clustering inputs
* Using **Triangle Inequality** in norm, we have

 <center>
<img class="center large" src=".//ml_pictures/ml088.png" height="50%" width="70%">
</center>

* Therefore, we want cluster centers to be far apart and cluster radii to be small

 <center>
<img class="center large" src=".//ml_pictures/ml089.png" height="50%" width="70%">
</center>

* Explanation about pitcture above:
    * 1st Step is about how to generate center points in each cluster;
    * 2nd Step is about how to assign every points in data set $\mathcal{D}$ to $C$ clusters
    * 3rd Step is about after assigned point to each cluster, we need to update its center point and the radius

### 9.10 Parametric vs. Non-parametric
> Parametric Model
> * Hypotheses have a parametrized form
> * Parameters learned from training data; can discard training data afterwards;
> * Cannot exactly model every target function
>
> Non Parametric Models
> * Hypotheses cannot be expressed using a finite number of parameters
>    * Example: kNN, decision trees
> * Training data generally need to be stored in order to make predictions
> * Can recover any target function given enough data

### 9.11 Radial Basis Functions(RBF)
> * kNN only consider some points and weights them equally
> * What if we considered all points but weighted them unequally?
> * Intution: all points are useful but some points are more useful than others!
> * Bouns: no need to choose $k$

Suppose we have a binary classification problem

 <center>
<img class="center large" src=".//ml_pictures/ml090.png" height="50%" width="70%">
</center>

> * If $r$ is really small, then $\frac{\|\mathbf{x}-\mathbf{x}_i\|}{r}$ will always be large (unless $\|\mathbf{x}-\mathbf{x}_i\|$ is small)
> * If $\frac{\|\mathbf{x}-\mathbf{x}_i\|}{r}$ is large, then $\phi(\frac{\|\mathbf{x}-\mathbf{x}_i\|}{r})$ will always be small(unless $\|\mathbf{x}-\mathbf{x}_i\|$ is small)
> * The smaller $r$ is, the closer $\mathbf{x}$ has to be to $\mathbf{x}_i$ in order for $\phi(\frac{\|\mathbf{x}-\mathbf{x}_i\|}{r})$ to be non-zero

 <center>
<img class="large" src=".//ml_pictures/ml091.png" height="50%" width="50%">
</center>

In a sense, $r$ is like $k$, if $r$ increases, we care more and more points.

Intutively, we want points close to $\mathbf{x}$ to have larger weights and points far from $\mathbf{x}$ to have small weights

 <center>
<img class="center medium" src=".//ml_pictures/ml092.png" height="50%" width="50%">
</center>

And finally, we have

 <center>
<img class="center medium" src=".//ml_pictures/ml093.png" height="50%" width="50%">
</center>

## Chapter 10 (L19-21) Support Vector Machine

### 10.1 Maximal Margin Linear Separators
> We want maximum the margin with restraint on correct classification.
>
> $$
\begin{aligned}
&\textbf{max}\ margin(\mathbf{w})\\
&\textbf{subject\ to\ } \mathbf{w}\ classify\ every\ (\mathbf{x}_i,y_i)\ correctly
\end{aligned}
$$
>
> We can use special scaling and make every linear separators become separating hyperplanes.

 <center>
<img class="center large" src=".//ml_pictures/ml094.png" height="50%" width="70%">
</center>

> After scaling our weight vector, every separating hyperplane have margin expression:
>
> $$\frac{1}{\|\mathbf{w}\|}$$

### 10.2 How to calculate the margin?
> First, we want to prove that weight vector $\mathbf{w}$ is orthogonal to the hyperplane $h(\mathbf{x})=\mathbf{w^{T}x}+w_0=0$
> 
> Second, we will use the knowledge of projection. Suppose $\mathbf{x}'$ be an arbitrary point on the hyperplane, and $\mathbf{x}''$ be an arbitrary point. The distance between $\mathbf{x}''$ to the hyperplane $h(\mathbf{x})=\mathbf{w^{T}x}+w_0=0$ will be
>
> $$d(x'', h)=|\frac{\mathbf{w^{T}(\mathbf{x''}-\mathbf{x'})}}{\|\mathbf{w}\|}|=|\frac{\mathbf{w^T{x''}}+w_0}{\|\mathbf{w}\|}|$$
>
> The margin of separating hyperplane is the distance between the hyperplane and the nearest training point

 <center>
<img class="center large" src=".//ml_pictures/ml095.png" height="50%" width="70%">
</center>

### 10.3 Why maximal margin?
> With minimum margin $\rho$, linear separators in $\mathcal{H}_{\rho}$ can not always shatter all sets of three points.

<center>
<img class="center large" src=".//ml_pictures/ml096.png" height="50%" width="70%">
</center>

### 10.4 Soft-Margin SVMs

<center>
<img class="center large" src=".//ml_pictures/ml097.png" height="50%" width="70%">
</center>

> $\xi_i$ is the soft error on the $i^{th}$ training

<center>
<img class="center large" src=".//ml_pictures/ml098.png" height="50%" width="70%">
</center>


## Chapter 11 (L22): Neural Networks
### 11.1 Combining Perceptrons

<center>
<img class="center large" src=".//ml_pictures/ml099.png" height="50%" width="80%">
</center>

### 11.2 Multi-Layer Perceptron(MLP)

<center>
<img class="center large" src=".//ml_pictures/ml100.png" height="50%" width="100%">
</center>

### 11.3 Architecture
> The architecture of an MLP is the vector $\vec{d}=[d^{(0)}, d^{(1)},\cdots, d^{(L)}]$

<center>
<img class="center large" src=".//ml_pictures/ml101.png" height="50%" width="100%">
</center>

### 11.4 Weights
> The weights between layer $l-1$ and layer $l$ are a matrix: $W^{(l)} \in {\mathbb{R}^{(d^{(l-1)}+1)\times{d^{(l)}}}}$

### 11.5 Signal and Outputs

<center>
<img class="center large" src=".//ml_pictures/ml102.png" height="50%" width="80%">
</center>

### 11.5 Forward Propagation for Predictions

<center>
<img class="center large" src=".//ml_pictures/ml103.png" height="50%" width="80%">
</center>

## Chapter 12 (L23): Backpropagation
### 12.1 Computing Gradients

<center>
<img class="center large" src=".//ml_pictures/ml104.png" height="50%" width="80%">
</center>

### 12.2 Computing Partial Derivatives With Chain Rule

<center>
<img class="center large" src=".//ml_pictures/ml105.png" height="50%" width="80%">
</center>

<center>
<img class="center large" src=".//ml_pictures/ml106.png" height="50%" width="80%">
</center>

### 12.3 Back Propagation

<center>
<img class="center large" src=".//ml_pictures/ml107.png" height="50%" width="90%">
</center>

### 12.4 Computing Gradients with Feed Forward and Back Propagation

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