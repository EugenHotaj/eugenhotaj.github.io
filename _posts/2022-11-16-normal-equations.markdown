---
layout: post
title:  "Deriving the Normal Equations"
date:   2022-11-16
tag: technical
---

Suppose we are given a design matrix $$\mathbf{X} \in \mathbb{R}^{N \times K}$$ 
and targets vector $$\mathbf{y} \in \mathbb{R}^N$$. We want to find
parameter vector $$\mathbf{w} \in \mathbb{R}^K$$ which minimizes the 
residual sum of squares, i.e. 

$$
\begin{align}
\mathop{\arg \min}\limits_\mathbf{w} \ \mathrm{RSS}(\mathbf{w}) &= \sum_i^N (y_i - \mathbf{x}_i^T \mathbf{w})^2 \\
&= (\mathbf{y} - \mathbf{Xw})^T(\mathbf{y} - \mathbf{Xw})
\end{align}
$$

The solution to the (least squares) problem can be obtained using the normal equations. 
We can derive the normal equations from first principles as follows. First, let's expand 
the $$\mathrm{RSS}$$ definition so it's easier to work with.

$$
\begin{align}
\mathrm{RSS}(\mathbf{w}) &= (\mathbf{y} - \mathbf{Xw})^T(\mathbf{y} - \mathbf{Xw}) \\

&= (\mathbf{y}^T - \mathbf{w}^T\mathbf{X}^T)(\mathbf{y} - \mathbf{Xw})
&& \text{definition of transpose} \\

&= \mathbf{y}^T\mathbf{y} - \mathbf{y}^T\mathbf{Xw} - \mathbf{w}^T\mathbf{X}^T\mathbf{y} 
+ \mathbf{w}^T\mathbf{X}^T\mathbf{Xw} \\

&= \mathbf{y}^T\mathbf{y} - 2\mathbf{y}^T\mathbf{Xw} + \mathbf{w}^T\mathbf{X}^T\mathbf{Xw} \\
\end{align}
$$

The last step follows because $$\mathbf{w}^T\mathbf{X}^T\mathbf{y}$$ is a scalar 
and so it is equal to its transpose $$\mathbf{y}^T\mathbf{Xw}$$.


Now, to minimize $$\mathrm{RSS}(\mathbf{w})$$, we take
its derivative w.r.t. $$\mathbf{w}$$, set it to $$0$$, and solve for $$\mathbf{w}$$.

$$
\begin{align}
\nabla_\mathbf{w} \mathrm{RSS}(\mathbf{w}) &= 0 \\

\nabla_\mathbf{w} (
\mathbf{y}^T\mathbf{y} - 2\mathbf{y}^T\mathbf{Xw} + \mathbf{w}^T\mathbf{X}^T\mathbf{Xw} 
) &= 0 \\

0 - 2 \mathbf{X}^T\mathbf{y} + 2 \mathbf{X}^T\mathbf{X}\mathbf{w} &=0 \\

\mathbf{X}^T\mathbf{X}\mathbf{w} &= \mathbf{X}^T\mathbf{y} \\

\mathbf{w} &= (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}

\end{align}
$$

What we have arrived at is exactly the normal equations, where 
$$(\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T$$ is known as the (Moore-Penrose) pseudo-
inverse.
