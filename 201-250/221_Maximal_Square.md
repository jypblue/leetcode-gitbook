# 221. Maximal Square
##### Tags
1. Dynamic Programming

>Given a 2D binary matrix filled with 0's and 1's, find the largest square containing all 1's and return its area.

>For example, given the following matrix:
```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```
>Return 4.

##### 题意：
给定一个二维二进制矩阵填充0和1，找到包含所有1最大的正方形，返回其面积。

##### 分析：
典型的动态规划解决矩阵问题，方法很简单，数字四周都是1，则+1；如果是0就取原值不变。四周1越多，边线长也就越大，最后的矩形值也就越大。比较规则就是，循环当前值与左边，上边及左上的值进行比较，取三者比较后的最小值+1，如果是0，+1后是1，不影响计算面积，如果是>=1，+1后，数字增大，平方值就是面积。

##### 思路：
1. 创建二维矩阵m行n列；
2. 以第一行第一列为基准，第二行第二列开始循环比较
3. 比较规则就是，当这个数是1的时候，与左，上，左上的数字相比，取最小数+1；然后将数字放入二维矩阵数组中；当这个数为0的时候，就存入0.
4. 循环二维数组，求每个数的平方值，最大的值就是我们要返回的最大正方形的面积

##### Js实现：
##### 复杂度：
时间复杂度度O(n)

```
/**
 * @param {character[][]} matrix
 * @return {number}
 */
let maximalSquare = function(matrix) {
    //如果矩阵为空或者第一行为空，则为0
    if(matrix === null || matrix.length ===0 || matrix[0].length=== 0){
        return 0;
    }
    
    //获取矩阵的行列长度
    let m = matrix.length;
    let n = matrix[0].length;
    
    //创建m行n列的二维数组
    let t = [];
    for(let i = 0; i < m;i++) {
        let g = [];
        for(let j = 0;j < n;j++) {
            g[j] = 0;
        }
        t[i] = g;
    }
    
    //第一行
    for (let i = 0; i < m; i++) {
		t[i][0] = parseInt(matrix[i][0],10);
	}
    //第一列
    for(let j = 0;j < n ;j++) {
        t[0][j] = parseInt(matrix[0][j],10);
    }

    //除去第一行第一列的矩阵内
    for(let i = 1;i < m;i++) {
        
        for(let j = 1; j < n;j++) {
            //如果某项数字为1,输入的不一定是数字，可能是字符串
            if(matrix[i][j] == '1') {
                //将比较该位置的数字的左，上，左上位置的数字大小，
                //取三个位置最小值加1重新设定在二维数组t中相应的地方,
                //标记那个位置区域为1的个数的平方根
                //如果都为1，则累加1；如果有一个位置为0，则设定为原数0+1，仍为1不变。
                //console.log(matrix[i][j]);
                let min = Math.min(t[i - 1][j], t[i - 1][j - 1]);
				min = Math.min(min,t[i][j - 1]);
			//	console.log(min);
				t[i][j] = min + 1;
			//	console.log(t[i][j]);
            } else {
                t[i][j] = 0;
            }
        }
    }
    //默认最大为0
    //获取数组中最大的那个值
    let max = 0;
    for(let i = 0; i < m;i++) {
        for(let j = 0; j < n;j++) {
            if(t[i][j]>max) {
                max = t[i][j]
            }
        }
    }
    
    return max*max;
};

```