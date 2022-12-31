---
layout: post
title:  "Probabilistic Numerics"
date:   2022-12-12
tag: technical
---

I recently came across the topic of 
[probabilistic numerics](https://en.wikipedia.org/wiki/Probabilistic_numerics).  The 
essence of the idea is actually very simple, as I'll try to illustrate in this post.

Almost all problems that we face in real life are intractable. Because of this, we're 
forced to use numerical methods to approximate their solutions. For example, finding the 
minimum of a loss function in machine learning is generally intractable for 
classification problems. To get an approximate solution, we use (stochastic) gradient 
descent to get a point estimate of the true minimum.

However, the point estimate is just that, an _estimate_. In fact, at the end of the 
approximation, we have no idea how good our estimate is: we could be very close to the 
true minimum or we could be very far off. To put it differently, there is  _uncertainty_ 
associated with our estimate.

#### Deriving Worst Case Bounds

A common way to handle uncertainty is to derive bounds on the worst (or average) case 
estimate. Unfortunately, deriving these bounds requires godly math talent and making 
strong assumptions about the problem. Furthermore, for complicated problems like deep 
learning, the bounds are extremely loose and don't have any benefits in practice.

One particularly poignant example is from my time at Google Research. While there, 
I worked on [Adanet](https://github.com/tensorflow/adanet), a deep learning library 
whose main innovation was to provide generalization guarantees based on bounds some 
researchers had derived. Our collaborators were very impressed at how smart this 
sounded, but it never worked in practice! We always ended up using (cross-)validation, 
which was the dirty secret on our team.

#### Probabilistic Inference

Luckily, a straightforward method exists to handle uncertainty, namely probabilistic 
modeling. The basic idea behind probabilistic numerics is to **treat the approximation 
as a random variable**, and use all the tools of probabilistic inference to quantify the
uncertainty of our approximation. The neat thing about this is that we can combine and 
propagate the uncertainty arising from our approximation with the uncertainty arising 
from our data, model, etc. Therefore, instead of a single point estimate, we can output 
a full (posterior) distribution of potential estimates.

Bayesian optimization is probably the most common application of probabilistic numerics 
in machine learning. However, similar probabilistic formulations can be extended to many 
other numerical methods in integration, linear algebra, ordinary differential equations, 
etc. 

In retrospect, it's very "obvious" that probabilistic numerics can be naturally extended
beyond optimization. Since I work pretty extensively with Bayesian optimization, I'm a 
little annoyed I didn't think of this :) .


