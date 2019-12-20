---
layout: notes
section-type: notes
title: Matrix Tricks
category: math
---

* TOC
{:toc}
---

## Basics Review about Linear Algebra

### Determinat of a Matrix

* Determinat: must be square

$$
det\left[
 \begin{matrix}
   a_{11} & a_{12}\\
   a_{21} & a_{22}
  \end{matrix}
  \right]
=
\left|
 \begin{matrix}
   a_{11} & a_{12}\\
   a_{21} & a_{22}\\
  \end{matrix}
\right|
=
a_{11}a_{22}-a_{21}a_{12}
$$

&NewLine;

$$
det\left[
 \begin{matrix}
   a_{11} & a_{12} & a_{13}\\
   a_{21} & a_{22} & a_{23}\\
   a_{31} & a_{32} & a_{33}
  \end{matrix}
  \right]
=
a_{11}
\left|
 \begin{matrix}
   a_{11} & a_{12}\\
   a_{21} & a_{22}\\
  \end{matrix}
\right|
-
a_{12}
\left|
 \begin{matrix}
   a_{21} & a_{23}\\
   a_{31} & a_{33}\\
  \end{matrix}
\right|
+
a_{13}
\left|
 \begin{matrix}
   a_{21} & a_{22}\\
   a_{31} & a_{32}\\
  \end{matrix}
\right|
$$



### Matrix Sum

* $A$ and $B$ must have the same dimensions
* $A_{m\times{n}} + B_{m\times{n}} = C_{m\times{n}}$
* In specific, $c_{ij}=a_{ij}+b_{ij}$


### Matrix Product

* $C_{n\times{p}}=A_{n\times{m}}B_{m\times{p}}$
* In specific, $c_{ij}=\sum^{m}_{k=1}{a_{ik}b_{kj}}$

### Transpose of a Matrix

* Matrix $A$ is an $m\times{n}$ element array

$$
A_{m\times{n}}=\left[
 \begin{matrix}
   a_{11} & a_{12} &\cdots & a_{1n} \\
   a_{21}\\
   .\\
   .\\
   .\\
   a_{m1} &\cdots &\cdots & a_{mn}
  \end{matrix}
  \right]
$$

* **transpose** of matrix $A$(written $A^{T}$) is $a_{ji}$($A_{m\times{n}}$ with rows and columns flipped)

* Some arithmetic rules for this:
  * $(A+B)^{T}=A^T+B^T$
  * $(AB)^T = B^{T}A^{T}$ 
  * If $A^T = A$, we say A is **symmertric**.

### Inverse of a Matrix

* If A is a square matrix, the **inverse** of $A$, called $A^{-1}$, satisfies

$$AA^{-1}=I$$
$$ A^{-1}A=I$$

Where $I$, the **indentity matrix**, is a diagonal matrix with all $1$' s on the diagonal, like the following matrix:

$$
\left[
 \begin{matrix}
   1 & 0\\
   0 & 1\\
  \end{matrix}
\right]
$$

* Inverse of a 2D Matrix

For a 2D matrix, if

$$A=
\left[
 \begin{matrix}
   a & b\\
   c & d\\
  \end{matrix}
\right]
$$

then

$$A^{-1}=\frac{\left[
 \begin{matrix}
   d & -b\\
   -c & a\\
  \end{matrix}
\right]}
{|A|}
$$

* Inverse of Matrix


### Linear Dependant
These [**video1**](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/linear-independence/v/linear-algebra-introduction-to-linear-independence), [**video2**](https://www.youtube.com/watch?v=yLi8RxqfowA) may explain this clearly.

* A set of vectors is **linear dependant** if one of the vectors can be expressed as a linear combination of the other vectors.

Example:

$$
\left[
\begin{matrix}
  1\\
  0\\
  0
\end{matrix}
\right]
,
\left[
\begin{matrix}
  0\\
  1\\
  0
\end{matrix}
\right]
,
\left[
\begin{matrix}
  2\\
  1\\
  0
\end{matrix}
\right]
$$


### Other Terms

* Trace of a matrix is $Tr(A)=\sum^{N}_{i=1}a_{ii}$(the sum of the diagonal entries)

* Matrix $A$ is orthonormal if

$$A^{T} = A^{-1}$$

and in this case

$$AA^{T} = I$$

* Matrix transformation

rotation matrix is given by

$$
A=
\left[
 \begin{matrix}
   cos(\theta) & -sin(\theta)\\
   sin(\theta) & cos(\theta)\\
  \end{matrix}
\right]
$$

So to rotate vector

$$
\left(
  \begin{matrix}
    1\\
    0
  \end{matrix}
\right)
$$

by 30 deg we multiply

$$
\left[
  \begin{matrix}
    0.8660 & -0.5\\
    0.5 & .08660
  \end{matrix}
\right]
\left(
  \begin{matrix}
    1\\
    0
  \end{matrix}
\right)
$$

* Matrix Transformation: Scale

* Eigenvalues and Eigenvector

If Matrix $A$ is a $n$ dimension square matrix, and have a number $\lambda$ and non-zero vector $X=(x_1, x_2,\cdots, x_n)^{T}$, and 

$$AX = \lambda{X} \  or (\lambda{I}-A)X=0$$

we will name $\lambda$ as **eigenvalue**, and name $X$ as **eigenvecotr**  for Matrix $A$.

Therefore, the formula $(\lambda{I}-A)X=0$ can be written as following linear equations:

$$
\begin{cases}
(\lambda-a_{11})x_1-a_{12}x_2-\cdots-a_{1n}x_{n}=0 \\
-a_{21}x_1+(\lambda-a_{22})x_{2}-\cdots-a_{2n}x_{n}=0\\
.\\
.\\
.\\
-a_{n1}x_1-a_{n2}x_2-\cdots+(\lambda-a_{nn})x_{n}=0
\end{cases}
$$

* Eigenvalue and Eigenvector Solving Process  
(1)Calculate Characteristic Polynomical $|A-\lambda{E}|$  
(2)Calculate all the solutions for $|A-\lambda{E}|$  
(3)For every eigenvalue $\lambda_0$, calculate the basic solution $\xi_1,\cdots,\xi_{t}$ for linear homogeneous equation $(A-\lambda_0{E})x = 0$  





