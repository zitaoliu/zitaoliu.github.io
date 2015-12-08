---
layout:     post
title:      Introduction to Catalan Number and Its Relevant Programming Interview Questions
date:       2015-12-08 15:07:29
summary:    Catalan number sequence is an interesting natural number sequences that have nice properties and lots of programming interview questions can be viewed as finding the Catalan numbers.
categories: cs interview 
---

## Catalan numbers [https://en.wikipedia.org/wiki/Catalan_number](https://en.wikipedia.org/wiki/Catalan_number)

In combinatorial mathematics, the Catalan numbers form a sequence of natural numbers that occur in various counting problems, often involving recursively-defined objects. They are named after the Belgian mathematician [Eugène Charles Catalan](https://en.wikipedia.org/wiki/Eug%C3%A8ne_Charles_Catalan) (1814–1894).

There are a couple of equivlant descriptive definitions about Catalan number sequences:

1. $$C_n = \frac{1}{n+1} \binom{2n}{n} = \prod_{k=2}^n \frac{n+k}{k}$$

2. $$C_n = \binom{2n}{n} - \binom{2n}{n+1}$$

3. $$C_{n+1} = \sum_{i=0}$$