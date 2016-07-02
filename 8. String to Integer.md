# 8. String to Integer (atoi)
##### Tags
1. String
2. Math

>Implement atoi to convert a string to an integer.
><strong>Hint: </strong>Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

><strong>Notes: </strong>It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

><strong>Requirements for atoi:</strong>
>The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

>The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

>If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

>If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

##### 题意：
实现atoi函数，将字符串转换为整数。

##### 分析：
题目很简单，就一句话，哪什么叫atoi呢？我搜索了一下，发现它是alphanumeric to integer的简称，翻译过来就是把字符串转换成整型数的意思，也就是说它代表的就是这么一个函数，那么我们需要做的就是将字符串转换成一个整数，那么涉及到的第一个问题就是数字的边界问题了，JavaScript中Number的数值范围是`-1.7976931348623157E+308`~`1.7976931348623157E+308`之间,所以不可能这么大，还好要求中明确的限定了最大最小数的范围。
第二问题就是整数是有正有负的，所以需要判断正负情况。

##### 思路：
根据上面的分析下来，思路其实已经比较清晰了：
1. 判断字符串是否有正负符号，然后定义一个变量做标记，最后根据标记再给求出的数字转换正负；
2. 设定要求中的最大最小值边界，如果越界了，要做限定；
3. 字符串都是左往右的，所以转成数字大小的时候切记反过来，字符的低位就是数字的高位。而且每位字符转成数字的条件必须满足在0~9之间

##### Js实现
##### 复杂度
时间复杂度O(n)

```
/**
 * @param {string} str
 * @return {number}
 */
let myAtoi = function(str) {

  let INT_MAX = 2147483647;
  let INT_MIN = -2147483648;
  let sign = 1,
    index = 0,
    num = 0;
  //去除空格
  str = str.trim();
  if (str.length === 0 || str === null) {
    return 0;
  }

  if (str.charAt(index) == '+') {
    index++;
  } else if (str.charAt(index) == '-') {
    sign = -1;
    index++;
  }

  while (str.length > index && str.charAt(index) >= '0' && str.charAt(index) <= '9') {
    num = num * 10 + (str.charAt(index) - '0');
    index++;
  }

  if (sign === -1) {
    num = -num;
  }
  if (num > INT_MAX) {
    return INT_MAX;
  }
  if (num < INT_MIN) {
    return INT_MIN;
  }

  return num;
};

```















