---
layout: post
title:  Many Small Proofs and Derivations
date:   2023-03-10
tag: technical
---

*Last updated: March 10, 2023*

When reading textbooks, papers, or work stuff, I occasionally find myself writing small 
proofs or derivations to better understand a particular topic. Eventually I'll forget 
these derivations and have to look them up or re-derive them again.

This post is an attempt to gather such derivations in a central place for future use.
I plan to occasionally update this post as new material comes up.

<br><br>


### 1. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $$\log \det(\mathbf{A}) = \mathrm{Tr}(\log \mathbf{A})$$

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