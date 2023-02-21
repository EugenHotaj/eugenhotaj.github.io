---
layout: post
title:  Two Proofs About the Kullback–Leibler Divergence
date:   2023-02-21
tag: technical
---

This post shows two different ways to prove that $$D_\mathrm{KL}(p || q) \ge 0$$ given 
distributions $$p(x), q(x)$$.

### Jensen's Inequality

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

### Natural Logarithm Bounds

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