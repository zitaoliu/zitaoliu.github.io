---
layout:     post
title:      Minimum Knowledge Set
date:       2010-10-17 11:21:29
summary:    今天我没吃药，犯神经了，我想来讲讲Minimum Knowledge Set。
categories: cs general
---

某天突然想到一个概念：最小知识集合 **Minimum Knowledge Set(MKS)**. 回来google了一番，没有找到自己想要的答案。

我理想中的MKS应该是given一个research topic，存在一个MKS与之相对应。MKS里包括了精通这个research topic的所有知识。很显然，这是一个set。而这种set是infinite的，当然我们care的是最小知识集合 Minimum Knowledge Set(MKS). 不知道是谁好像说过，当你在XXX领域一直持续研究5-6年之后，你就自然而然的成为了这个领域的expert。其实换句话说，也就是你掌握了这个领域的Minimum Knowledge Set。

当然，这只是对MKS的一个简单的描述，抽象成定义不是难事，略显无聊，略去。。。

当然上面的对MKS的描述同时也是不准确的，因为首先要解决的问题是 MKS是否always存在。要证明MKS的存在性，就要go back到MKS的定义或描述，可惜定义或描述又不准确，貌似陷入了chicken-egg problem，所以暂且假设 MKS存在。

MKS是一个set，所以人们自然会问这样的问题：

1. what's the boundary of MKS?
2. is MKS closed or open?
3. is MKS bounded?
4. is MKS compact?

....

首先对于MKS的boundary，我觉得是一个模糊的概念，MKS里的每一个元素都在它的boundary，同时有在它的interior里。同时很显然，MKS是closed的。如果MKS存在，我相信他是bounded的，一个closed和bounded的set，它是compact的。除了这些set的基本性质，我们可能会更想dig一下，MKS有没有更interesting的properties。第一个想到的就是convexity。MKS是一个convex set么？MKS的convex hull interesting吗？鉴于MKS较为抽象，所以我们也要把linear combination抽象了才能在同一个层次上考虑MKS的convexity。对于MKS里面的元素，他们的linear combination是什么呢？

暂时还木有想出来，待续。。。
