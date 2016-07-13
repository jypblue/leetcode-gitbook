# 321. Create Maximum Number
##### Tags
1. Dynamic Programming
2. Greedy

>Given two arrays of length m and n with digits 0-9 representing two numbers. Create the maximum number of length k <= m + n from digits of the two. The relative order of the digits from the same array must be preserved. Return an array of the k digits. You should try to optimize your time and space complexity.
>
><strong>Example 1:</strong>
>
nums1 = `[3, 4, 6, 5]`
>
nums2 = `[9, 1, 2, 5, 8, 3]`
>
k = `5`
>
return `[9, 8, 6, 5, 3]`
>
>
<strong>Example 2:</strong>
>
nums1 = `[6, 7]`
>
nums2 = `[6, 0, 4]`
>
k = `5`
>
return `[6, 7, 6, 0, 4]`
>
<strong>Example 3:</strong>
>
nums1 = `[3, 9]`
>
nums2 = `[8, 9]`
>
k = `3`
>
return `[9, 8, 9]`


##### 题意：
给定两个数组的长度m和n是数字0-9之间的两个数。创建从两个数字中的数字的最大长度K。必须保留同一个数组中的数字的相对顺序。返回k个大数字的数组。尝试优化你的时间和空间复杂度。

##### 分析：


##### 思路：

##### Js实现：
##### 复杂度：
时间复杂度O(n<sup>2</sup>)

```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[]}
 */
var maxNumber = function(nums1, nums2, k) {
  //新建目标数值的数组
  let ans = new Array(k);

  for (let i = Math.max(k - nums2.length, 0); i <= Math.min(nums1.length, k); i++) {
    let res1 = get_max_sub_array(nums1, i);
    let res2 = get_max_sub_array(nums2, k - i);
    let res = new Array(k);
    let pos1 = 0,
      pos2 = 0,
      tpos = 0;

    while (pos1 < res1.length || pos2 < res2.length) {
      res[tpos++] = greater(res1, pos1, res2, pos2) ? res1[pos1++] : res2[pos2++];
    }

    if (!greater(ans, 0, res, 0))
      ans = res;
  }

  return ans;
};

function greater(nums1, start1, nums2, start2) {
  for (; start1 < nums1.length && start2 < nums2.length; start1++, start2++) {
    if (nums1[start1] > nums2[start2]) return true;
    if (nums1[start1] < nums2[start2]) return false;
  }
  return start1 != nums1.length;
}

function get_max_sub_array(nums, k) {
  let res = new Array(k);
  let len = 0;
  for (let i = 0; i < nums.length; i++) {
    while (len > 0 && len + nums.length - i > k && res[len - 1] < nums[i]) {
      len--;
    }
    if (len < k)
      res[len++] = nums[i];
  }
  return res;
}
```
