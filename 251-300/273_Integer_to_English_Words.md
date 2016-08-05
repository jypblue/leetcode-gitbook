# 273. Integer to English Words 
##### Tags
1. Math
2. String

> Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2<sup>31</sup> - 1.

>For example,
```
123 -> "One Hundred Twenty Three"
12345 -> "Twelve Thousand Three Hundred Forty Five"
1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

##### 题意：
将非负整数转换为它的英文单词表示。给定输入保证小于2<sup>31</sup> - 1

##### 分析：
 这道题刚拿到的时候，最直接的想法就是分断求余数，然后根据每个数字对应的英文单词拼接起来返回即可，具体实施的时候，发现并没有那么简单，于是谷歌了发现基本思路的确是这样，但是很多细节还是得考虑周全才行。
 
 ##### 思路：
 见Js实现代码，谷歌查看Java代码改编而来
 
 ##### Js实现：
 ##### 复杂度：
 时间复杂度O(n)
 
 ```
 /**
 * @param {number} num
 * @return {string}
 */
let numberToWords = function(num) {
    if (num < 0) {
            return "";
        }

        //数字为0直接返回
        if (num === 0) {
            return "Zero";
        }

        //左起段落
        let segment1 = Math.floor(num / 1000000000);             //段落1：十亿位-千亿位
        let segment2 = Math.floor((num % 1000000000) / 1000000); //段落2：百万位-亿位
        let segment3 = Math.floor((num % 1000000) / 1000);       //段落3：千位-十万位
        let segment4 = Math.floor(num % 1000);                   //段落4：个位-百位

        let result = "";
        
        if (segment1 > 0) {
            result += numToWordsLessThan1000(segment1) + " " + "Billion";
        }
        if (segment2 > 0) {
            result += numToWordsLessThan1000(segment2) + " " + "Million";
        }
        if (segment3 > 0) {
            result += numToWordsLessThan1000(segment3) + " " + "Thousand";
        }
        if (segment4 > 0) {
            result += numToWordsLessThan1000(segment4);
        }

        return result.trim();
};


 
    /**
     * 按英语读法输出阿拉伯数字对应单词
     * @param num 数字，范围：(0,1000)
     * @return
     */
    function numToWordsLessThan1000(num) {
        
        if (num === 0 || num >= 1000) {
            return "";
        }
        
        let result = "";
        if (num >= 100) {
            result += numToWordsBase(Math.floor(num / 100)) + " " + "Hundred";
        }
        num = num % 100;
        if (num > 20) {
            result += numToWordsBase(Math.floor(num / 10) * 10);
            if (num % 10 !== 0) { 
                result += numToWordsBase(num % 10);
            }
        } else if (num > 0) {
            result += numToWordsBase(num);
        }
        
        return result;
    }
    
    
     /**
     * 按英语读法输出阿拉伯数字对应单词
     * @param num 数字，范围：(0,20)∪{30,40,50,60,70,80,90}
     * @return
     */
    function numToWordsBase(num) {
        let result = " ";
        switch (num) {
        case 1: result += "One"; break;
        case 2: result += "Two"; break;
        case 3: result += "Three"; break;
        case 4: result += "Four"; break;
        case 5: result += "Five"; break;
        case 6: result += "Six"; break;
        case 7: result += "Seven"; break;
        case 8: result += "Eight"; break;
        case 9: result += "Nine"; break;
        case 10: result += "Ten"; break;
        case 11: result += "Eleven"; break;
        case 12: result += "Twelve"; break;
        case 13: result += "Thirteen"; break;
        case 14: result += "Fourteen"; break;
        case 15: result += "Fifteen"; break;
        case 16: result += "Sixteen"; break;
        case 17: result += "Seventeen"; break;
        case 18: result += "Eighteen"; break;
        case 19: result += "Nineteen"; break;
        case 20: result += "Twenty"; break;
        case 30: result += "Thirty"; break;
        case 40: result += "Forty"; break;
        case 50: result += "Fifty"; break;
        case 60: result += "Sixty"; break;
        case 70: result += "Seventy"; break;
        case 80: result += "Eighty"; break;
        case 90: result += "Ninety"; break;
        }
        return result;
    }
 ```