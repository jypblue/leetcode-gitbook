# 310. Minimum Height Trees
##### Tags
1. Graph
2. Breadth-first Search

>For a undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

><strong>Format</strong>
>
>The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).
>
>You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.
>
><strong>Example 1:</strong>
>
Given n = 4, edges = [[1, 0], [1, 2], [1, 3]]
```
        0
        |
        1
       / \
      2   3
```      
>return [1]
>
<strong>Example 2:</strong>
>
>Given n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]
```
     0  1  2
      \ | /
        3
        |
        4
        |
        5
```        
>return [3, 4]

##### 题意：
对于一个有树特征的无向图，我们可以选择任何节点作为根。结果图是一个根深蒂固的树。所有可能的根树中，那些具有最小高度为最小高度的树木（MHTS）。在这样一个图，写一个函数来找到所有MHTS并返回一个列表的根标签。

##### 分析：
知识点：拓扑排序，剥洋葱方法

1. 由于是无向图，且图中没有环，那么对于图中的叶子节点来说，其跟的临接表大小为1；
2. 找出图中所有临接表大小为1的节点，并且删除和它们相连接的节点的这条连接线；
3. 每删除一次，判定当前节点的临接表大小是不是1，如果是1，证明它也变成了叶子节点，这个就作为下一步删除的叶子节点;
4. 根据上面分析，根节点至多两个，所以叶子节点最后的数量不能多余两个；

##### 思路：
根据以上分析，具体实现见代码

##### Js实现：
##### 复杂度：
时间复杂度O(n<sup>2</sup>)

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number[]}
 */
var findMinHeightTrees = function(n, edges) {
    if (n === 1) {
        let result = [];
        result.push(0);
        return result;
    } 
    let list = new Array(n);
    for (let i = 0; i < n; i++) list[i] = [];
    for (let edge of edges) {
            list[edge[0]].push(edge[1]);
            list[edge[1]].push(edge[0]);
    }
    let leaf = [];
    for(let i = 0 ; i < n;i++) {
        if(list[i].length === 1 ) {
            leaf.push(i);
        }
    }
    while(n > 2) {
     n -= leaf.length;
        let newLeaf = [];
            for (let i of leaf) {
                let j = list[i][0];
                list[j].forEach(function(value,index){
                    if(value == i) {
                        list[j].splice(index,1);
                    }
                })
                if(list[j].length ==1) {
                    newLeaf.push(j);
                }
            }
        leaf = newLeaf;
    } 
    return leaf;
};
```









