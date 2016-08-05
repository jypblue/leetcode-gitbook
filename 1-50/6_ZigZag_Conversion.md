# 6. ZigZag Conversion
##### Tags
1. String

>The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
>
```
P   A   H   N
A P L S I I G
Y   I   R
```
>And then read line by line: `"PAHNAPLSIIGYIR"`
>
>Write the code that will take a string and make this conversion given a number of rows:
>
```
string convert(string text, int nRows);
```
>
>`convert("PAYPALISHIRING", 3) `should return `"PAHNAPLSIIGYIR"`.


##### 题意：
给定一个字符串是一ZigZag这种格式书写的，请将这些字符按照横向顺序合并起来返回。

##### 分析：
本题直接的表现就是递推找规律，横向纵向，所以我们用先用数字代表每个字符的坐标，然后按照它给定的ZigZag规则，推倒规律。以题目给的例子为例，坐标矩阵如下：
```
1   5   9     13
2 4 6 8 10 12 14
3   7   11 
```
我们可以发现每一行间隔数`2 * nRows - 2`;每一列的间隔是`2 * nRows - 2 - 2i,i = 0,1,2...`,我们多试几个例子看一看是否准确：
当 nRows = 4 时：
```
1     7        13  
2   6 8     12 14
3 5   9  11    15
4     10       16 
```
当nRows = 5 时：
```
1       9           17
2     8 10       16 18
3   7   11    15    19
4 6     12 14       20
5       13          21
```
发现都是满足的。所以我们规律找到了。

##### 思路：
通过分析我们找到了规律，方法步骤就很明确了，
1. 以nRows作为循环数循环每一行
2. 以`2*nRows-2`规律获取到每行第一个字符
3. 以`2*nRows-2-2*i`规律获取每行后续字符

##### Js实现：
##### 复杂度：
时间复杂度O(n)

```
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
let convert = function(s, numRows) {
    
    if(s===null || s.length === 0 || numRows < 2) return s;
    let str = '';
    let step = 2*numRows-2;  // numRows必须大于1
    for(let i=0; i < numRows; i++) {
        let j = i, gap = 2*numRows-2*i-2;
        
        while(j< s.length){
            //每行首列字符
            str+=s[j];
            //每行后续字符
            if(gap!==0 && gap!== step && j+gap<s.length) 
                str+=s[j+gap];
            //每行退出条件        
            j += step;
        }
    }
    return str;
};

```


