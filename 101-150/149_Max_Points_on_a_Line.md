# 149. Max Points on a Line
##### Tags
1. Hash Table
2. Math

>Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

##### 题意：
在一个给定的n个点的平面上，找到同一直线上最多能有多少个点。

##### 分析：
根据题意，我们可以抓住几个关键信息：点，线，面。由此，最直接的画面就在脑子里面浮现了=>象限。我们知道两点构成一条直线，任意两个点都可以成一条直线。那么怎么判断多个点在一条直线上呢？其实很简单，就是看他在象限中，前后点之间的角度是否一致，计算角度最直接的方法，就是Y坐标距离除以X坐标距离，就是我们要的角度。当然也有可能点重复，亦或者与象限平行/垂直的情况。

##### 思路：
根据以上分析，思路如下：
1. 冒泡循环，比较前后点
2. 两种情况，1. 在竖直直线上；2. 在斜线上，则需要计算角度，若角度相等，就在该直线上
3. 情况1，2取最大值后在比较那种情况的值最大，返回最终最大值

##### 复杂度：
时间复杂度O(n<sup>2</sup>)

##### Js实现：
```
/**
 * Definition for a point.
 * function Point(x, y) {
 *     this.x = x;
 *     this.y = y;
 * }
 */
/**
 * @param {Point[]} points
 * @return {number}
 */
 
var maxPoints = function(points) {
    
//如果点为null或为0
if(points === null || points.length ===0) {
    return 0;
}

//ES6创建一个Map结构
let map = new Map();
let max = 1;
for(let i = 0; i < points.length; i++){
    //定义重复点及垂直点
    let dupPoint = 1,verPoint = 0;
    
    for(let j = i+1; j < points.length; j++){
        //处理垂直与重复的点
        if(points[i].x == points[j].x){
            if(points[i].y == points[j].y){
                //横纵坐标一致的时候说明是重复点，否则是垂直点
                dupPoint++;
            }else{
                verPoint++;
            }
        }else{
            //横纵坐标都不相同的时候
            //获取点在坐标系的偏移角度
            //如果纵坐标一致，为0度，否则两点的y轴距离除以x轴距离则是坐标角度；
            //如果角度一致说明在一条直线上
            let slope = points[j].y == points[i].y ? 0.0 : (1.0 * (points[j].y - points[i].y)) / (points[j].x - points[i].x);
            
            //如果map中已经有了该角度就累加，否则新增。
            if(map.has(slope)){
                map.set(slope, map.get(slope) + 1);
            }else{
                map.set(slope, 1);
            }
        }
    }
     for(let value of map.values()){
            if(value+dupPoint > max){
                max = value+dupPoint;
            }
        }
 
        max = Math.max(verPoint + dupPoint, max);
        map.clear();
    
}
    return max;
};

```