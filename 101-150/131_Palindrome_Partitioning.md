# 131. Palindrome Partitioning
##### Tags
1. Backtracking

>Given a string s, partition s such that every substring of the partition is a palindrome.

>Return all possible palindrome partitioning of s.

>For example, given s = `"aab"`,
>Return
>```
[
  ["aa","b"],
  ["a","a","b"]
]
```

##### 题意：
给定一个字符串s，将字符串s进行分解，分解的子字符串都是回文，返回s中所有可能的回文划分。

##### 分析：
本题跟77. Combinations题很类似,总体方法基本一致。对于给定字符串用DFS层层遍历，唯一的区别在于本题多了一个回文的判断。

##### 思路：
1. 主体思路见[ 77. Combinations ](51-100/77. Combinations.md)
2. 回文判断（就是比较字符串中的首尾对应字符是否一致）

##### Js实现：

##### 方法 #1 DFS
##### 复杂度：
时间复杂度O(n!)
```
/**
 * [partition description]
 * @param  {[type]} s [传入的字符串]
 * @return {[type]}   [返回所有可能的回文结构子字符串划分数组]
 */
let partition = function(s) {
  let result = [];
  let partition = [];
  if (s === null || s.length === 0) return result;

  addPalindrome(s, 0, partition, result);
  return result;
};
function addPalindrome(s, start, partition, result) {
  if (start === s.length) {
    //因为partition会不断改变，所以temp只保存符合条件的数组值，
    //如果直接=是js引用,temp会根据partition的变化而变化，
    //因此要以js赋值的写法写
    let temp = [].concat(partition);
    result.push(temp);
    return;
  }
  for (let i = start + 1; i <= s.length; i++) {
    //循环截取字符串
    let str = s.substring(start, i);
    //判断是否是回文，如果是，存入临时数组partition中，递归调用addPalindrome函数，将符合条件的数组添加给result
    if (isPalindrome(str)) {
      partition.push(str);
      //当i<=3 的时候递归调用addPalindrome
      //1:1,2,3
      //2:2,3
      //3=3直接跳过
      addPalindrome(s, i, partition, result);
      partition.splice(partition.length - 1, 1);
    }
  }
}
//判断字符串是否是回文
function isPalindrome(str) {
  let left = 0;
  let right = str.length - 1;
  while (left < right) {
    if (str.charAt(left) != str.charAt(right)) {
      return false;
    }
    left++;
    right--;
  }
  return true;
}
```

##### 方法 #2 动态规划


