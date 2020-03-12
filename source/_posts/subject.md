---
title: 10分钟题目
date: 2017-08-03 17:54:27
tags: subject
categories: 
- 题目
---
# 问题1

使用for循环、while循环和递归写出3个函数来计算给定数列的总和。
<!-- more -->

```javascript
function forFun(arr) {
    var sum = 0;
    for (var i = arr.length; i > 0; i--) {
        sum = sum + arr[i - 1];
    }
    console.log(sum);
}

function whileFun(arr) {
    var sum = 0;
    var i = arr.length;
    while (i > 0) {
        sum = sum + arr[i - 1];
        i--;
    }
    console.log(sum)
}

function recFun(arr, i) {
    if (i <= 0) {
        return arr[i]
    } else {
        return arr[i] + recFun(arr, i - 1)
    }
}
```

# 问题2

编写一个交错合并列表元素的函数。例如：给定的两个列表为[a，B，C]和[1，2，3]，函数返回[a，1，B，2，C，3]。

```javascript
function crossFun(arr1, arr2) {
    var arr3 = [];
    var sortArr = arr1 > arr2 ? arr1.slice() : arr2.slice();
    sortArr.map(function (item, index) {
        arr3.push(arr1.shift());
        arr3.push(arr2.shift());
    });
    arr3 = arr3.concat(arr1, arr2);
    console.log(arr3);

}
```

# 问题3

编写一个计算前100位斐波那契数的函数。根据定义，斐波那契序列的前两位数字是0和1，随后的每个数字是前两个数字的和。例如，前10位斐波那契数为：0，1，1，2，3，5，8，13，21，34。

```javascript
function fiboFun() {
    var fiboArr = [];
    for (var i = 0; i < 100; i++) {
        if (i < 2) {
            fiboArr[i] = i;
        } else {
            fiboArr.push(fiboArr[i - 2] + fiboArr[i - 1]);
        }
    }
    console.log(fiboArr);
    console.log(fiboArr.length);
}
```

# 问题4

编写一个能将给定非负整数列表中的数字排列成最大数字的函数。例如，给定[50，2，1,9]，最大数字为95021。

```javascript
function maxNumFun(arr) {
    var arr1 = arr.toString();
    arr1 = arr1.split(",");
    for (var i = 1; i < arr1.length; i++) { //根据最大的那一位排序
        for (var j = 0; j < arr1.length - 1; j++) {
            if (arr1[j][0] < arr1[j + 1][0]) {
                var temp = arr1[j];
                arr1[j] = arr1[j + 1];
                arr1[j + 1] = temp;
            }
        }
    }
    for (var j = 0; j < arr1.length; j++) {
        for (var i = 0; i < arr1.length - 1; i++) {
            var res = getTheSortBig(arr1[i], arr1[i + 1], 0);
            arr1[i] = res[0];
            arr1[i + 1] = res[1];
        }
    }

    arr1;
}

function getTheSortBig(str1, str2, k) {
    if (str1[k] == str2[k]) {//如果第一位一样大，就继续比较下一位
        var i = k + 1;
        return getTheSortBig(str1, str2, i);
    } else if (str1[k] < str2[k]) {
        var res = [str2, str1];
        return res;
    } else if (str1[k] > str2[k]) {
        var res = [str1, str2];
        return res;
    } else {
        var res = [];
        if (str1[k]) {// 比较的两个数，第一个数的K位存在，比较第一个数的k位和第二个数的上一位
            if (str1[k] > str2[k - 1]) {
                res = [str1.length > str2.length ? str1 : str2, str1.length > str2.length ? str2 : str1];
            } else {
                res = [str1.length > str2.length ? str2 : str1, str1.length > str2.length ? str1 : str2];
            }
        } else {
            if (str2[k] > str1[k - 1]) {
                res = [str1.length > str2.length ? str1 : str2, str1.length > str2.length ? str2 : str1];
            } else {
                res = [str1.length > str2.length ? str2 : str1, str1.length > str2.length ? str1 : str2];
            }
        }

        return res;
    }
}
```

# 问题5

编写一个在1，2，…，9（顺序不能变）数字之间插入+或-或什么都不插入，使得计算结果总是100的程序，并输出所有的可能性。例如：1 + 2 + 34 – 5 + 67 – 8 + 9 = 100。

```javascript
var totalNum = 0;
var symbol = new Array(9);
var numArr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
for (var s1 = 0; s1 < 3; s1++) {
    symbol[0] = toSymbol(s1);
    for (var s2 = 0; s2 < 3; s2++) {
        symbol[1] = toSymbol(s2);
        for (var s3 = 0; s3 < 3; s3++) {
            symbol[2] = toSymbol(s3);
            for (var s4 = 0; s4 < 3; s4++) {
                symbol[3] = toSymbol(s4);
                for (var s5 = 0; s5 < 3; s5++) {
                    symbol[4] = toSymbol(s5);
                    for (var s6 = 0; s6 < 3; s6++) {
                        symbol[5] = toSymbol(s6);
                        for (var s7 = 0; s7 < 3; s7++) {
                            symbol[6] = toSymbol(s7);
                            for (var s8 = 0; s8 < 3; s8++) {
                                symbol[7] = toSymbol(s8);
                                for (var s9 = 0; s9 < 3; s9++) {
                                    symbol[8] = toSymbol(s9);
                                    var equation = "";
                                    for (var i = 0; i < 9; i++) {
                                        equation += symbol[i] + numArr[i];
                                    }
                                    if (eval(equation) == 100) {
                                        console.log(equation);
                                        totalNum++;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
console.log(totalNum);

function toSymbol(num) {
    switch (num) {
        case 0:
            return '+';
            break;
        case 1:
            return '-';
            break;
        case 2:
            return '';
            break;
    }
}
```

