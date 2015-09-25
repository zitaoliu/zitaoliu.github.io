---
layout:     post
title:      漫谈算法（四）分治算法 Divide and Conquer Algorithm
date:       2011-04-19 12:17:10
summary:    分治算法是基于多分枝递归的一种算法设计模式。分治算法递归地把一个大问题分解为多个类型相同的子问题，直到这些子问题足够的简单能被直接解决。最后把这些子问题的解结合起来就能得到原始问题的解。
categories: cs algorithm
---

先看一段来自wikipedia的定义：[http://en.wikipedia.org/wiki/Divide_and_conquer_algorithm](http://en.wikipedia.org/wiki/Divide_and_conquer_algorithm)

> Divide and conquer (D&C) is an important algorithm design paradigm based on multi-branched recursion. A divide and conquer algorithm works by recursively breaking down a problem into two or more sub-problems of the same (or related) type, until these become simple enough to be solved directly. The solutions to the sub-problems are then combined to give a solution to the original problem.

简单翻译一下：

分治算法是基于多分枝递归的一种算法设计模式。分治算法递归地把一个大问题分解为多个类型相同的子问题，直到这些子问题足够的简单能被直接解决。最后把这些子问题的解结合起来就能得到原始问题的解。

根据这个定义，我们可以很明显的知道，对于D&C问题，我们解决它需要两步，

* 一是要找到递归式；
* 二是要根据递归式能找到最后的答案。

## 什么是递归式。

下面是从算法导论（Introduction to Algorithm Edition 3）上copy下的一小段话，解释的相当清楚。
Recurrences go hand in hand with the divide-and-conquer paradigm, because theygive us a natural way to characterize the running times of divide-and-conquer algorithms.A recurrence is an equation or inequality that describes a function in terms of its value on smaller inputs.
举个例子，
T(n) = 4T(n/2) + n，这个表达式就是我们的递归式。
对于不同的问题，我们得到的递归式各不相同，通常这个是因问题而已。但总体思路是如何分解原始的问题。
而本文的重点则是在后面，介绍如何在有了递归式的情况下，找到问题的答案。如分析某个问题的时间复杂度。
通常，解决这类问题（一直递归式，找答案）有三种方法：
1. Mathematical Induction 数学归纳法
2. Recursion Tree 画递归树找规律
3. Master Theorem 主定理(好像中文版的算法导论上就是这样翻译的，感觉真挫)
后面就简单针对以上三种方法用具体例子做一个简单的说明。
1. Mathematical Induction 数学归纳法
使用数学归纳法，这个大家基本都清楚，就是假设一个在n的时候结论成立，证明在n+1的时候结论也成立，当然，在我们这里，稍微有点变化。举个例子。
T(n) = T(n/2) + T(n/4) + T(n/8) + n
现在我们要就上面表达式T(n)，现在我们就先guess T(n) = Theta(n)。
当然我们知道要证明T(n) = Theta(n)，我们需要分别证明T(n) = O(n)和T(n) = Omega(n)。
很显然，这里T(n) = Omega(n)的，因为T(n) = T(n/2) + T(n/4) + T(n/8) + n > n，显然，T(n) = Omega(n).
下面用数学归纳法证明T(n) = O(n)
假设T(n) <= cn，所以其中c是一个常数。
所以T(n) <= c*n/2 + c*n/4 + c*n/8 + n = (7c/8+1)n
我们只需让(7c/8+1)n <= cn，显然我们可以找到一个正常数c使该式成立。所以T(n) = O(n)。
综上，T(n) = Theta(n)。
上面的证明是没有问题了，但是可能有朋友要问，凭什么你一开始就guess T(n) = Theta(n) 呢？没错，make a good guess 是这种方法的关键，下面就简单的说一下make this guess的intuition。
首先，我们可以简单的画出下面这棵树。

![divide-and-conquer-tree](/images/posts/{{ page.date | date: site.date_dir_format }}/divide-and-conquer-tree.jpg)

当然我们可以发现，在每一层，随着递归的深入，每一层的总cost是减小的，所以我们可以推测，在层数很大的情况下，那一层的总cost很小，无法和顶层相比，这也就是说，这个问题的T(n)主要由顶层决定，最顶层是n，所以我们有理由guess答案是cn。c为一常数。
下面在介绍两个guess的小tricks
1）遇到T(n) = aT(n/b + d) + f(n)的时候，在绝大多数的情况下，我们可以直接忽略d来进行guess，因为当n足够大的时候 n/b + d 和 n/b 几乎是一样的。
2）guess的时候可以加一个常数项，比如上面guess T(n) = O(n)的时候，我们用的是 T(n)<= cn，有时候推导不顺利的时候，可以试试 用T(n) <= cn-d，这样可以摆脱一些常数项的干扰。
2. Recursion Tree 画递归树找规律
其实这个方法和前面的画树的方法很相似，这里就举一个简单的例子来说明问题。
现在假设我们的递归式是 T(n) = aT(n/b) + n^k。 这里由于画树比较麻烦（偷个懒(*^__^*) 。。。）我就画成表格了，其实原理都一样，只是呈现的方式不一样。

![table](/images/posts/{{ page.date | date: site.date_dir_format }}/table.jpg)

当然，我们知道最后的level是 log_{b}^n,然后我们把最后一列相加，就得到了我们的结果，








