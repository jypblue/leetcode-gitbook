# 171. Excel Sheet Column Number
##### Tags
1. Math

>Related to question <a href="https://jypblue.gitbooks.io/leetcode/content/151-200/168_Excel_Sheet_Column_Title.html">Excel Sheet Column Title </a>

>Given a column title as appear in an Excel sheet, return its corresponding column number.

>For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

##### 题意：
给出一个在表格中显示的列的标题，返回其对应的列的数值号码

##### 分析：
本题就是 <a href="https://jypblue.gitbooks.io/leetcode/content/151-200/168_Excel_Sheet_Column_Title.html">168. Excel Sheet Column Title </a> 反向，将168的做法反过来即可，而且javascript中有codePointAt()方法将英文字符转化为数字，所以此题做起来也很简单。

##### 思路：
1. 循环截取字符串中的每个字符将其转换为数字
2. 按照数字和大写英文字符的对应规律关系，算出最后的数字，然后累加

##### Js实现：
##### 复杂度
时间复杂度O(n)

```
/**
 * @param {string} s
 * @return {number}
 */
var titleToNumber = function(s) {
    let result = 0;
    let i = s.length - 1;
    let t = 0;
    while(i >= 0){
        let curr = s.codePointAt(i).toString(10);
        result = result+Math.pow(26, t)*(curr-65 + 1);
        t++;
        i--;
    }
 
    return result;
};
```