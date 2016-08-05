# 100. Same Tree
##### Tags
1. Tree
2. Depth-first Search

>Given two binary trees, write a function to check if they are equal or not.
>
>Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

##### 题意：
给两棵树，写一个函数来判断这两棵树是否相同. 判定树是否相同的条件为这两棵树的结构相同，并且每个节点的值相同.

##### 分析：
题目很简单，直接利用DFS遍历比较两棵树即可

##### 思路：
1. 判断树是否为null
2. DFS判断val是否相等，左右节点是否一致

##### 复杂度：
时间复杂度O(n)

##### Js实现：
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if(p === null && q === null) {
            return true;
        } else if(p === null || q === null) {
            return false;
        }

        let isLeftSame = isSameTree(p.left, q.left);
        let isRightSame = isSameTree(p.right, q.right);

        return p.val==q.val && isLeftSame && isRightSame;
};
```