# 11. Container With Most Water 
##### Tags
1. Array
2. Two Pointers

>Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
>
>Note: You may not slant the container.

##### 题意
给定n个非负整数 a1, a2, ..., an,每个整数代表在坐标（i,ai）上的一个点。n条垂直线条被画在了两个端点为（i,ai）和（i,0）的线条i上。
找到两条线段，把它们拼成一个容器，而这个容器可以盛最多的水。

##### 分析
我们最初可以假设拼成的容器容积为0，然后我们可以从两侧开始扫描。
如果leftheight < rightheight，向右移动，找到一个值是大于leftheight；同样的，如果leftheight > rightheight，向左移动，找到一个值是大于rightheight。
此外，还要保持跟踪的是最大值。

##### 思路



