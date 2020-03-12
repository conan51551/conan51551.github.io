---
title: 标签中嵌入链接跳转
tags:
  - optimize
date: 2018-01-05 18:31:24
categories:
- 前端
- blog
---
### html标签中嵌入url

在html标签中嵌入url不能直接点击链接跳转，此时需要将url链接匹配出来，然后添加a标签，完成跳转
<!-- more -->
``` javascript
if(str.indexOf("http://")>=0||str.indexOf("https://")>=0){
    var reg = /(http:\/\/|https:\/\/)((\w|=|\?|\.|\/|&|-)+)/g;
    str = str.replace(reg, "<a style='text-decoration:none;color:#fff;' href='$1$2'>$1$2</a>");
}
```
