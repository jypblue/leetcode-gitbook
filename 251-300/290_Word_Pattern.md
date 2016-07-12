# 290. Word Pattern
##### Tags
1. Hash Table

>Given a pattern and a string str, find if str follows the same pattern.
>
>Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.
>
<strong>Examples:</strong>
```
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
```
><strong>Notes:</strong>
>
>You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.


##### 题意：
给定一个模式和一个字符串，如果发现字符串遵循相同的模式，返回true,不相同则返回false。

##### 分析：

##### 思路：

##### Js实现：


##### 方法 #1
##### 复杂度：

```
/**
 * @param {string} pattern
 * @param {string} str
 * @return {boolean}
 */
let wordPattern = function(pattern, str) {
    let strArr = str.split(" ");
    let mapPattern = new Map();
    let mapStr = new Map();
    
    if(strArr.length !== pattern.length){
        return false;
    }
    
    for(let i = 0; i < strArr.length; i++) {
      mapPattern.set(pattern.charAt(i),i);
      mapStr.set(strArr[i],i);
    }
    //第一种解法108-120ms
    for(let i = 0; i < strArr.length; i++) {
        if(mapStr.get(strArr[i]) !== mapPattern.get(pattern.charAt(i))) {
          return false;
        }
    }
    return true;
};

```