# 13. Roman to Integer
##### Tags
1. Math
2. String

>Given a roman numeral, convert it to an integer.
>
>Input is guaranteed to be within the range from 1 to 3999.

##### 题意：
给定一个罗马数字，将它转换为一个阿拉伯数字整数

##### 分析：
这一题，与上一题<a href="https://jypblue.gitbooks.io/leetcode/content/1-50/12_Integer_to_Roman.html" target="_blank">12.Integer to Roman</a>相反；其实基本思路差不多，但是因为涉及到字符串，所以有细小的区别。
所以罗马数字分析请见上一题。

##### 思路：
从第一个字符开始，如果当前字符对应的数字比下一个数字大，那么就把结果加上当前字符对应的数字，否则减去当前字符对应数字。注意边界情况，所以在原字符串最后添加一个字符，该字符是原来的最后一个字符。

##### Js实现：
##### 复杂度
时间复杂度O(n)

```
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
 // let map = new Map();
 // map.set('I',1);
 // map.set('V',5);
 // map.set('X',10);
 // map.set('L',50);
 // map.set('C',100);
 // map.set('D',500);
 // map.set('M',1000);

  var map = {};
  map['I'] = 1;
  map['V'] = 5;
  map['X'] = 10;
  map['L'] = 50;
  map['C'] = 100;
  map['D'] = 500;
  map['M'] = 1000;

  let res = 0, n = s.length;
  s +=s[n-1];
  for(let i = 0; i < n; i++) {
    if(map[s[i]] >= map[s[i+1]]) {
      res += map[s[i]];
    } else {
      res -= map[s[i]];
    }  
  }
  return res;
};

```
