---
title: 优化造成浏览器锁死的循环
date: 2017-08-04 19:52:02
tags: optimize
categories: 
- 前端
- optimize
---
# 优化for循环
当一个循环耗时过长时，会造成浏览器锁死，用户界面会无反应，用户体验极差，因此可以用定时器处理。
定时器处理会延长处理的时间，但是避免浏览器锁死，因此更值得使用
<!-- more -->
```
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
var i = [1,2,3,4,5,6,7];
processArray(i, logOut,callBack);
```
