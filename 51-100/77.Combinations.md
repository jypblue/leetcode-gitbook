# 77. Combinations
##### Tags
1. Backtracking

>Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

>For example,
>
>If n = 4 and k = 2, a solution is:
>```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
>```

##### 题意：
给定两个整数n和k，返回1...n之间所有k个数可能的组合.

##### 分析：
根据题意，我们可以获取到几个关键的信息：
1. 组合是介于1~n之间的，最小最大值是1和n；
2. 组合数组个数等于k，k<n;
3. 求出满足条件的所有组合。注：[2,3][3,2]是同一种组合不能重复。

##### 思路：
根据上面分析，最直观的想法，就是需要从1-n逐步，找出可能的组合情况，组合长度等于k，所有最直接的方法就是递归调用循环。
1. 从1开始自增循环，将数存储到item
2. 递归调用自己后，item清空自己，以便下次临时存储新数据
3. 当item的长度等于k的时候，将item的数值复制给inner，再存储到返回数组中，注：千万不要使用=，=是引用，会根据item变化而变化
4. 最后循环到n为止，返回满足长度等于k数值介于1和n之间的所有数组组合


##### 复杂度：
时间复杂度O(n!)

##### Js实现：
```
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
let combine = function(n, k) {
    let res = [],item = [];
    if (n <= 0) return res;
	dfs(n, k, 1, item, res); // 从1开始
	return res;
};

function dfs(n,k,start,item,res) {
    if (item.length === k) {
    //因为item是临时存储数组，不能直接相等，js中=是引用，数组会根据item的变化而变化，所以必须将满足条件那一刻的数据复制到新变量中才可以
        let inner = [].concat(item);
		res.push(inner);
		return;
	}
	if(item.length > k) return; //剔除一部分循环，节约时间
	for (let i = start; i <= n; i++) {
		item.push(i);
		dfs(n, k, i + 1, item, res);
		item.splice(item.length - 1,1);
	}
}
```