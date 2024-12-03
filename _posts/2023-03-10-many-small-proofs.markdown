---
layout: post
title:  Many Small Proofs and Derivations
date:   2023-03-10
tag: technical
---

*Last updated: Dec 2, 2024*

When reading textbooks, papers, or work stuff, I occasionally find myself writing small 
proofs or derivations to better understand a particular topic. Eventually I'll forget 
these derivations and have to look them up or re-derive them again.

This post is an attempt to gather such derivations in a central place for future use.
I plan to occasionally update this post as new material comes up.

<br><br>


### 1. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Evidence Lower Bound (ELBO)

Suppose we have a joint distribution $$p(\mathbf{x}, \mathbf{z})$$ where $$\mathbf{z}$$
are latent variables. Then the Evidence Lower Bound (ELBO) for $$p(\mathbf{x})$$ can be 
derived as:

$$
\begin{align}

\log p(\mathbf{x}) &= \log \int p(\mathbf{z}, \mathbf{x}) d\mathbf{z} && 
\text{definition of marginalization} \\

&= \log \int q(\mathbf{z}|\mathbf{x}) \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} d\mathbf{z}
&& \text{identity trick} \ q(\mathbf{z}|\mathbf{x})/q(\mathbf{z}|\mathbf{x})  = 1 \\

&= \log \mathbb{E}_{q(\mathbf{z}| \mathbf{x})} \left[ \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} \right] 
&& \text{definition of expectation} \\

&\ge \mathbb{E}_{q(\mathbf{z}| \mathbf{x})} \left[ \log \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} \right] 
&& \text{Jensen's inequality} \\

&= \mathcal{L}

\end{align}
$$

<br>


### 2. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Normal Equations

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

<br>

### 3. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Kullback-Leibler Divergence (Two Proofs)

We show two different ways to prove that $$D_\mathrm{KL}(p || q) \ge 0$$ given 
distributions $$p(x), q(x)$$.

#### Jensen's Inequality

The first proof makes use of [Jensen's inequality](https://en.wikipedia.org/wiki/Jensen%27s_inequality)
and the fact that $$-\log(x)$$ is a convex function. Jensen's inequality states that
$$\mathbb{E}[f(x)] \ge f(\mathbb{E}[x])$$ for any convex function $$f(x)$$. We can 
use this to show:

$$
\begin{align}
D_\mathrm{KL}(p||q) &= \mathbb{E}_{p(x)} \left[ -\log \left( \frac{q(x)}{p(x)} \right) \right] \\
&\ge -\log \left( \mathbb{E}_{p(x)} \left[\frac{q(x)}{p(x)} \right] \right)
&& \text{Jensen's inequality} \\
&= -\log \left( \int p(x) \frac{q(x)}{p(x)} dx \right) 
&& \text{definition of expectation} \\
&= -\log \left( \int q(x)dx \right) \\
&= -\log(1) \\
&= 0
\end{align}
$$

#### Natural Logarithm Bounds

The second proof makes use of the [natural logarithm bounds](https://proofwiki.org/wiki/Bounds_of_Natural_Logarithm).
More specifically, we use the fact that $$-\log(x) \ge 1 - x$$ to show:

$$
\begin{align}
D_\mathrm{KL}(p||q) &= \mathbb{E}_{p(x)} \left[ -\log \left( \frac{q(x)}{p(x)} \right) \right] \\
&\ge \mathbb{E}_{p(x)} \left[ \left( 1 -\frac{q(x)}{p(x)} \right) \right] \\
&=\int p(x) \left( 1 -\frac{q(x)}{p(x)} \right) dx 
&& \text{definition of expectation} \\
&=\int  p(x) - q(x)  dx \\
&= 1 - 1 \\
&= 0
\end{align}
$$

<br>

### 4. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$\log \det(\mathbf{A}) = \mathrm{Tr}(\log \mathbf{A})$$

We show that $$\log \det(\mathbf{A}) = \mathrm{Tr}(\log \mathbf{A})$$ for 
*diagonalizable* matrices. This property holds for general matricies, but we do not
prove that here.

Suppose that $$\mathbf{A}$$ is a diagonalizable matrix with eigenvalues $$\lambda_i$$.
Then, 

$$
\begin{align}
\log \det(\mathbf{A}) &= \log \left( \prod_i \lambda_i \right) \\
&= \sum_i \log \lambda_i \\
&= \mathrm{Tr}(\log \mathbf{A})
\end{align}
$$

The first line makes use of the identity $$\det(\mathbf{A}) = \prod_i \lambda_i$$. 
The third line makes use of the identity 
$$\log(\mathbf{A}) = \mathbf{P}^{-1}(\log \boldsymbol{\Lambda})\mathbf{P}$$ for 
diagonalizable $$\mathbf{A}$$ and that
$$\mathrm{Tr}(\mathbf{A}) = \sum_i \lambda_i$$. 

<br>

### 5. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Posterior motivation for $$\sigma(\cdot)$$

Using $$\sigma(\cdot)$$ as the output function for classification, where $$\sigma$$ is either the
sigmoid or softmax function, can be motivated from a number of angles. One interesting motivation
from [Bishop](https://www.bishopbook.com) uses the class posterior probability as follows.

#### Binary classification

Suppose we have data $$\mathbf{x}$$, labels $$\mathcal{C}$$ sampled from $$p(\mathbf{x}, \mathcal{C})$$, where $$\mathcal{C} \in {0, 1}$$.
Then the posterior probability that $$C=1$$ can be written as

$$
\begin{align}
p(\mathcal{C}=1|\mathbf{x}) &= \frac{p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)}{p(\mathbf{x}|\mathcal{C}=0)p(\mathcal{C}=0) + p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)} \\
&=\frac{1}{\frac{p(\mathbf{x}|\mathcal{C}=0)p(\mathcal{C}=0) + p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)}{p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)}} && \text{reciprocal rule} \\
&=\frac{1}{1+\frac{p(\mathbf{x}|\mathcal{C}=0)p(\mathcal{C}=0)}{p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)}} \\
&=\frac{1}{1+\exp(-a)} \\
&= \sigma(-a)
\end{align}
$$

where we have defined 
$$
a=\ln\frac{p(\mathbf{x}|\mathcal{C}=1)p(\mathcal{C}=1)}{p(\mathbf{x}|\mathcal{C}=0)p(\mathcal{C}=0)}.
$$
Therefore, given some function that outputs logits $$\text{h} = f(\mathbf{x})$$, the function $$\sigma(h)$$ directly corresponds to the posterior probability of observing the positive class $$\mathcal{C}=1$$.


#### Multiclass classification

The same motivation extends to the case when we have $$K$$ classes. The posterior probability that $$C=k$$ can be written as

$$
\begin{align}
p(\mathcal{C}=k|\mathbf{x}) &= \frac{p(\mathbf{x}|\mathcal{C}=k)p(\mathcal{C}=k)}{\sum_j p(\mathbf{x}|\mathcal{C}=j)p(\mathcal{C}=0)} \\
&= \frac{\exp(a_k)}{\sum_j \exp(a_j)} \\
&= \sigma(a_k)
\end{align}
$$

where we have defined 
$$ 
a_k = \ln p(\mathbf{x}|\mathcal{C}=k)p(\mathcal{C}=k).
$$
Interestingly, the multiclass motivation is much easier to see and simpler to derive.
