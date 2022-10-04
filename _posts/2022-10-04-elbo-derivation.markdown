---
layout: post
title:  "Deriving the Evidence Lower Bound (ELBO)"
date:   2022-10-04
tag: technical
---

Suppose we have a joint distribution $$p(\mathbf{x}, \mathbf{z})$$ where $$\mathbf{z}$$
are latent variables. Then the Evidence Lower Bound (ELBO) for 
$$p(\mathbf{x})$$ can be derived as:

$$
\begin{align}

\log p(\mathbf{x}) &= \log \int p(\mathbf{z}, \mathbf{x}) d\mathbf{z} && 
\text{definition of marginalization} \\

&= \log q(\mathbf{z}|\mathbf{x}) \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} 
&& \text{identity trick} \ q(\mathbf{z}|\mathbf{x})/q(\mathbf{z}|\mathbf{x})  = 1 \\

&= \log \mathbb{E}_{q(\mathbf{z}| \mathbf{x})} \left[ \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} \right] 
&& \text{definition of expectation} \\

&\ge \mathbb{E}_{q(\mathbf{z}| \mathbf{x})} \left[ \log \frac{p(\mathbf{z}, \mathbf{x})}{q(\mathbf{z}|\mathbf{x})} \right] 
&& \text{Jensen's inequality} \\

&= \mathcal{L}

\end{align}
$$
