---
layout:     post
title:      漫谈算法（三）NP问题
date:       2011-04-15 09:11:10
summary:    解释一下什么是NP问题，什么是NP hard问题，什么是NP完全问题。再举几个经典的NP-complete的问题。 
categories: cs algorithm
---

# 什么是NP/NP-hard/NP-complete问题


看下面的图，他们之间的关系表示的比较清楚。

* **P Problem**：这个应该最易理解，就是一个问题可以在Polynominal的时间的得到解决，当然，是对于任意input size。

* **NP Problem**：对于一类问题，我们可能没有一个已知的快速的方法得到问题的答案，但是如果给我们一个candidate answer，我们能够在polynominal的时间内验证这个candidate answer到底是不是我们已知问题的答案，这类问题叫做NP problem。所以很显然 P Problem是NP problem的一个子集。

* **NP-hard Problem**：对于这一类问题，用一句话概括他们的特征就是“at least as hard as the hardest problems in NP Problem”， 就是NP-hard问题至少和NP问题一样难。

* **NP-complete Problem**：对于这一类问题，他们满足两个性质，一个就是在polynomial时间内可以验证一个candidate answer是不是真正的解，另一个性质就是我们可以把任何一个NP问题在polynomial的时间内把他的input转化，使之成为一个NP-complete问题。

![np problem](/images/posts/{{ page.date | date: site.date_dir_format }}/np-problem.png)

所以对于NP-hard问题，我们可以把他们分成两个部分，一部分可以用polynomial的时间验证一个candidate answer是不是真正的answer，这一部分问题组成了NP-complete集合。

我们经常说的 \\(NP = P \\) 或者 \\( NP \neq P \\)，其实就是说目前而言，我们并不知道，是不是对于NP Problem集合里面的所有问题，都能够在Polynomial的时间内解决。当然只里面比较interesting的一点是，如果我们能把NP-complete集合中的任意一个问题在polynomial的时间内解决了，那么所有的NP问题都可以在polynomial的时间内解决。原因，看看上面说的NP-complete的性质就知道了，因为任何一个NP问题都可以在polynomial的时间内把他的input转化，使之成为一个NP-complete问题，所以....

介绍了上面说的一些定义，来举几个经典的NP-complete的问题。

## [Vertex Cover](http://en.wikipedia.org/wiki/Vertex_Cover)

Informally来说，就是对于一个图G(V,E)，我们在V中选一个subset V'， 使得E中的所有边的两点中的一个点在V'中。 所谓Vertex Cover也就是说V'中的点cover了每一条边（因为每一条边至少有一端是在V'中的啦）给你一个G(V,E)和一个k，问你在整个G中，是否存在一个大小为k的Vertex Cover（**Decision Problem**）

Formally, a vertex cover of a graph G is a set C of vertices such that each edge of G is incident to at least one vertex in C. The set C is said to cover the edges of G. The following figure shows examples of vertex covers in two graphs (the set C is marked with red).

![vertex-cover-problem](/images/posts/{{ page.date | date: site.date_dir_format }}/vertex-cover-problem.png)

## [3-CNF-SAT](http://en.wikipedia.org/wiki/3SAT#3-satisfiability)

举个例子，\\( E = (x_1 \vee \neg x_2 \vee \neg x_3) \wedge (x_1 \vee x_2 \vee x_4) \\)，每一个括号包括的东西叫一个clause，里面的 \\(x_1, x_2, x_3 \\) 在离散数学里面叫做文字，取值True或者False。每个括号之间是合取，括号里面是析取，这个问题就是，对于这样的一个表达式，是不是能找到一组 \\( x_i \\) 的值，使得表达式为True。 Given the expression, is there some assignment of TRUE and FALSE values to the variables that will make the entire expression true?

## [Integer Linear Programming](http://en.wikipedia.org/wiki/Linear_program#Integer_unknowns)

当然这个最显而易见了，就是LP中的所有变量都要求是整数了。关于Linear Programming的问题，后面会专门有一篇文章来讲解。O(∩_∩)O~


# 证明一个问题是NP问题。

给你一个结果，你能在polynomial的时间内验证他的正确性。

## 证明一个问题是NP-hard的。

对于证明一个问题是NP-hard，我们经常用到的一个technique是归约（reduction），通常用<=这个符号来表示，如P<=Q，这个就表示P is reducible to Q or Q is the reduction from P or P is reduced to Q. P问题可以归约到Q问题。可以把P归约到Q。这里的reduction的符号可以当成是 比较难易程度的小于等于号，意味着问题Q至少和问题P一样难。当我们要证明一个问题是NP-hard的时候，我们通常要做的是找到一个NPC问题（就用这个代替NP-complete问题），把这个NPC问题归约到NP-hard上去，即NPC<=NP-hard。

证明一个问题是NPC的。要证NPC，我们要分两步走，第一步证明这个问题属于NP，就是验证答案（感觉这句话我都说烂了）。第二步，证明这个问题是NP-hard的。当然这里面第二步是问题的关键，但是第一步也一定要在证明里面提到。

如何证明一个问题是NP-hard 是以上证明的关键，即如何归约。

这里我们归约要做的主要步骤就是，

1. 把NPC的input转化到NP-hard的input，即每一个NPC的input，实际上都是一个NP-hard的input。

2. 把NP-hard的output转化到NPC的output上来，说明给我一个NP-hard的output，我就能给你一个NPC的output。

** 注意：以上的两个转化都要在polynomial的时间内完成。**


下面举几个例子来证明上面的归约的方法。

## 用 [3SAT]((http://en.wikipedia.org/wiki/3SAT#3-satisfiability)) 证明 [Vertex Cover]((http://en.wikipedia.org/wiki/Vertex_Cover)) 是NP-hard的。即 3SAT <= Vertex Cover

这个就是表明我们已知3SAT这个问题是NP-complete的，如何把3SAT问题归约到Vertex Cover上。

首先，我们要建立我们的通过input建立这两个问题的对应。假设我的3SAT是

\\( E = (x_1 \vee \neg x_2 \vee \neg x_3) \wedge (x_1 \vee x_2 \vee x_4) \\)

我们按照下面的方法构造我们的Graph，对应每一个个变量 \\( x_i \\)，我们构造点 \\( x_i \\) 和 \\( \neg x_i \\)，对于每一个clause，我们构造3个点，这3个点直接彼此有边，假设这三个点叫 A,B,C。同时我们还要建立A,B,C这三个点和该clause的联系：假设我们的clause是 \\( (x_1 \vee \neg x_2 \vee \neg x_3) \\) 我们就把 \\( x_1 \\) 和 A 连起来，\\( \neg x_2 \\) 和 B 连起来，\\( \neg x_3 \\) 和C连起来。注意，每一个clause有一个全连通的三角，他们共用那6个变量点 \\( (x_1, \neg x_1, x_2, \neg x_2, x_3, \neg x_3) \\) 如下图所示。

![3sat-to-vertex-cover](/images/posts/{{ page.date | date: site.date_dir_format }}/3sat-to-vertex-cover.jpg)

要注意的一点是，对于E中的每一个clause，我们都对应图里面的一个三角形（也就是我用矩形圈住的那部分），同时所有的clause共享上面的六个点，也就是2*变量个数 那么多个点是共用的。

通过这个图，我们也就建立起了3SAT和Vertex Cover之间的联系。通常这个也是此类证明问题中最难和最creative的部分。

后面就是表述一下如何进行转换的。通常这个是很trival的部分。

1. 假设我有一个解能满足3SAT，那么我就一定能找到相应的解满足Veterx Cover。 如上图，3SAT满足了，必然每一个clause满足，就拿 \\( (x_1 \vee \neg x_2 \vee \neg x_3) \\) 为例，这个式子满足了，必有一个变量为true，它可以是 \\( x_1 \\) 或者 \\( \neg x_2 \\) 或者 \\( \neg x_3 \\)，假设 \\( x_1 \\) 为true，这时对应的vertex cover中，我们就选上面6个点中的 \\( x_1 \\) ，同时对于下面的三角形中的3个点，我们选除了那个与 \\( x_1 \\) 相连的另外两个点。对于每一个clause，我们都可以这样做，同时，我们也cover了这个图中的所有边。也就是我们有了一个满足要求的vertex cover。

2. 假设我有一个解能满足Vertex Cover，那么我就一定能找到相应的解满足3SAT。因为要cover这个图，所以三角形里面至少要cover两个点，上面的一对一对的pair里面也至少要cover一个，所以对于一个size为n+2m的vertex cover（n是变量个数，m是clause的个数），我们一定可以找到一个满足的3SAT，（显然啊，因为每个clause都有一个点和上面的一对一对pair的点相连） （说的好拗口，郁闷。还不清楚的可以看下这个链接 [http://users.eecs.northwestern.edu/~fortnow/classes/w08/EECS395/lecture11.pdf](http://users.eecs.northwestern.edu/~fortnow/classes/w08/EECS395/lecture11.pdf) ）

然后，然后，。。。我们就证完了。



## 用3SAT证明ILP是NP-hard的。即 3SAT <= ILP

还是首先找映射，这个映射不涉及图的东西，应该比较容易构造和理解。

还是拿上面那个3SAT的例子说事。对于 每个clause，我们都对应于ILP中的一个constraint，比如 E中有4个变量，\\( x_1 \\), \\( x_2 \\), \\( x_3 \\) 和 \\( x_4 \\)， 我们的ILP中也有同样的这4个变量，并且我们要求他们都是只能取 0 或 1。对于一个clause，如 \\( (x_1 \vee \neg x_2 \vee \neg x_3) \\)，我们对应的constraint是 \\( x_1 + (1-x_2) + (1 - x_3) \leq 1 \\)，很显然了，ILP中的变量选0对应于3SAT中的变量选false，ILP中的变量选1对应于3SAT中的变量选true，这样我们就映射好了。

很显然，这两个问题的input/output的转换trival的不行了。如果一个clause满足了，对应的那个ILP中的constraint肯定也满足了；反之依然。偷个懒~O(∩_∩)O~

证毕。

**这类NP的证明问题其实还是很有难度的，只能说很锻炼脑子，对于它有没有用，这要看你对“useful”的定义了，仁者见仁，智者见智吧。**


