# 10. Regular Expression Matching
##### Tags
1. Dynamic Programming
2. Backtracking
3. String

>Implement regular expression matching with support for '.' and '*'.
>
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
>
The matching should cover the entire input string (not partial).
>
The function prototype should be:
bool isMatch(const char *s, const char *p)
>
Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

##### 题意：
实现支持 "." 和 "*" 的正则表达式匹配


##### Js实现：
##### 复杂度
时间复杂度O(n<sup>2</sup>)

```

/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
  //return matches(s, p);
    // if pattern is empty - whole string should be empty to match
  //如果模式是空的-匹配到的整个字符串也应该是空的
  if (p.length === 0) return s.length === 0;

  // retrieve 2nd character of the pattern
  //检索模式的第二个字符
  let nextChar = (p.length > 1) ? p.charAt(1) : "";
  let t = (s.length > 0) ? s.charAt(0) : 0;
  let pf = p.charAt(0);

  // if 2nd char is not '*' - it means that we are checking if next char in string matches with next char in pattern
  // and recursively run the code starting from +1 char in both pattern/string
  //
  if ("*" !== nextChar) {
    return ((t == pf) || (pf == '.' && t !== 0)) &&
      isMatch(s.substring(1), p.substring(1));
  } else {
    while ((t == pf) || (pf == '.' && t !== 0)) {
      // check if current string matches tail part of the pattern (+2 symbols)
      //检查当前S是否匹配模式的尾部（+ 2个符号）
      if (isMatch(s, p.substring(2))) return true;
      // cut first symbol in original string and repeat the check in the loop
      //在原始S中切割第一个符号并在循环中重复检查
      s = s.substring(1);
      t = (s.length > 0) ? s.charAt(0) : 0;
    }
    return isMatch(s, p.substring(2));
  }
};

```



