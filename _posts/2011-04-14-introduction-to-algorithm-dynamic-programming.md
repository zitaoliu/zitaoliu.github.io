---
layout:     post
title:      漫谈算法（二） 动态规划 Dynamic Programming
date:       2011-04-14 18:27:10
summary:    动态规划，Dynamic Programming。这里的programming没有翻译成编程，是因为，这里的programming的意思是指一个tabular method。其实这也暗示了DP的本质，用一个table保存子问题的中间结果。
categories: cs algorithm
---

动态规划，Dynamic Programming。这里的programming没有翻译成编程，是因为，这里的programming的意思是指一个tabular method。其实这也暗示了DP的本质，用一个table保存子问题的中间结果。（后面会有例子具体介绍）

和分治算法比较类似，但不同的是分治算法把原问题划归为几个相互独立的子问题，从而一一解决，而动态规划则是针对子问题有重叠的情况的一种解决方案。

目前design DP主要有两个思路：

### 1. Recursive method

即首先把问题用递归的方法解决，然后用一个table保存recursive中的中间结果，这不就避免了递归中重复计算的低效了吗？遇到需要计算以前计算过的东西，直接查表就OK，总之一句话，先写recursive，然后比葫芦画瓢基本就能把DP的方法写出来。这里的难点是如何找到recursive。算法导论里面也给的是这个思路。下面的前三个例子全部出自《算法导论》。

### 2. Exhaust search

这个好像是我们老师发明的方法，这里有篇Kirk的论文， [How to design dynamic programming algorithms sans recursion](people.cs.pitt.edu/~kirk/papers/dynprog.ps)。有兴趣的大家可以仔细研究一下，我下面也会简单举例介绍一下这个方法。

下面的例子中多数代码都是伪代码，旨在illustrate idea。同时节省时间。代码中都省去了backtrack的过程，即只得到了optimal solution的值，省去了如何construct optimal solution的过程。这个一般用一个数组记录一下就OK了。

先来个比较简单的例子（其实后面的也不难O(∩_∩)O~） 

### 例 Rod-cutting problem

Input：有一个长n米的木头，和一个price table，table如下：

| ------------- | - | - | - | - | - | - | --- |
| 长度 i         | 1 | 2 | 3 | 4 | 5 | 6 | ... | 
| 价格 \\(P_i\\) | 1 | 5 | 8 | 9 | 10| 17| ... |

意思很明显，就是长度为1米的木头可以买1元，长5米的可以卖10元，依次类推

Output：找一个cut的方法，使最后赚的钱最多。

很显然，这个递归的主要思路是我切一刀之后，分成两段，一段我按table的价钱卖了，另一段我当成一个新的子问题，继续作为我的函数的新的参数，这样不就递归了吗？(*^__^*) 但是问题是这一刀怎么切，没错，我们就来个找最大值，即 

\\[ \max_{i =1 \to n} P_i + Cut(n-i) \\]

所以，递归函数应该是：

~~~
 Cut(P, n){ //P 就是我的table，n是木头长度

  if n == 0
      return 0;

  q = -infinity;

  for i = 1 to n
      q = max(q, P[i]+Cut(P,n-i));

  return q;
}
~~~

然后，根据这个recursive写DP

~~~
Cut(P, n){
  for(int i = 1; i<=n; i++){
	q = -infinity;

	for(int j = 1; j<=i; j++){
	  q = max(q, P[j] + r[i-j]);
	}
	r[i] = q;
  }
  return r[n];
}
~~~


### 例 最长公共字串 Longest common subsequence problem  

问题描述：这个，很。。。显而易见吧，不知道的，。。。看这里 [http://en.wikipedia.org/wiki/Longest_common_subsequence_problem](http://en.wikipedia.org/wiki/Longest_common_subsequence_problem)

当然这里，我们也是要先找递归的。假设我的两个sequence，一个是X，长度为n；另一个是Y，长度为m。

现在假设我有两个pointers，一个是i，指在X的最后一个元素上，另一个是j，指在Y的最后一个元素上。我们的递归应该是分三种情况的。

1. 如果X[i] == Y[j] 那么LCS(X[i],Y[j]) = LCS(X[i-1],Y[j-1]) + 1。这个很明显，因为发现了一组公共元素，就看剩下的有多少公共元素。

2. 如果X[i] != Y[j] 那么 LCS(X[i],Y[j]) = max( LCS(X[i-1], Y[j]), LCS(X[i], Y[j-1]) )。这个其实也很容易相同，就是如果发现不同的，就去掉X或Y的最后一个，然后和另一个完整的比较，这样去掉X还是Y的最后一个，就有两种可能，所以就是要找中间max的一个。

3. 如果 i=0 或者 j=0，就return 0。因为有一个sequence已经完了。

所以递归这里还是比较明显的：

~~~
LCS(n,m){

　　if m==0 || n==0
　　　　return 0;

　　if(X[n] == Y[m])
　　　　return LCS(n-1,m-1)+1;

　　else
　　　　return max( LCS(n,m-1), LCS(n-1,m) );
}
~~~

现在有了递归，我们就应该能把它写成tabular的DP。

初始化：Table LCS的第一行第一列都设为0。

~~~
for i = 1 to m
  for j = 1 to n
	if(X[i]==Y[j])
	  LCS[i,j] = LCS[i-1,j-1]+1;
    else
	  LCS[i,j] = max(LCS[i,j-1], LCS[i-1,j] );
~~~

### 例 矩阵链相乘，求最小的乘法次数的问题

问题具体描述，看这里 [http://en.wikipedia.org/wiki/Matrix_chain_multiplication](http://en.wikipedia.org/wiki/Matrix_chain_multiplication)

先形式化一下我们的input，矩阵链\\( \\{A_1, A_2, \cdots, A_n \\} \\)，其中对于矩阵\\(A_i\\)，它是一个 $$ P_{i-1} * P_i $$ 的矩阵。m[i,j] 表示 $$ \{ A_i, A_{i+1}, \cdots, A_j \} $$相乘的最小的乘法次数。

这个递归的思路其实和第一个问题有点类似，先看怎么递归。

首先我们要找出一个点来分隔这个链，相当于这个点把这个问题转换为了 该点前一部分的矩阵链的最小的乘法次数问题和该点后一部分的矩阵链的最小的乘法次数问题。

但是这个点怎么找呢？和第一个例子一样，我们直接遍历的来找。

所以我们的递归应该是这样的：

$$ m[i,j] = \min_{i \leq k \leq j} (m[i,k] + m[k+1,j] + P_{i-1}*P_k*P_j)$$

当然，这是对于i!=j的情况，当i==j的时候呢？显然 是0了，因为我们的矩阵链就一个矩阵。 

即

~~~
Matrix-chain(i,j){

　　if(i==j)
　　　　return 0;

　　q = infinity;

　　for k = i to j
　　　　q = min(q, Matrix-chain(i,k)+Matrix-chain(k+1,j)+P_{i-1}*P_k*P_j );

　　return q;
}
~~~

现在就是把这个recursive的东西搞成DP了。算法导论上有具体的代码，这里只写个简要的。

之类就假设我们保存中间结果的是一个n*n的table m.

初始化：m的对角元素初始化为0.

~~~
for l = 2 to n
  for i=1 to n-l+1
	j = i+l-1
	m[i,j] = infinity

	for k=i to j-1
	  q = m[i,k]+m[k+1,j]+P_{i-1}*P_k*P_j;

	  if(q < m[i,j])
		m[i,j] = q;

return m
~~~

参照上面的recursive的例子，这个DP的代码应该不难理解。

=========================================

下面主要介绍一下，我们老师发明的那个方法，穷尽搜索加减枝~还是exhaust search with pruning好听 O(∩_∩)O~

这个方法的主要思想也就是首先通过构造一棵树，使得树的叶子节点成为一个可能的最终的解，换句话说也就是最后的答案一定蕴育在树的最下面一层的某个叶子节点中。很显然，一般情况下这个树还是比较好构造的，毕竟不用考虑什么条件，就是一个exhaust 展开的过程，但是随着这个树的展开，分枝越来越多，这样肯定是不make sense的，所以需要找到一些pruning rules，来修剪这棵树。其实说了半天，肯定也比较模糊，还是先看个例子吧，我觉得看完例子，在看这段话肯定比较有感觉。

### 例 最长递增字串 

问题描述：[http://en.wikipedia.org/wiki/Longest_increasing_subsequence_problem](http://en.wikipedia.org/wiki/Longest_increasing_subsequence_problem)   （其实显而易见）

假设我的一串input是 X1，X2，X3，。。。，Xn，按下图构造我们的树（enumeration tree）。

