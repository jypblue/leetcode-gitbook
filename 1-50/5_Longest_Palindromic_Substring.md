# 5. Longest Palindromic Substring 
##### Tags
1. String

>Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

##### 题意：
给定一个字符串S，找到字符串S中最长的回文子字符串。也许你可能认为S的最大长度是1000，就会存在一个独特的最长的回文子串。

##### 分析：
题目要求是找字符串的最长回文子串，然后返回这个回文子串,提取关键信息点：
1. 回文子串 => 回文判断
2. 最长子串 => 截取可能最长子串

##### 思路：
根据提取关键信息点，最基本的思路就是：
1. 循环依次截取每种子串
2. 依次判断每种子串是否是回文子串
3. 比较子串长度，将最长的返回

##### Js实现：

##### 方法 #1 暴力算法
##### 复杂度：
时间复杂度O(n<sup>3</sup>),肯定Time Limit Exceeded,所以放弃，不过还是贴一下实现代码。
```
let longestPalindrome = function(s) {
    let maxLength = 0;
    let maxStart = 0;
    let len = s.length;
    //i是字符串长度
    for(let i = 0; i < len; i++){
        //j是字符串起始位置
        for(let j = 0; j < len - i; j++){
            //挨个判断是否回文
            if(isPalindrome(s,i,j) && (i+1)>maxLength){
                maxLength = i + 1;
                maxStart = j;
            }
        }
    }
    return s.substring(maxStart,maxStart + maxLength);
}

function isPalindrome(s, i, j){
    let left = j;
    let right = j + i;
    while(left<right){
        if(s.charAt(left)!=s.charAt(right)){
            return false;
        }
        left++;
        right--;
    }
    return true;
}

```

##### 方法 #2
方法#1不行，于是又想到了像动态规划那样找规律来节省时间复杂度，以`aaabaaaa`为例我发现的规律如下：
```
  a a a b a a a a
a 1 1 1 0 1 1 1 1
a 1 1 1 0 1 1 1 1
a 1 1 1 0 1 1 1 1
b 0 0 0 1 0 0 0 0
a 1 1 1 0 1 1 1 1
a 1 1 1 0 1 1 1 1
a 1 1 1 0 1 1 1 1
a 1 1 1 0 1 1 1 1
```

我发现以b为中心点，两边等距延展划线，匹配的最长回文子字符串是倒过来的斜向上那条。

##### 复杂度
时间复杂度O(n<sup>2</sup>)
```
 var longestPalindrome = function(s) {
    if(s===null || s.length<=1)  return s;
    
    let longest = s.substring(0, 1);
	for (let i = 0; i < s.length; i++) {
		//奇数个的时候以i为中心点
        //判断字符串长短，取长的留下
		let tmp = helper(s, i, i);
		if (tmp.length > longest.length) {
			longest = tmp;
		}
 
		//偶数个的时候以 i, i+1为中心点
        //判断字符串长短，取长的留下
		tmp = helper(s, i, i + 1);
		if (tmp.length > longest.length) {
			longest = tmp;
		}
	}
 
	return longest;
};
//以中心点为中心，左右逐渐外延，返回找到的满足回文的子字符串
function helper(s, begin, end) {
	while (begin >= 0 && end <= s.length - 1 && s.charAt(begin) == s.charAt(end)) {
		begin--;
		end++;
	}
	return s.substring(begin + 1, end);
}
```

##### 方法 #3
##### 复杂度
时间复杂度O(n)

最后补充一个谷歌发现的最强算法实现，算法地址链接是 <a href="http://articles.leetcode.com/longest-palindromic-substring-part-ii">http://articles.leetcode.com/longest-palindromic-substring-part-ii</a> ; 在此基础上改写成了JavaScript版本.

```
let longestPalindrome = function(s) {
  let T = preProcess(s);
  let n = T.length;
  let P = new Array(n);
  let C = 0,
    R = 0;
  for (let i = 1; i < n - 1; i++) {
    let i_mirror = 2 * C - i; // equals to i' = C - (i-C)

    P[i] = (R > i) ? Math.min(R - i, P[i_mirror]) : 0;

    // Attempt to expand palindrome centered at i
    while (T[i + 1 + P[i]] == T[i - 1 - P[i]])
      P[i]++;

    // If palindrome centered at i expand past R,
    // adjust center based on expanded palindrome.
    if (i + P[i] > R) {
      C = i;
      R = i + P[i];
    }
  }

  // Find the maximum element in P.
  let maxLen = 0;
  let centerIndex = 0;
  for (let i = 1; i < n - 1; i++) {
    if (P[i] > maxLen) {
      maxLen = P[i];
      centerIndex = i;
    }
  }
  P = [];

  return s.substr((centerIndex - 1 - maxLen) / 2, maxLen);
}

// Transform S into T.
// For example, S = "abba", T = "^#a#b#b#a#$".
// ^ and $ signs are sentinels appended to each end to avoid bounds checking
function preProcess(s) {
  let n = s.length;
  if (n === 0) return "^$";
  let ret = "^";
  for (let i = 0; i < n; i++)
    ret += "#" + s.substr(i, 1);

  ret += "#$";
  return ret;
}

```



















