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
遇到这种两个串的问题，很容易想到动态规划(DP);我们先尝试做一个二维的表int[][] dp，用来记录匹配子序列的个数（以S ="rabbbit",T = "rabbit"为例）：
```
    r a b b b i t
  1 1 1 1 1 1 1 1
r 0 1 1 1 1 1 1 1
a 0 0 1 1 1 1 1 1
b 0 0 0 1 2 3 3 3
b 0 0 0 0 1 3 3 3
i 0 0 0 0 0 0 3 3
t 0 0 0 0 0 0 0 3  
```
可以看出，无论T的字符与S的字符是否匹配，dp[i][j] = dp[i][j - 1]。也就是说，假设S已经匹配了j - 1个字符，得到匹配个数为dp[i][j - 1]。现在无论S[j]是不是和T[i]匹配，匹配的个数至少是dp[i][j - 1]。除此之外，当S[j]和T[i]相等时，我们可以让S[j]和T[i]匹配，然后让S[j - 1]和T[i - 1]去匹配。所以递推关系为：

1. `dp[0][0] = 1`; // T和S都是空串.
2. `dp[0][1 ... S.length() - 1] = 1`; // T是空串，S只有一种子序列匹配。
3. `dp[1 ... T.length() - 1][0] = 0`; // S是空串，T不是空串，S没有子序列匹配。
4. `dp[i][j] = dp[i][j - 1] + (T[i - 1] == S[j - 1] ? dp[i - 1][j - 1] : 0).1 <= i <= T.length(), 1 <= j <= S.length()`

##### 思路：
经过我们细致的分析，已经推导出核心的递推关系，所以只需通过循环，根据上面的递推关系实现即可

##### Js实现：

##### 方案 #1
##### 复杂度：
时间复杂度O(m*n)

```
let numDistinct = function(s, t) {
  //如果字符串有一个为空或者长度为0，需要删除的字符为0
  if (s.length === 0 || s === null || t === null || t.length === 0) return 0;
  //新建二维数组table
  let table = [];
  for (let i = 0; i < s.length + 1; i++) {
    let row = [];
    for (let j = 0; j < t.length + 1; j++) {
      row[j] = 0;
    }
    table[i] = row;
  }
  //设定第一列的所有数字都为1
  for (let i = 0; i < s.length; i++)
    table[i][0] = 1;
  for (let i = 1; i <= s.length; i++) {
    for (let j = 1; j <= t.length; j++) {
      //如果第i-1行第j-1列的字符相等，数组table等于数组左，左上以及自己相加的值
      //如果不相等，数组左，自己相加
      if (s.charAt(i - 1) == t.charAt(j - 1)) {
        table[i][j] += table[i - 1][j] + table[i - 1][j - 1];
      } else {
        table[i][j] += table[i - 1][j];
      }
    }
  }
  return table[s.length][t.length];
};
```

##### 方案 #2
##### 复杂度
时间复杂度O(m*n)

```
let numDistinct = function(s, t) {
  if (s === null || t === null || t.length === 0 || s.length === 0) return 0;
  let dp = [];
  for (let i = 0; i < t.length; i++) {
    dp[i] = 0;
  }
  for (let i = 0; i < s.length; i++) {
    let c = s.charAt(i);
    for (let j = dp.length - 1; j >= 0; j--) {
      //s与t字符相等
      //数组累加前一个数或者加1
      if (c == t.charAt(j)) {
        dp[j] += (j !== 0 ? dp[j - 1] : 1);
      }
    }
  }
  //返回倒数第二个数
  return dp[t.length - 1];
};
```






