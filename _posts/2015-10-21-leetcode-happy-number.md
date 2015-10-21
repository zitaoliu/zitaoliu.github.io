---
layout:     post
title:      LeetCode - Happy Number
date:       2015-10-21 13:51:02
summary:    Write an algorithm to determine if a number is "happy".
categories: leetcode
---

### Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: 

Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

[Link](https://leetcode.com/problems/happy-number/)


~~~
public class Solution {
    public boolean isHappy(int n) {
        
        if (n <= 0) {
            return false;
        }
        
        if (n == 1) {
            return true;
        }
        
        boolean result = true;
        HashSet<Integer> set = new HashSet<Integer>();
        
        while (true) {
            
            n = computeHappyNum(n);
            if (n == 1) {
                break;
            } else {
                if (set.contains(n)) {
                    result = false;
                    break;
                } else {
                    set.add(n);
                }
            }
        }
        
        return result;
    }
    
    public int computeHappyNum(int num) {
        
        int happyNum = 0;
        
        while( num > 0) {
            
            int tmp = num % 10;
            happyNum += tmp * tmp;
            num = num / 10;
        }
        
        return happyNum;
    }
}
~~~