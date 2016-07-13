# 330. Patching Array
##### Tags
1. Greedy

>Given a sorted positive integer array nums and an integer n, add/patch elements to the array such that any number in range [1, n] inclusive can be formed by the sum of some elements in the array. Return the minimum number of patches required.
>
><strong>Example 1:</strong>
>
>nums = [1, 3], n = 6
>
>Return 1.
>
>Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
>
>Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
>
>Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
>
>So we only need 1 patch.
>
><strong>Example 2:</strong>
>
>nums = [1, 5, 10], n = 20
>
>Return 2.
>
>The two patches can be [2, 4].
>
><strong>Example 3:</strong>
>
>nums = [1, 2, 2], n = 5
>
>Return 0.

##### 题意：
给定一个正整数数组排序数组和一个整数n，添加/补丁元素的数组，例如，任何数量在范围[ 1，n ]，包含可以通过数组中的一些元素的和形成。返回所需的最小数量的数字。

##### 分析：
1. 给定一个正整数数组排序数组和一个整数n，添加/补丁元素的数组，例如，任何数量在范围[ 1，n ]
2. 包含可以通过数组中的一些元素的和形成。返回所需的最小数量的数字。让错过成为数组中元素的总和不能形成的最小的数字。
3. 在[ 0，miss)的所有元素都可以形成。错过值开始于1。下一个数 nums[i]<=miss，然后边增加到[ 0，miss+nums[i]），
4. 因为所有的边界之间的数字可以形成；如果下一个nums[i] > miss，这意味着有一个差距，我们需要插入一个数字，
5. 插入miss本身是一个选择，因为它的边界双打和覆盖每一个数字之间的界限[ 0，miss+miss]

##### 思路：
思路很简单:
1. 当miss < n 时，循环数组；
2. 如果nums[i] <= miss; nums[i]累加到miss中；
3. 如果nums[i] > miss; miss累加miss,count自增

##### Js实现：
##### 复杂度：
时间复杂度O(n)

```
/**
 * @param {number[]} nums
 * @param {number} n
 * @return {number}
 */
let minPatches = function(nums, n) {
  let miss = 1;
  let count = 0;
  let i = 0;
  while (miss <= n) {
    //数组nums的长度，以及nums数字小于初始目标数字
    if (i < nums.length && nums[i] <= miss) {
      miss = miss + nums[i];
      i++;
    } else {
      miss += miss;
      count++;
    }
  }
  return count;
};
```











