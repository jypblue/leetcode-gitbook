# 152. Maximum Product Subarray
##### Tags
1. Array
2. Dynamic Programming

>Find the contiguous subarray within an array (containing at least one number) which has the largest product.

>For example, given the array `[2,3,-2,4]`,
the contiguous subarray `[2,3]` has the largest product = `6`.

>Subscribe to see which companies asked this question

##### 题意：
在数组中找到子阵（至少包含一个数字）数字的最大乘积

##### 分析：
根据题目提示可以发现，数字有正有负。当乘数中都为正数的时候,数值越大，乘积越大；当乘数中为负数的时候，数值越小，乘积越大。

##### 思路：
1. 新建两个数组max和min,分别临时存储数组中连着的两个数的乘积，最大值，最小值。
2. 数组循环，数字前后冒泡比较
3. 当数为正的时候，数值乘积越大，越大；反之，当数为负的时候，数值乘积越大，越小。

##### Js实现：
##### 复杂度：
时间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @return {number}
 */
let maxProduct = function(nums) {
    let max = [],min = [],
     result = nums[0];
     max[0] = min[0] = nums[0];
     
    for(let i = 1; i < nums.length; i++) {
        
        if(nums[i] > 0) {
            max[i] = Math.max(nums[i],max[i-1]*nums[i]);
            min[i] = Math.min(nums[i],min[i-1]*nums[i]);
        } else {
            max[i] = Math.max(nums[i],min[i-1]*nums[i]);
            min[i] = Math.min(nums[i],max[i-1]*nums[i]);
        }
        
        result = Math.max(result,max[i]);
    }
    return result;
};
```