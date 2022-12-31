---
layout: post
title:  "Linear Sandwich"
date:   2022-10-11
tag: technical
---

Creating a `Linear` sandwich by stacking a bunch of `Linear` layers on top of each other
just results in another linear transformation. Below, we show that this is indeed the 
case.

Suppose we have $$3$$ `Linear` layers with parameters $$\mathbf{W}_i$$, $$\mathbf{b}_i$$
$$, i \in \{1, 2, 3\}$$. Then given input, target $$\mathbf{x}$$, $$\mathbf{y}$$ we have

$$
\begin{align}
\mathbf{y} &= \mathbf{W}_1(\mathbf{W}_2 (\mathbf{W}_3\mathbf{x} + \mathbf{b}_3) + \mathbf{b}_2) 
  + \mathbf{b}_1 \\

&= \mathbf{W}_1\mathbf{W}_2(\mathbf{W}_3\mathbf{x} + \mathbf{b}_3) 
+ \mathbf{W}_1\mathbf{b}_2 + \mathbf{b}_1.
\end{align}
$$ 

To make the notation cleaner, we can define $$\mathbf{A}_1 = \mathbf{W}_1\mathbf{W}_2$$ 
and $$\boldsymbol{\beta}_1 = \mathbf{W}_1\mathbf{b}_2 + \mathbf{b}_1$$. It's clear that
$$\mathbf{A}_1$$ and $$\boldsymbol{\beta}_1$$ are also linear because they're just 
compositions of linear functions. Substituting them into the last equation we have

$$
\begin{align}
\mathbf{y} &= \mathbf{A}_1(\mathbf{W}_3\mathbf{x} + \mathbf{b}_3) + \boldsymbol{\beta}_1 \\
&= \mathbf{A}_1\mathbf{W}_3\mathbf{x} + \mathbf{A}_1\mathbf{b}_3 + \boldsymbol{\beta}_1.
\end{align}
$$

Again, we can define $$\mathbf{A}_2 = \mathbf{A}_1\mathbf{W}_3$$,
$$\boldsymbol{\beta}_2 = \mathbf{A}_1\mathbf{b}_3 + \boldsymbol{\beta}_1$$ and 
substitute into the last equation to get

$$
\mathbf{y} = \mathbf{A}_2\mathbf{x} + \boldsymbol{\beta}_2
$$

which is yet another linear function.

Obviously, the process above can be extended to any number of layers. This shows than 
any size stack of `Linear` layers is linear.
