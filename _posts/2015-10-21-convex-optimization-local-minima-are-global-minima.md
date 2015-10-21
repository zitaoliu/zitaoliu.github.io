---
layout:     post
title:      Proof of "For convex optimization problems, local minima are global minima."
date:       2015-10-21 16:03:29
summary:    I would like to show how to prove "For convex optimization problems, local minima are global minima."
categories: cs ml optimization
---

Probably, everyone in or partially in machine learning or data mining heard about the quote **"There is no local minima for convex problem."** Today I would like to show the mathematical proof of this statement.


Before I start the proof, I would like to make things clear:

* What is convex optimization?
* What does the following notation mean?

The convex optimization problems are defined as follows: 

$$
\begin{align}
 			& min_{x \in D} f(x)  \\ \\
 \mbox{subject to } & g_i (x) \leq 0, i = 1, \cdots, m \\ \\
 			& h_j (x) = a_j^\top x + b_j = 0, j = 1, \cdots, r
\end{align}
$$

where $$f$$ and $$g_i$$ are convex and $$D$$ is the feasible set, i.e., $$ D = dom(f) \cap  \bigcap_{i = 1}^m dom(g_i) \cap \bigcap_{j = 1}^r dom(h_j) $$. 


Now lets look at how to prove the following statement. It turns out that the proof is pretty easy by using "proof by contradiction".

### Theorem.

> For convex optimization problems, local minima are global minima.


### Proof.

Let $$x$$ be the local minima with radius $$\rho$$. Since we assume the statement is incorrect, there is some feasible $$z$$, such that $$f(z) < f(x)$$ and $$ \|x - z\| > \rho$$.

Let's construct $$y$$ in the following way:

$$y = tz + (1 - t) x$$, where $$t \in [0, 1]$$.

First, $$y \in D$$ due to the fact that both $$x$$ and $$z$$ are feasible points in $$D$$ and $$D$$ is a convex set.

Then, $$y$$ satisfy all the constraints ($$g_i$$ and $$h_j$$). Very easy to check and remember $$g_i$$s are convex.

Up to now, we have a local minima $$x$$ (with radius $$\rho$$), a point $$z$$ outside the $$\rho$$-neighborhood, and $$y$$, which on the line of $$x$$ and $$z$$. We can take $$t$$ small enough to bring $$y$$ into the $$x$$'s $$\rho$$-neighborhood, which means $$y$$ is in $$x$$'s local area.

Since $$f$$ is a convex function, we have 

$$f(y) \leq tf(z) + (1-t)f(x) < f(x)$$

Here we see, $$f(y)$$ is less than $$f(x)$$ which contradicts with the assumption that $$f(x)$$ is the local minima. This means the assumption is wrong, which concludes the proof $$\blacksquare$$.










