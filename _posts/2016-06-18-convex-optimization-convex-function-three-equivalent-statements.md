---
layout:     post
title:      Convex Function And Its Three Equivalent Statements
date:       2016-06-18 16:03:29
summary:    What is a convex function?
categories: cs ml optimization
---


### Convex function

$$f: \mathbb{R}^n \rightarrow \mathbb{R} $$ such that $$dom(f) \subseteq \mathcal{R}^n$$ convex, and 

$$f(tx + (1-t)y) \leq tf(x) + (1-t)f(y)$$

for $$0 \leq t \leq 1$$ and all $$x, y \in dom(f)$$.


If $$f$$ is differentiable on $$\mathbb{R}^n$$, then the following statements are equivalent:

* (a) $$f$$ is convex
* (b) $$f(y) \geq f(x) + \bigtriangledown f(x)^T(y-x)$$ for all $$x, y \in \mathbb{R}^n$$
* (c) $$(\bigtriangledown f(x) - \bigtriangledown f(y))^T (x-y) \geq 0$$ for all $$x, y \in \mathbb{R}^n$$

The equivalence proof of (a), (b), and (c) can be found in [https://www.math.washington.edu/~burke/crs/516/notes/ch1.pdf](https://www.math.washington.edu/~burke/crs/516/notes/ch1.pdf). Also I keep a [local copy]({{ site.baseurl }}/download/opt_doc/ch1.pdf).

In the following, I am going to proof how to derive (b) from (a).

#### Proof

From the definition of convex function above, we have 

$$f(x + t(y - x)) \leq f(x) + t (f(y) - f(x))$$

which can be rewritten as

$$\frac{f(x + t(y-x)) - f(x)}{t(y-x)} \leq \frac{f(y) - f(x)}{y - x}$$

Then we take $$\lim_{t\to 0}$$ on both sides, we have 

$$\bigtriangledown f(x) \leq \frac{f(y) - f(x)}{y-x}$$

which is equal to (b) $$\blacksquare$$.


