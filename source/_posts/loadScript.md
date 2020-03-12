---
title: 优化前端脚本加载
date: 2017-07-18 13:39:27
tags: optimize
categories: 
- 前端
- optimize
---

******
# 优化javascript加载和执行

浏览器每次遇到``<script>``标签都会停下等待代码下载并执行，影响页面的加载。下面几个方法可以减少js对性能的影响
<!-- more -->
### ``</body>``标签闭合之前，将所有``<script>``标签放在页面底部
这能确保脚本执行前页面完成渲染

### 合并脚本

``<script>``标签越少，加载越快，无论内联还是外链文件都是如此
### 无阻塞下载js的方法

#### defer属性

defer属性表明本元素所含脚本不会修改DOM，因此代码能安全的延迟执行。
带有defer属性的``<script>``可以放在任何位置，对应的Javascript文件将在页面解析到``<script>``标签时开始下载，但不会执行，直到DOM加载完成
***onload事件被触发前***

#### 使用动态创建的``<script>``元素来下载并执行代码

```
function loadScript(url, callback) {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src = path;
    if(script.readyState){//ie
    script.onreadystatechange == function(){
        if(script.readyState == "loaded" || script.readyState == "complete"){
            script.onreadystatechange = null;
            callback();
        }
    }
    }else{
        script.onload = function() {
            callback();
        }
    }
    script.src = url;
    document.body.getElementsByTagName('head')[0].appendChild(script);
}
```

动态创建``<script>``标签，当下载完成执行callback，然后将``<script>``写入``<head>``标签中   

#### 使用XHR对象下载

```
var xhr = new XMLHttpRequest();
xhr.open("get","index.js",true);
xhr.onreadystatechange = function(){
if(xhr.readyState == 4){
	if(xhr.status >= 200 && xhr.status <300 || xhr.status == 304){
		var script = document.createElement("script");
		script.type = "text/javascript";
		script.text = xhr.responseText;
		document.body.appendChild(script);
		}
	}
}
```	  

发送一个GET请求获取index.js。
***好处:下载js代码但不执行。代码在``<script>``标签之外返回的，因此下载完不会立马执行***
局限性:js文件必须与请求的页面处于相同的域。以为这js不能从cdn下载。

