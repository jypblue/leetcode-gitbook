# 14. Longest Common Prefix
##### Tags
1. String

>Write a function to find the longest common prefix string amongst an array of strings.

##### 题意：
写一个查找字符串数组中最长公共前缀字符串的函数

##### 分析：
又是字符串问题，又是公共。那方法就很简单咯，就是将数组中的每个字符串两两对比每个字符串的每个字符，返回公共的子字符串即可。

##### 思路：
1. 以数组中的某个字符串为基准；
2. 循环比较两个字符串中的每个字符，找到最长公共前缀字符串，然后把位置记录下来，将基准字符串按此截掉，留下公共部分；
3. 直到数组中的每个字符串都与基准字符串比较完毕为止，返回公共子串

##### JS实现：
##### 复杂度
时间复杂度O(n<sup>2</sup>)

##### 方法 #1 以第一个字串为基准字符串

```
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
    if(strs ===null || strs.length ===0) {
        return "";
    }
    let prefix = strs[0];
    for(let i = 0; i < strs.length; i++){
        let j = 0;
        while(j < strs[i].length && j < prefix.length && strs[i].charAt(j)===prefix.charAt(j)){
            j++;
        }
        if(j===0) {
            return "";
        }
        prefix = prefix.substring(0,j);
    }
    return prefix;
};


```

##### 方法 #2 找数组中最短字符串为基准循环

```
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
    if(strs ===null || strs.length ===0) {
        return "";
    }   
    if(strs.length === 1) {
         return strs[0];
    }  
    let minlen = strs.length + 1;  
    for(let str of strs) {
        if(minlen > str.length) {
            minlen = str.length;
        }
    }
    for(let i = 0; i < minlen;i++){
        for(let j = 0; j < strs.length - 1;j++){
            let str1 = strs[j];
            let str2 = strs[j+1];
            if(str1.charAt(i) !== str2.charAt(i)) {
               return str1.substring(0,i);
            }
        }
    }
    return strs[0].substring(0,minlen);
};


```