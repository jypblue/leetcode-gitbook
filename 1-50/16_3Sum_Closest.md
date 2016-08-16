# 16. 3Sum Closest
##### Tags
1. Array
2. Two Pointers

>Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>```
 For example, given array S = {-1 2 1 -4}, and target = 1.
>
 The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

##### 题意：
给定一个拥有n个整数的数组S，找到数组S中的3个整数之和最接近给定的一个数字target。返回这三个整数数字的和。请你确保每次输入都只有一个结果。

##### 分析：
本题跟题15有相似的地方，从题意中来讲,我们只需比较三个数相加的和与目标数字的差值最小即可。思路一样的是遍历每个数，对剩余数组进行双指针扫描。区别仅在于当：
sum = A[left] + A[right]

1. sum = target时直接返回
2. sum != target时，在相应移动left/right指针之前，先计算abs(sum-target)的值，并更新结果，直到最小值时再返回。

##### 思路：
1. 先升序排序
2. 遍历数组，固定一个元素，对其后的元素采用双指针扫描。
3. 若距离更小，更新距离与三个数之和(直到最小返回sum值,如果距离为0，则直接返回)。
4. 否则，移动头指针或尾指针


##### Js实现：
##### 复杂度
时间复杂度O(n<sup>2</sup>)

```
/** 
* @param {number[]} nums 
* @param {number} target 
* @return {number} 
*/

var threeSumClosest = function(nums, target) { 
  let result = 0; let min = 2147483647; 
    switch (nums.length) {   
      case 0:     
        return 0;   
      case 1:     
        return nums[0];   
      case 2:     
        return nums[0] + nums[1];
    }
    nums.sort(function(a, b) { return a - b; });
    for (let i = 0; i < nums.length; i++) { 
      let j = i + 1; let k = nums.length - 1; 
        while (j < k) { 
          let sum = nums[i] + nums[j] + nums[k]; 
          let diff = Math.abs(sum - target);
          if (diff === 0) return sum;
          if (diff < min) { min = diff; result = sum; } 
          if (sum <= target) { 
            j++;
          } else { 
            k--; 
          } 
        } 
      }
   return result;
};
```