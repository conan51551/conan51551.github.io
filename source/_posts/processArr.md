---
title: processArr
date: 2017-10-11 11:16:36
tags: optimize
categories: 
- 前端
- optimize
---

### 拆分字符串的优化

最近的项目经常用到字符串的拆解，下面将一个拆分的优化方案记录，以便日后使用

<!-- more -->
``` javascript
function processArray(items, process, callback) {
    var todo = items.concat();

    setTimeout(function () {
        process(todo.shift());

        if (todo.length > 0) {
            setTimeout(arguments.callee, 25)
        } else {
            callback(items);
        }
    }, 25);
}

function logOut(val){
    console.log(val);
}
function callBack(){
    console.log("done");
}
var i = [1,2,3,5,9,6,7];
processArray(i, logOut,callBack);
```
