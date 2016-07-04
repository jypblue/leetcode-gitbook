# 115. Distinct Subsequences
##### Tags
1. Dynamic Programming
2. String

>Given a string S and a string T, count the number of distinct subsequences of T in S.

>A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ACE"` is a subsequence of `"ABCDE"` while `"AEC"` is not).

>Here is an example:
>S = `"rabbbit"`, T = `"rabbit"`

>Return 3.

##### 题意：
给定两个字符串S和T，求S有多少个不同的子串与T相同。
而S的子串定义为在S中任意去掉0个或者多个字符形成的串。

##### 分析：


