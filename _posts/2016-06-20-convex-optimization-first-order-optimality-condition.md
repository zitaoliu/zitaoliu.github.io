---
layout:     post
title:      First-Order Optimality Condition
date:       2016-06-20 15:03:29
summary:    What is "First-Order Optimality Condition" ?
categories: cs ml optimization
---

I will continue the notation I used in [previous post]({% post_url 2016-06-19-convex-optimization-local-minima-are-global-minima %}).

The convex optimization problems are defined as follows: 

$$
\begin{align}
 			& min_{x \in D} f(x)  \\ \\
 \mbox{subject to } & g_i (x) \leq 0, i = 1, \cdots, m \\ \\
 			& h_j (x) = a_j^\top x + b_j = 0, j = 1, \cdots, r
\end{align}
$$

Here, for notational brevity, the convex optimization problems can be expressed in the following way:

$$ min_{x \in D} f(x) \mbox{ subject to } C$$

where 

$$C = \{ x: g_i(x) \leq 0, i = 1, \cdots, m, Ax = b \} $$

### First-order condition for optimality.

> For a convex problem above, if $$f$$ is differentiable, a feasible point $$x$$ is optimal if and only if $$ \triangledown f(x)^\top (y - x) \geq 0 $$ for all $$y \in C$$.

### Take Home Message

*All feasible directions from $$x$$ are aligned with increasing gradient $$\triangledown f(x)$$.*

### Special Case

When $$C = \mathbb{R}^n$$ (unconstrained optimization), then optimality condition reduces to familiar $$\triangledown f(x) = 0$$.

