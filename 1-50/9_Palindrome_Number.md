# 9. Palindrome Number
##### Tags
1. Math

>Determine whether an integer is a palindrome. Do this without extra space.
>
><strong>Some hints:</strong>
>
Could negative integers be palindromes? (ie, -1)
>
>If you are thinking of converting the integer to string, note the restriction of using extra space.
>
>You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?
>
>There is a more generic way of solving this problem.

##### 题意：
判断一个整数是否是回文，不能使用额外空间

##### 分析：
此题与题7.Reverse Integer 类似，做法也类似，都是将数字反向颠倒过来比较是否相等即可。

##### 思路：
1. 取传入数字的绝对值，反向颠倒（注：负数不是回文）
2. 比较跟原值是否相等，相等就是回文，不等就不是

##### Js实现：
##### 复杂度
时间复杂度O(n)

```
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    let res = 0;
    let abs = Math.abs(x); 
    while(abs !== 0) {
        res = res*10 + abs % 10;
        abs = Math.floor(abs / 10);
    }
    return res===x;
};
```













