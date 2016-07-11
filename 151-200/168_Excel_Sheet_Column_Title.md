# 168. Excel Sheet Column Title
##### Tags
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
1. 有26个字母，数字与字母一一对应
2. 直接26求余，再将数字转变成字符，直到除尽为止

##### Js实现：
##### 复杂度：
时间复杂度O(n)

```
/**
 * @param {number} n
 * @return {string}
 */
let convertToTitle = function(n) {
    let ctArr = [];
     while(n > 0){
        n--;
        let ch = String.fromCodePoint(n % 26 + 65);
        n = Math.floor(n/26);
        ctArr.push(ch);
    }
 
    ctArr.reverse();
    return ctArr.join('');
}
```