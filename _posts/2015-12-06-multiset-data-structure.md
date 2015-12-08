---
layout:     post
title:      Multiset 
date:       2015-12-06 17:55:29
summary:    A multiset (or bag) is a generalization of the concept of a set that, unlike a set, allows multiple instances of the multiset's elements. 
categories: cs 
---

In mathematics, a multiset (or bag) is a generalization of the concept of a set that, unlike a set, allows multiple instances of the multiset's elements.

A multiset is similar to the set concept but with extra relaxation: allowing duplicate elements.  For example, {a, a, b} is not a valid set but is a multiset. 

Usually, for each element, we keep not only the value of the element itself, but also the occurrence of the element. For example, a multiset like {a, a, b} is usually stored as {a:2, b:1}.

Google's Guava has the implementation for multiseet ready to use. [https://github.com/google/guava](https://github.com/google/guava)

The implementation is straight forward and has the same idea with what I mentioned above.


