---
layout:     post
title:      Signed Number Representation and Bitwise Operation
date:       2015-10-26 00:51:29
summary:    It has been 8 years since the first and last time I learned signed number representation. Almost forgot everything. Might be a good time to pick it up!
categories: cs 
---

## Signed Number Representation

Representing numbers is an interesting topic. Intuitively, we can represent the numbers in many different ways. However, when it comes to the digital world, in computer hardware, we need to represent numbers **ONLY** using sequences of bits (0s and 1s), **NO** extra symbols.

How to design the mechanism to **WELL** represent the numbers is not an easy task. It (at least) requires the followings:

1. The ability to represent negative numbers.
2. Algorithmic operations (plus, multiplication) can be done **efficiently**. 

There are four best-known methods in history and presence to do this job: 

* Sign-and-magnitude (原码)
* Ones' complement (反码)
* Two's complement (补码)
* Excess-K (移码)

### Sign-and-magnitude

The idea in sign-and-magnitude is pretty simple, since we need to distinguish positive number and negative number. Let's allocate one bit to **solely** indicate the sign, which is called "sign bit". All the rest are used to represent the "magnitude" of the number.

Of course, there are two problems here:

1. There are two ways to represent zero, 00000000 (0) and 10000000 (−0).
2. Since we use one bit to denote the sign, we lose some capacity to represent more numbers.

### Ones' complement

Another way to represent numbers is ones' complement. In ones' complement, the positive numbers have the same representations compared to sign-and-magnitude. The difference comes to the negative numbers. In ones' complement, we **keep the sign bit unchanged and flip all the other bits: 0 -> 1, 1 -> 0**.

Some old machines actually used ones' complement in their implementations.

### Two's complement

Two's complement is the most popular and most widely used approach to represent numbers nowadays. In two's complement, there is a unique way to represent zero and it also avoids other problems in previous approaches. 

In two's complement, it also has the sign bit, where all  positive numbers' sign bit is 0 and 1 for all negative numbers. The representation of positive numbers is same to sign-and-magnitude and ones' complement. For negative numbers, they are represented by the bit pattern which is one greater (in an unsigned sense) than the ones' complement of the positive value. 

In other words, given a negative number, we get its two's complement representation in two steps:

1. obtain the ones' complement representation of the negative number, say $$x$$.
2. add 1 to $$x$$.

For example, to represent "-1", we have 

1111 1110 -> 1111 1111


### Excess-K

Excess-K is not that popular compared to previous three methods, if you are interested in excess-K representation, please see [https://en.wikipedia.org/wiki/Offset_binary](https://en.wikipedia.org/wiki/Offset_binary).


## Bitwise Operation

### Bitwise operators

There are four major bitwise operators: 

1. NOT
2. AND
3. OR
4. XOR

where XOR means if two bits agree, it is 0; otherwise, it is 1.

### Bit shifts

We can shift the bits from left to right or right to left. When this shift meets the signed number representation, it becomes more subtle. When we talk about bit shifting, we should always ask what the signed number representation is.

In the following, let's assume we are using two's complement.

In general, left shift onces means multiple two to the original number while right shift onces means divide two to the original number.

#### Right shift (>>) in two's complement

We use the sign bit to fill all the empty positions produced by the right shift. It is an **signed shift** since we keep the sign bit during the shift, which means after the right shift, positive numbers are still positive and negative numbers are still negative.


(Let's use Java for illustration.) For example, 

~~~
int a = 5; 

System.out.println(Integer.toBinaryString(a));  // output: 101

System.out.println(a >> 1); // output: 2        
System.out.println(a >> 2); // output: 1

int b = -4;

// output: 1111 1111 1111 1111 1111 1111 1111 1100
System.out.println(Integer.toBinaryString(b));  

// output: 1111 1111 1111 1111 1111 1111 1111 1110
System.out.println(a >> 1); // output: -2  

// output: 1111 1111 1111 1111 1111 1111 1111 1110      
System.out.println(a >> 2); // output: -1
~~~


#### Left shift (<<) in two's complement 

In left shifting, we treat the sign bit as a normal bit and simply do the shift and fill zeros into the empty positions on the right. It is an **unsigned shift** since we ignore the sign bit, which means **left shift can change the sign of the numbers!** 

(Let's use Java for illustration.) For example, 

~~~
int a = 5; 

System.out.println(Integer.toBinaryString(a));  // output: 101

System.out.println(a << 1); // output: 10  (1010)    
System.out.println(a << 2); // output: 20  (10100)

int b = -4;

// output: 1111 1111 1111 1111 1111 1111 1111 1100
System.out.println(Integer.toBinaryString(b));  

// output: 1111 1111 1111 1111 1111 1111 1111 1000
System.out.println(a << 1); // output: -8  

// output: 1111 1111 1111 1111 1111 1111 1111 0000      
System.out.println(a << 2); // output: -16



int c = new BigInteger("10000000000000000000000000000001", 2).intValue();

// output: -2147483647
System.out.println(c);
 
// output: 0000 0000 0000 0000 0000 0000 0000 0010
System.out.println(Integer.toBinaryString(c << 1)); 

// output: 2
System.out.println(c << 1);
   
~~~

### Unsigned right shift in Java

As we see in the previous descriptions, right shift is a signed shift and left shift is an unsigned shift. In Java, it also provides an unsigned right shift, denoted by ">>>". This unsigned right shift works similar to left shift where the sign bit is treated as the regular bit and empty positions are filled by zeros.



~~~
int a = 20; 

System.out.println(Integer.toBinaryString(a));  // output: 10100

System.out.println(a >>> 1); // output: 10  (1010)    
System.out.println(a >>> 2); // output: 5  (101)


int c = new BigInteger("10000000000000000000000000011111", 2).intValue();

// output: -2147483617
System.out.println(c);
         
// output: 0010 0000 0000 0000 0000 0000 0000 0111
System.out.println(Integer.toBinaryString(c >>> 2)); 

// output: 536870919
System.out.println(c >>> 2); 
~~~

## Tricks 

There are commonly used tricks involving bit shift operations:

* Obtain the sign of the product or division of two integers: `boolean isNeg = (num1^num2) >>> 31 == 1;`

* Get the right most bit of an integer: `(n & 1)`


