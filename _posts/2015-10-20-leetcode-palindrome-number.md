---
layout:     post
title:      LeetCode - Palindrome Number
date:       2015-10-20 23:27:02
summary:    Determine whether an integer is a palindrome. Do this without extra space.
categories: leetcode
---

### Determine whether an integer is a palindrome. Do this without extra space. [Link](https://leetcode.com/problems/palindrome-number/)



~~~
public class Solution {
    public boolean isPalindrome(int x) {
        
        if (x < 0) {
            return false;
        }
        
        if (x == 0) {
            return true;
        }
        
        // indirectly obtain the number of digits of x
        int base = 1;
        int tmp = x;
        while (tmp >= 10) {
            tmp = tmp / 10;
            base *= 10;
        }
        
        boolean result = true;
        // start to check if the first and last digits are the same
        while(x != 0) {
            
            int lastDigit = x % 10;
            int firstDigit = x / base;
            
            if (firstDigit != lastDigit) {
                result = false;
                break;
            }
            
            x = x % base;
            x = x / 10;
            
            base = base / 100;
            
            
        }
        
        return result;
    }
}
~~~