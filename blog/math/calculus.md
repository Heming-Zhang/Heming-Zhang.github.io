---
layout: notes
section-type: notes
title: Calculus
category: math
---

* TOC
{:toc}
---
## Related Materials
* [The Calculus Lifesaver - All the tools you need to excel at calculus](https://heming-zhang.github.io/course/Princeton_Calculus.pdf)

## Part 1 Introduction to Limits
### 1.1 Limits: The Basic Use
Let function $f$ have domain $\mathbb{R}\setminus\{2\}$, and set $f(x)=x-1$ on this domain. Formally, you might write:

$$f(x) = x-1\ \ \text{when}\ x\neq{2}$$

And here is a question: what is $f(2)$? If you think about it, you can see that $x$ is really colse to 2, the value of $f(x)$ is really close to 1.

Anyway, let us just write

$$\lim_{x\rightarrow{2}}{f(x)=1}$$

Or another wat of writing the above statement is

$$f(x)\rightarrow{1}\ \ \text{as}\ x\rightarrow{2}$$

If you read this out loud, it should sound like "the limit, as $x$ goes to 2, of $f(x)$ is equal to 1."

<center>
<img class = "medium" src="./calculus_pictures/calculus_001.png" height="55%" width="55%">
</center>

### 1.2 Limits: Definition
> Let $f$ be a function defined on some open interval that contains the number $x_0$, except possibly at $x_0$ itself. We say the limit of $f(x)$ as $x$ approaches $x_0$ is $L$, and we write
>
> $$\lim_{x\rightarrow{x_0}}{f(x)=L}$$
>
> if for every $\epsilon>0$ (no matter how small $\epsilon$ is), there exists $\delta>0$ such that for all $x$
>
>$$0<|x-x_0|<\delta\ \ \Rightarrow\   |f(x)-L|<\epsilon$$
<br>
<center>
<img class = "medium" src="./calculus_pictures/calculus_005.png" height="55%" width="55%">
</center>

### 1.3 Left-Hand[or Right-Hand] Limit: Definition
> Let $f$ be a function defined on some open interval $(b,x_0)\ [\text{or\ }(x_0,b)]$. We say the left-hand [or right-hand] limit of $f(x)$ as $x$ approaches $x_0$ is $L$, and we write
>
> $$\lim_{x\rightarrow{x_0^{-}}}{f(x)=L}\ \ \Big[\lim_{x\rightarrow{x_0^{+}}}{f(x)=L}\Big]$$
>
> if for every $\epsilon>0$, there exists $\delta>0$ such that
>
> $$|f(x)-L|<{\epsilon}$$
>
> whenever
>
> $$x_0-\delta<x<x_0\ \ [x_0<x<x_0+\delta]$$


### 1.4 When the Limit Does Not Exist?
> * **Infinite Limit**: If left-hand limit or right-hand limit DNE(Does Not Exist), like
>
> $$\lim_{x\rightarrow{0^{+}}}{f(x)}=\lim_{x\rightarrow{0^{+}}}{\frac{1}{x}}=+\infty $$
>
>* **Right $\neq$ Left**: If left-hand limit does not equal to right-hand limit.

* There are some interesting examples for first circumstances
    * $f(x)=\frac{1}{x}$
    * $f(x)=\frac{1}{x^2}$
    * $f(x)=\sin(\frac{1}{x})$
<center>
<img class = "medium" src="./calculus_pictures/calculus_002.png" height="55%" width="55%">
</center>
<center>
<img class = "medium" src="./calculus_pictures/calculus_003.png" height="55%" width="55%">
</center>
<center>
<img class = "medium" src="./calculus_pictures/calculus_004.png" height="55%" width="55%">
</center>

The above third graph is a real mess near $x=0$. It oscillates infinitely often between 1 and -1, faster and faster as you move from the right toward $x = 0$.

### 1.5 The Limit at $+\infty$ and $-\infty$
> Let $f$ be a function defined on some open interval of $(a, +\infty)\ [(-\infty, a)]$. We say the limit of $f(x)$ as $x$ approaches {negative} infinity is $L$, and we write
>
> $$\lim_{x\rightarrow{[-]\infty}}{f(x)}=L$$
>
> if for every $\epsilon>0$, there exists $N$ such that
>
> $$|f(x)-L|<\epsilon$$
>
> whenever
>
> $$x>N\ \ [x<N]$$

For example, the function $\lim_{x\rightarrow{+\infty}}{f(x)}=\lim_{x\rightarrow{+\infty}}\sin{(\frac{1}{x})}=0$
<center>
<img class = "medium" src="./calculus_pictures/calculus_006.png" height="55%" width="55%">
</center>
