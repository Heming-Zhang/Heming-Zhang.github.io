---
layout: notes
section-type: notes
title: Machine Learning
category: ml
---

* TOC
{:toc}
---

Similar Courses
* [Washu CSE 417T: Intro to Machine Learning](https://classes.cec.wustl.edu/~SEAS-SVC-CSE417T/)
* [NTU Machine Learning Foundation](https://www.csie.ntu.edu.tw/~htlin/course/ml13fall/)

Recommended Books

* [Matrix Cookbook](http://www.math.uwaterloo.ca/~hwolkowi/matrixcookbook.pdf)
* [Learning From Data (Color)](https://heming-zhang.github.io/course/Learning_From_Data(Color).pdf)
* [Learning From Data (2012)](https://heming-zhang.github.io/course/Learning_From_Data(2012)-Abu-Mostafa.pdf)
* [Computer Age Statistical Inference](https://heming-zhang.github.io/course/[Bradley_Efron,_Trevor_Hastie]_Computer_Age_Statis(z-lib.org).pdf)

## 1. Learning Problem
### 1.1 Mathematical Notation
> * unknown target function$f:\mathcal{X}\rightarrow\mathcal{Y}$
> * training data $\mathcal{D}$
> * hypothesis set $\mathcal{H}$
> * learning algorithm $\mathcal{A}$
> * learned hypothesis $\mathcal{H}$, and $\mathcal{H}\ni g\approx{f}$
>
> $\mathcal{H,A}$ will be called as learning model, this is what we can control.

### 1.2 Perceptron
> Input $\mathcal{X}\in\mathbb{R}^n$ ($\mathbb{R}^{n}$ is the $n$-dimensional Euclidean space). Output $\mathcal{Y}\in \{+1,-1\}$. Give a sign function
>
> $$
h(\mathbf{x})=
\begin{cases}
    +1\ \ if\sum_{i=1}^{2}w_{i}x_{i}-b>0 \\
    -1\ \ otherwise
\end{cases}
$$
>
> which can also be expressed in this way:
>
> $$
h(\mathbf{x})=sign((\sum_{i=1}^{n}w_{i}x_{i})+b)
$$
>
> To simplify the noation of the perceptron formula, we will treat the bias $b$ as a weight $w_0=b$ and merge it with the other weights into one vector $\mathbf{w}=[w_0,w_1,\cdots,w_n]^{T}$,where $^{T}$ denotes the transpose of a vector, so $\mathbf{w}$ is a column vector. We also treat $\mathbf{x}$ as a column vector and modify it to become $\mathbf{x}=[x_0,x_1,\cdots,x_n]^T(where\ x_0=1)$, therefore $\mathbf{x}=(x_1, x_2,\cdots,x_n)\in\mathbb{R}^{n}$

With such convention, we will have 

$$\mathbf{w}^{T}\mathbf{x}=\sum_{i=0}^{d}w_ix_i$$

Tips: 

 $$
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


> **Finally, we will get** 
>
> $$h(\mathbf{x})=sign(\mathbf{w}^T\mathbf{x})$$

<span id = "jump3"></span>

### 1.3 Perceptron Learning Algorithm(PLA)

We will use iterative method to find $\mathbf{w}$. At iteration $t$, where $t=0,1,2,\cdots$, there is a current value of the weight vector, call it $\mathbf{w}(t)$. Then the algorithm will pick one of misclassified examples, called $(\mathbf{x}(t),y(t))$, and uses it to update $\mathbf{w}(t)$. And the update rule is

$$\mathbf{w}(t+1)=\mathbf{w}(t)+y(t)\mathbf{x}(t)$$

Tip1: $y(t)$ and $\mathbf{x}(t)$ are actully $y_{n(t)}$, $\mathbf{x}_{n(t)}$ in short.

Tip2: $y(t)$ and $\mathbf{x}(t)$ is a point from training data set $\mathcal{D}=\{(\mathbf{x_1}, y_1), (\mathbf{x_2}, y_2),\cdots,(\mathbf{x_i}, y_i),\cdots,(\mathbf{x_n}, y_n)\}$
>
> Intution: suppose $(\mathbf{x},y)\in\mathcal{D}$ is a misclassified training example and $y=+1$
> * $\mathbf{w}^T\mathbf{x}$ is negative
> * After updating $\mathbf{w}'=\mathbf{w}+y\mathbf{x}$
> * $\mathbf{w}'^T\mathbf{x}=(\mathbf{w}+y\mathbf{x})^T\mathbf{x}=\mathbf{w}^T\mathbf{x}+y\mathbf{x}^T\mathbf{x}$ is less negative that $\mathbf{w}^T\mathbf{x}$
> * This will make $\mathbf{w}^T\mathbf{x}$ closer to 0.

* [PLA extension reading](https://www.csie.ntu.edu.tw/~htlin/course/ml13fall/doc/02_handout.pdf)


## 2. Linear Model
As pictures shown below, we have some circumstances that cannot be separated in linear way.
<center>
<img src=".//ml_pictures/ml020.png" height="25%" width="25%">
</center>


### 2.1 Linear Regression
> **Linear Models**:
>
> $$h(\mathbf{x})= \mathbf{some\ function\ of\ w^{T}x}$$
>
> $$
\mathbf{x}=
\left[
\begin{matrix}
1\\
x_1\\
.\\
.\\
x_d
\end{matrix}
\right]
$$
>
> where $\mathcal{X}=\mathbb{R}^d$ and y=$\mathbb{R}$. For linear models, we use squared error
>
>$$
\begin{aligned}
E_{in}(h)&={\frac{1}{n}\sum_{i=1}^{n}(h(\mathbf{x}_i)-y_i)^2 }\\
&={\frac{1}{n}\sum_{i=1}^{n}(h(\mathbf{x}_i)-y_i)^2 }\\
&=\frac{1}{n}||\mathbf{Xw-y}||^2 \\
&= \frac{1}{n}(\mathbf{Xw-y})^T(\mathbf{Xw-y})
\end{aligned}
$$

**To Minimize the Error**: We will find the gradient, and set it equal to zero. By solving the equation, we will need to check that the solution is a minimum. Following are concrete procedure:

$$
\begin{aligned}
E_{in}(\mathbf{w})&= \frac{1}{n}(\mathbf{Xw-y})^T(\mathbf{Xw-y})\\
&=\frac{1}{n}((\mathbf{Xw})^T-\mathbf{y}^T)(\mathbf{Xw-y})\\
&=\frac{1}{n}(\mathbf{w^T{X^T}Xw-2w^TX^Ty+y^Ty            })
\end{aligned}
$$

Therefore, the gradient will be

$$\nabla_{\mathbf{w}}E_{in}(\mathbf{w})=\frac{1}{n}(2\mathbf{X^TXw}-2\mathbf{X^Ty})$$

The Optimized $\mathbf{w^{*}}$

$$\nabla_{\mathbf{w}}E_{in}(\mathbf{w^{*}})=\frac{1}{n}(2\mathbf{X^TXw^{*}}-2\mathbf{X^Ty})=0$$

The formula above equals to 0

$$
\begin{aligned}
2\mathbf{X^TXw^{*}}-2\mathbf{X^Ty}&=0\\
\mathbf{X^TXw^{*}}&=\mathbf{X^Ty}\\
\mathbf{w^{*}}&=\mathbf{(X^TX)^{-1}X^Ty}
\end{aligned}
$$

Another thing we need do is to check the second derivative of $\mathbf{w}$

$$H_{\mathbf{w}}E_{in}(\mathbf{w})=\frac{1}{n}(2\mathbf{X^TX})$$

Here, $H_{\mathbf{w}}E_{in}(\mathbf{w})$ is semidefinite.

### 2.2 Logistic Regression

> We will use new sigmoid function, $h(\mathbf{x})=\theta(\mathbf{w^Tx})$, $\theta$ is a function which show the probability with range [0,1].
<center>
<img class = "large" src=".//ml_pictures/ml023.png" height="60%" width="70%">
</center>

> Observation are still **binary**: $y_i=\pm1$. And our goal is to learn $f(\mathbf{x})=P(y=+1\|\mathbf{x})$ (This means that we need to give a probability of $\mathbf{x}$ being $+1$). Therefore, we can rewrite the target goal $f(\mathbf{x})=P(y=+1\|\mathbf{x})$ as
>
> $$
P(y|\mathbf{x})=   
\begin{cases}
f(\mathbf{x}), & for\ y=+1\\
1-f(\mathbf{x}), & for\ y=-1
\end{cases}
$$

With settling the model function, we need to find a good hypothesis to measure the error. Some hypothesis is good if the probability of the training data $\mathcal{D}$ given by $h$ is high(which measures how our function give probability to). Therefore, we use **Cross Entropy** function:

$$E_{in}(\mathbf{w})=\frac{1}{n}{\sum_{i=1}^{n}\ln{(1+e^{-y_i\mathbf{w^Tx_i}})}}$$

Following figures will use **Probability Union** to explain how cross entropy function is got from mathematical induction:


<center>
<img class = "large" src=".//ml_pictures/ml024.png" height="60%" width="70%">
</center>

With maximization of above probability union

<center>
<img class="large"  src=".//ml_pictures/ml025.png" height="60%" width="70%">
</center>

To minimize above probability function, we introduce **Gradient Descent** approach. First, we shuold know that cross_entropy is a convex function. After getting the Hessian Matrix with positive semidefinite, we know that Cross-Entropy function is convex.

<center>
<img class="large"  src=".//ml_pictures/ml061.png" height="60%" width="70%">
</center>

Then we introduce the **Gradient Descent Intution** to do such thing. 
> Suppose current location $\mathbf{w}(t)$ and we get a small step of size $\eta$ in the direction of a unit vector $\hat{v}$. Then we want to move some distance $\eta$ in the "most downhill" direction possible $\hat{v}$
>
> $$\mathbf{w}(t+1)=\mathbf{w}(t)+\eta\hat{v}$$
>
> After that, we want to fix $\eta$ and choose $\hat{\mathbf{v}}$ to maximize the decrease in $E_{in}$ after making the update $\mathbf{w}(t+1)=\mathbf{w}(t)+\eta\hat{v}$. Therefore, we can get
> $$\Delta{E_{in}}(\hat{v})=E_{in}(\mathbf{w}(t)+\eta\hat{v})-E_{in}(\mathbf{w}(t))$$
> What we want to do here is to maximum the decreation here to Minimum the $E$ function.
>
> $$
\begin{aligned}
\Delta{E_{in}}(\hat{v})&=E_{in}(\mathbf{w}(t)+\eta\hat{v})-E_{in}(\mathbf{w}(t))\\
&{\approx}  (E_{in}(\mathbf{w}(t))+\eta\hat{v}^{\mathbf{T}}\nabla_{\mathbf{w}}{E_{in}(\mathbf{w}(t)))}-E_{in}(\mathbf{w}(t)) \\
&{\approx}\eta\hat{v}^{\mathbf{T}}\nabla_{\mathbf{w}}{E_{in}(\mathbf{w}(t))}\\
&\geq{-\eta||\nabla_{\mathbf{w}}{E_{in}(\mathbf{w}(t))||}} 
\end{aligned}
$$

The explanation for the last line here is

$$\mathbf{a}\cdot\mathbf{b}=-|\mathbf{a}|\cdot|\mathbf{b}|$$

And the explanation for second line here(Gradient):
* Knowing that $\mathbf{x,\ w}\in{\mathbb{R}^{d+1}}$, and means that $\mathbf{x,\ w}$ has d+1 dimensions.
* Thus, 

$$\nabla{E}_{in}(\mathbf{w})=(\frac{\partial{E_{in}(\mathbf{w})}}{\partial{w}_0},\cdots,\frac{\partial{E_{in}(\mathbf{w})}}{\partial{w}_d})^{\mathbf{T}}$$

* And $\mathbf{v}$ is a vector with same dimensions as $\mathbf{w}$
* **First Order Taylor Expansion**: 

$$\nabla{E}_{in}(\mathbf{w+v})={E}_{in}(\mathbf{w})+\nabla{E}_{in}(\mathbf{w})^{\mathbf{T}}{\mathbf{v}}+o(\|\mathbf{h}\|)$$

* Thus, the optimial direction should be

$$\hat{v^{*}_{t}}=-\frac{\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))}{||\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))||}$$

* Intution for Step
<center>
<img  src=".//ml_pictures/ml026.png" height="50%" width="100%">
</center>

> A simple heuristic can do this. The gradient close to minimum is small and away from minimum can be large. Thus, we can set
> 
> $$\eta_{t}=\eta_{0}||\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))||$$
>
> Finally, we get
>
> $$
\begin{aligned}
\mathbf{w}(t+1)&=\mathbf{w}(t)+\eta_t\hat{v^{*}_{t}}\\
&=\mathbf{w}(t)+(\eta_{0}||\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))||)(-\frac{\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))}{||\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))||})\\
&= \mathbf{w}(t)-\eta_0\nabla_{\mathbf{w}}E_{in}(\mathbf{w}(t))
\end{aligned}
$$

* Gradient Descent Algorithm

<center>
<img class="center large" src=".//ml_pictures/ml027.png" height="50%" width="70%">
</center>

* SGD(Stochastic Gradient Descent)

<center>
<img class="center large" src=".//ml_pictures/ml028.png" height="50%" width="70%">
</center>

## 3. Overfitting

With High-Dimensional Input Space, sometimes it will cause low in-sample error and bad generalization, which can be demonstrated in following figure:

<center>
<img class="center medium" src=".//ml_pictures/ml034.png" height="50%" width="50%">
</center>


Also **Error and Model Complexity**'s relationship can be demonstrated in following ways:
<center>
<img class="large" src=".//ml_pictures/ml035.png" height="50%" width="50%">
</center>

To understand the overfitting, we need to know the cause for Overfitting:
* Too complexity: High kth-Order=>High VC-dimension: drive too fast
* Noise: bumpy road
* Too limited data: not familiar with road conditions

<center>
<img class="center medium" src=".//ml_pictures/ml038.png" height="50%" width="50%">
</center>

The figure above shows that in the right of green line area, which means we have limited data samples. The complex model($\mathcal{H_{10}}$) have larger $E_{out}$ than simple model ($\mathcal{H_{2}}$).

Before getting more data, the simple model will have better effect. Following first figure is the comparison between lower order and higher order polynomial.

* Less Data with 20 Points

<center>
<img class="center large" src=".//ml_pictures/ml039.png" height="50%" width="70%">
</center>

* More Data with 100 Points

<center>
<img class="center large" src=".//ml_pictures/ml040.png" height="50%" width="70%">
</center>

After increasing number of data, the complex model($\mathcal{H_{10}}$) wins. And to solve overfitting problems, we may want to (1)start from simple model;(2)data cleaning / pruning; (3)data hinting; (4)regularization; (5)validation. 

## 4. Validation
### 4.1 Model Selection (Not Single Hypothesis Anymore)

<center>
<img class="center large" src=".//ml_pictures/ml068.png" height="50%" width="70%">
</center>

<center>
<img class="center medium" src=".//ml_pictures/ml077.png" height="50%" width="50%">
</center>

> Tips: At here, $\mathcal{H}_{val}$ are formed up from many signle hypothesis from multiple hypothesis sets, and we are going to pick a best hypothesis set.

<center>
<img class="center large" src=".//ml_pictures/ml069.png" height="50%" width="70%">
</center>

### 4.2 Leave-one-out cross validation(LOOCV)

Cross here means that this data point can be training data and validation data. And $E_{cv}$ is almost an unbiased estimator of $E_{out}(g)$.

<center>
<img class="center large" src=".//ml_pictures/ml073.png" height="50%" width="70%">
</center>

Making an concrete example for calculating LOOCV Error:

<center>
<img class="center large" src=".//ml_pictures/ml074.png" height="50%" width="70%">
</center>

Model selection
  * For each hypothesis set, we need to run $n$ points to get its error.
  * Then, just like the validation data set above, we can just pick a best hypothesis $g^{-}_{m^{*}}$ which comes from hypothesis set $\mathcal{H}_{m^{*}}$

### 4.3 K-fold cross validation

<center>
<img class="center large" src=".//ml_pictures/ml076.png" height="50%" width="70%">
</center>
