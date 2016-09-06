# 17. Letter Combinations of a Phone Number 
##### Tags
1. Backtracking
2. String

>Given a digit string, return all possible letter combinations that the number could represent.
>
>A mapping of digit to letters (just like on the telephone buttons) is given below.
>
>```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
><strong>Note:</strong>
>
Although the above answer is in lexicographical order, your answer could be in any order you want.

##### 题意：
给定一个数字字符串，返回数字可能代表的所有可能的字母组合。一个数字映射到字母（就像在电话按钮上）是下面给出的。

##### 分析：
根据题意，以及实例。可以看出输入的数字字符串就是选定电话键盘号码中对应的英文字母集合字符串，输出的是所有可能的字母组合。可以看出，输入的数字字符串，决定了组合的字母，然后再把字母相互组合即可。由此我们可以通过输入数字字符串确定字符串，再通过递归将所有可能的字母组合起来。

##### 思路:
1. 定义电话键盘字母字符串数组
2. 传入数字字符串和起始位置
3. 循环组合数字字符串对应的电话键盘字符串中的字母，知道位置idx与数字字符长度一致时停止，然后返回最后的结果数组

##### Js实现：
##### 复杂度
时间复杂度O(n<sup>2</sup>)

```
/** * @param {string} digits * @return {string[]} */

const digitStr = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"];
let result = [];
let tmp = "";
var letterCombinations = function(digits) {
  result = [];
  if (digits.length === 0) return result;
  dfs(digits, 0);
  return result;
};

function dfs(digits, idx) {
 //递归结束条件
 if (idx == digits.length) {
   result.push(tmp);
   return;
 }
 for (let i = 0; i < digitStr[digits[idx]].length; i++) {
   //回溯！
   tmp = tmp.substr(0, idx);
   tmp += (digitStr[digits[idx]])[i];
   dfs(digits, idx + 1);  
 }
}

```



