---
layout:     post
title:      Matlab编程规范(MATLAB Programming Style Guidelines)
date:       2011-09-28 11:21:29
summary:    Matlab编程规范，自己总结的，主要是参考了下面这篇文章 “MATLAB Programming Style Guidelines”。
categories: cs coding
---


主要是参考了下面这篇文章，简洁总结在这里。

[MATLAB Programming Style Guidelines](http://www.datatool.com/downloads/matlab_style_guidelines.pdf)

简洁总结如下：

1. 表示object的数量的时候，用n做前缀，如 nFiles。
2. 因为matlab里提到矩阵都是说m*n的矩阵，所以用mRows表示矩阵的行数，算是上面一条的一个特例吧。
3. 用i做前缀表示iterator variable，如iFile。 for iFile = 1:nFiles ... end。
4. 嵌套循环的话，iterator variable按字母顺序使用。如 i, j, k, l, m, n...。
5. 常量可以用一个通用的类型名作前缀，如 COLOR_RED, COLOR_GREEN, COLOR_BLUE。
6. 结构命名第一个字母大写。
7. 函数的命名驼峰和下划线分隔的都行，一致就好。
8. 只有一个返回值的函数的用它的返回值含义命名，如 mean()。
9. 没有返回值的函数用它具体做的事情命名，如plot()。
10. 用于计算某个东西的函数用compute作为前缀。
11.用于查找某个东西的函数用find作为前缀。
12.用于初始化的函数用initialize作为前缀。
13. 返回值是布尔值的函数用is作为前缀。
14. 如果一个函数只被一个m文件里的函数调用，这个函数不用单独写成一个m文件，直接定义在那个调用它的函数文件里就好。
15. 文件中所有重要变量的注释全部放在文件的开头。
16. 常量的赋值注释现在那句赋值语句的后面。
17. 避免复杂的条件判断，用单独的布尔变量分隔。
18. 每一行的代码尽量不要超过80个column的长度。
19. 简单的if, for, while语句可以写在一行，如 if(condition), statement; end。
20. 函数开头的注释应该支持 help和lookfor。
21. 最后讲Documentation的时候，引用了Dick Brandon的话

>"Documentation is like sex; when it's good, it's very, very good, and when it's bad, it's better than nothing."
