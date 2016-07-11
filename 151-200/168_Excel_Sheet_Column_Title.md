# 168. Excel Sheet Column Title
##### Tags:
1. Math

>Given a positive integer, return its corresponding column title as appear in an Excel sheet.

>For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

##### 题意：
给定一个正整数，就如同出现在一个表格中那样返回其对应的列标题。

##### 分析：
本题很简单，说白了就是将数字转换为英文字符，javascript中也有对应的函数String.fromCodePoint(),因此直接转换就可以了。

##### 思路：
