---
title: iphone回退不刷新的问题
date: 2018-02-27 14:55:20
tags:
    - optimize
categories: 
    - 前端
    - optimize  
---
在iphone上存在返回上一页面后，页面不会刷新的问题，只需要在上一页面加上如下代码即可
<!-- more -->


``` javascript
//  解决iphone会退后不刷新页面的问题
(function(){
    var isPageHide = false;
    window.addEventListener('pageshow', function(){
        if(isPageHide) {
            window.location.reload();
        }
    });
    window.addEventListener('pagehide', function(){
        isPageHide = true;
    });
})();
```