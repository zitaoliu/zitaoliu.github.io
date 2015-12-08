---
layout:     post
title:      Binomial Coefficient Basics 
date:       2015-12-07 18:07:29
summary:    Let's QUICKLY go over the basics of binomial coefficient.
categories: cs 
---


## Binomial Coefficient

The majority content in the following can be found in wikipedia [https://en.wikipedia.org/wiki/Binomial_coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient). Here I would like to highlight some key "basics" concisely.

### Definition

$$(x + y)^n = \Sigma_{k=0}^n \binom{n}{k} x^{n-k}y^k$$

### Recursive Formula (Pascal's rule)

$$\binom{n}{k} = \binom{n-1}{k}+ \binom{n-1}{k-1}$$


### Multiplicative Formula

$$\binom{n}{k} = \prod_{i=1}^k \frac{n+1-i}{i}$$

### Factorial Formula

$$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$

### Pascal's Triangle (杨辉三角)


0:									1								

1:								1		1							

2:							1		2		1						

3:						1		3		3		1					

4:					1		4		6		4		1				

5:				1		5		10		10		5		1			

6:			1		6		15		20		15		6		1		

7:		1 		7 		21		35		35		21		7 		1 	

8:	1 		8 		28		56		70		56		28		8 		1 

Row number $$n$$ contains the numbers $$\binom{n}{k}$$ for $$k = 0, \cdots, n$$. It is constructed by starting with ones at the outside and then always adding two adjacent numbers and writing the sum directly underneath. **This method allows the quick calculation of binomial coefficients without the need for fractions or multiplications**.


### Compute Binomial Coefficient via Programming Languages

1. Using Recursive Formula 
	1. Recursive implementation 
	2. Iterative implementation (DP) [http://www.brpreiss.com/books/opus5/html/page460.html](http://www.brpreiss.com/books/opus5/html/page460.html)
2. Using Multiplicative Formula
3. Using Factorial Formula



