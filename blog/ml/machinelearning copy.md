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
### Mathematical Notation
> * unknown target function$f:\mathcal{X}\rightarrow\mathcal{Y}$
> * training data $\mathcal{D}$
> * hypothesis set $\mathcal{H}$
> * learning algorithm $\mathcal{A}$
> * learned hypothesis $\mathcal{H}$, and $\mathcal{H}\ni g\approx{f}$
>
> $\mathcal{H,A}$ will be called as learning model, this is what we can control.

### Perceptron
Input $\mathcal{X}\in\mathbb{R}^n$ ($\mathbb{R}^{n}$ is the $n$-dimensional Euclidean space), Output $\mathcal{Y}\in \{+1,-1\}$. Give a sign function

$$
h(\mathbf{x})=
\begin{cases}
    +1\ \ if\sum_{i=1}^{2}w_{i}x_{i}-b>0 \\
    -1\ \ otherwise
\end{cases}
$$

which can also be expressed in this way:
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

### Perceptron Learning Algorithm(PLA)

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