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