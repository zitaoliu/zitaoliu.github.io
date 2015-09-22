---
layout:     post
title:      漫谈算法（零）符号标记以及基本数学公式
date:       2011-04-12 12:52:29
summary:    
categories: cs algorithm
---

说到算法，大家最熟悉的恐怕就是这个大欧标记了，即 \\(\mathcal{O}\\)。什么基于比较的排序算法最好是 \\(\mathcal{O}(n \log n)\\)了什么的。（注，本系列文章里不区分 \\(\log\\) 和 \\(\lg\\)，两个符号都是表示以二为底的对数）

更general一点，我们可以写成 \\(\mathcal{O}(g(n))\\)，这个东西是什么吗，其实他是一个集合，表示所以满足条件的一系列函数，这一系列函数有什么特点呢？那就是 \\(g(n)\\)是他们的上界，更准确的说，是一个constant \\(c\\)， \\(cg(n)\\) 是他们的上界。如下图，（截自算法导论）

![big O notation g function illustrationn](/images/posts/{{ page.date | date: site.date_dir_format }}/big-o-g-function.jpg)

假设 \\(f(n)\\) 表示我们 quick sort 的时间，我们写作 \\(f(n) = \mathcal{O}(n\log n)\\)，这时候你可能要问了，刚才上面不是说 \\(\mathcal{O}(n\log n)\\) 表示一个集合吗，这么集合里面显然都是函数，那怎么能写 **函数 = 函数的集合**呢？没错，其实这样写确实不好，但是我们现在已经约定俗成了，这里的等号就表示元素和集合关系的属于的符号。

现在来看一下 \\(\mathcal{O}\\) 的formal的定义。

\\[ \mathcal{O}(g(n)) = {f(n) : 存在一个正常数 c，和一个 N_0， 对于所有的 N > N_0， 0 \leq f(n) \leq cg(n)} \\]

其实结合上面的图和这个定义，\\(\mathcal{O}\\) 的意思还是很明显的。他是 \\(f(n)\\) 的一个upper bound。

同理，我们可以定义 \\(\mathcal{\Omega}\\) 和 \\(\mathcal{\Theta}\\)

\\[ \mathcal{\Omega} (g(n)) = {f(n): 存在一个正常数 c，和一个 N_0， 对于所有的 N > N_0， 0 \leq cg(n) \leq f(n) } \\]

当然，这是我们 \\(f(n) \\)的一个lower bound。

\\[ \mathcal{\Theta} (g(n)) = {f(n): 存在正常数 c_1 和 c_2，和一个 N_0， 对于所有的 N > N_0， c_1g(n) \leq f(n) \leq c_2g(n)} \\]

下面是算法导论里面完整的图。


![big O notation g function illustrationn](/images/posts/{{ page.date | date: site.date_dir_format }}/big-o-g-function-all.jpg)



通过上面的定义我们可以发现，在\\(\mathcal{O}\\)，\\(\mathcal{\Omega}\\) 和 \\(\mathcal{\Theta}\\)的定义中，我们都出现了“=”，当然，类比当我们数字的比较，我们有大于等于，小于等于，同样，我们也有大于，小于。

当然对于这个等号，我们可以说是一个tight的bound，比如 \\(2n^2 = \mathcal{O}(n^2)\\)，这个bound就是asymptotically tight的，但是对于 \\(2n = \mathcal{O}(n^2)\\) 来说，这个就不是tight的。所以，这时我们的 \\(o\\) 就孕育而生了。用算法导论里面的原话就是： We use \\(o\\) to denote an upper bound that is not asymptotically tight.

下面来看 \\(o\\) 的formal的定义。

\\[ o(g(n)) = {f(n): 对于任意的正常数 c，存在一个 N_0，对于所有的 N > N_0, 0 \leq f(n) < cg(n)} \\]

同样，我们可以定义 \\(\omega\\)。

\\[\omega (g(n)) = {f(n): 对于任意的正常数 c，存在一个 N_0，对于所有的 N > N_0, 0 \leq cg(n) \leq f(n)} \\]

=============================华丽的分割线=============================

对于这些标记，其实我们还可以从growth rate和极限的方面来考虑。

比如对于 \\(o\\)， it means that \\(g(x)\\) grows much faster than \\(f(x)\\), or similarly, the growth of \\(f(x)\\) is nothing compared to that of \\(g(x)\\).（偷懒一下，直接从wikipedia上抄下来）

\\[ \lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} = 0 \\]


其余的大家自己也应该都可以琢磨出来。(*^__^*) 嘻嘻……

最后给几个常用且简单的数学公式，权当给自己提醒了。


* \\( n! \leq n^n \\)
* \\( n! \leq (\frac{n}{e})^n \\)
* \\( \log n! = \Theta(n \log n) \\)
* \\( e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots = \sum_{i = 0}^\infty \frac{x^i}{i!} \\)
* \\( e^x \geq 1 + x \\)
* \\( a^{\log_b c} = c^{\log_b a} \\)
* \\( \lim_{n \rightarrow \infty} (1 + \frac{x}{n})^n = e^x \\)
* \\( x - 1 < \lfloor x \rfloor \leq x \leq \lceil x \rceil  < x + 1 \\)







