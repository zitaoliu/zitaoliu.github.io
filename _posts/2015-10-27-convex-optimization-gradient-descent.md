---
layout:     post
title:      Gradient Descent Essentials
date:       2015-10-22 15:33:29
summary:    Gradient descent essentials - interpretation, how to choose step size and more.
categories: cs ml optimization
---

Gradient descent is arguably the most widely used optimization techniques. At least in my personal research, it almost occupied the majority of my research solutions.

Gradient descent looks pretty simple at the first glance but it is worthwhile to dig into it a little bit.

### What is Gradient Descent?

Think about optimizing an unconstrained, smooth convex optimization problem 

$$min_x f(x)$$

Gradient descent solves the above problem as follows:

$$x^{(k+1)} = x^{(k)} - t_{k+1} \triangledown f(x^{(k)})$$

Start the iteration and stop at some point.

Intuitively, this can be understood easily: every iteration, we are moving along the direction which can minimize the function value and how far we move is controlled by step size $t_k$.

## Mathematical Interpretation

The intuition of gradient descent is pretty clear. However, as a mathematical tool, it should root in the solid mathematical foundation. 

Remember the [Taylor Series](https://en.wikipedia.org/wiki/Taylor_series),

$$f(x) = \sum_{n = 0}^\infty \frac{f^{(n)}(a)}{n!} (x - a)^n$$

In optimization, a widely used trick is **quadratic approximation** based on taylor expansion, 

$$f(y) \approx f(x) + \triangledown f(x)^\top (y-x) + \frac12 \triangledown^2 f(x) (y-x)^2$$

Here, we play the same trick with a **slight** change, we replace $$\triangledown^2 f(x)$$ by $$\frac{1}{t}I$$, which leads to the following approximation:

$$f(y) \approx f(x) + \triangledown f(x)^\top (y-x) + \frac{1}{2t} (y-x)^2$$

* $$f(x) + \triangledown f(x)^\top (y-x) $$ represents the linear approximation to $$f$$.
* $$\frac{1}{2t} (y-x)^2$$ represents the proximity term to $$x$$, with a weight $$\frac{1}{2t}$$.

Going back to our minimization problem, we want to find the minimizer $$x^*$$ iteratively. Assume we just finish the $$k$$th iteration and are about to start the $$(k+1)$$th iteration. We have to solve the following problem: 

$$x^{(k+1)} = arg \min f(x) = arg \min \sum_{n = 0}^\infty \frac{f^{(n)}(x^k)}{n!} (x - x^k)^n$$

By applying the **slightly** changed quadratic optimization, we will solve the following new problem:

$$x^{(k+1)} = arg \min_y f(x^k) + \triangledown f(x^k)^\top (y-x^k) + \frac{1}{2t} (y-x^k)^2 $$

Of course, this is much easier to solve. Let's to the high school algebra,

$$
\begin{align}
x^{(k+1)} & = arg \min_y f(x^{(k)}) + \triangledown f(x^{(k)})^\top (y-x^{(k)}) + \frac{1}{2t} (y-x^{(k)})^2 \\
& = arg \min_y \frac{1}{2t} \Big( y^2 - 2(x^{(k)} - t \triangledown f(x^{(k)})) y  \Big) \\
& = arg \min_y \frac{1}{2t} \Big( y - (x^{(k)} - t \triangledown f(x^{(k)}))  \Big)^2 \\
& = x^{(k)} - t \triangledown f(x^{(k)})
\end{align} 
$$

Note that we apply this approximation at every iteration, and we can set $$t$$ to different values according to each iteration, such as setting $$t$$ to $$t_k$$ at $$k$$th iteration.


Here is a plot illustration from my instructor [Ryan](http://www.stat.cmu.edu/~ryantibs/)'s [slides](http://www.stat.cmu.edu/~ryantibs/convexopt/lectures/05-grad-descent.pdf).

![gd_approx_illustration](/images/posts/{{ page.date | date: site.date_dir_format }}/gd_approx_illustration.png)


## How to choose Step Size

Setting the step size is an art in gradient descent and it can directly lead your optimization procedure to success or failure. 

I have seen lots of presentations and papers talked about this. Some did it right, some did it wrong, and some did it partially right (of course, it means partially wrong.)

There is no need to argue the importance of step size: if it is too small, it takes forever to get converged; if it is too large, the program jumps back and forth and never reaches the optimality.


### Backtracking Line Search

A general solution to adaptively choose the step size is to use **backtracking line search**. It is a general and simple solution and lots of people have demonstrate its practical usage.

The backtracking line search works as follows:

1. First fix parameters $$0 < \beta < 1$$ and $$0 < \alpha \leq 1/2$$.
2. At each iteration, start with $$t = 1$$, and while $$f(x − t \triangledown f(x)) > f(x) − \alpha t \| \triangledown f(x) \|_2^2 $$, shrink $$t = \beta t$$. Else perform gradient descent update $$ x^+ = x − t \triangledown f(x) $$.

Usually, $$\alpha$$ can be simply set to 1/2. 


#### Interpretation




### Exact Line Search


### Constant Step Size

I have to admit the power of backtracking line search. However, in some (lots of) cases, we even don't need the backtracking. 

When the function $$f$$ is 

1. convex
2. differentiable
3. dom$$(f) = \mathbb{R}^n$$
4. $$\triangledown f$$ is Lipschitz continuous.

**If our objective function satisfy the above conditions, we can simply set the step size to constant**!


#### Lipschitz continuous

A function $$f$$ is **Lipschitz continuous** if for any x and y, we can always find a positive constant $$L$$, such that 

$$\| f(x) - f(y)  \|_2 \leq L \|x -y \|_2$$

Here we use $$\|\cdot\|_2$$ since our input is scalar, the distance function depends on the metric space.

In our case, we require $$\triangledown f$$ is Lipschitz continuous, which means 

$$\| \triangledown f(x) - \triangledown f(y)  \|_2 \leq L \|x -y \|_2$$

#### Choice of step size

**Theorem**

> Gradient descent with fixed step size $$t \leq 1/L$$ satisfies $$f(x^{(k)}) - f^* \leq \frac{\|x^{(0)} - x^* \|_2^2}{2tk}$$.

**Proof**




The above Theorem leads to the following two equivalent lemmas.

**Lemma1** 

> Gradient descent with fixed step size $$t \leq 1/L$$ has convergence rate $$\mathcal{O}(1/k)$$.


**Lemma2** 

> Gradient descent with fixed step size $$t \leq 1/L$$ needs $$\mathcal{O}(1/\epsilon)$$ to get $$f(x^{(k)}) - f^* \leq \epsilon$$.



