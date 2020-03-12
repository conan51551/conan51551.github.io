---
title: DOM编程
date: 2017-07-20 13:21:10
tags: optimize
---

# DOM编程
DOM（文档对象模型）是独立于语言的。浏览器通常把DOM与js分开实现。
<!-- more -->
### DOM的访问与修改
***尽量将运算放在js这一端处理***
#### innerHTML和DOM方法
修改页面区域的最佳方案究竟是用非标准但支持良好的innerHTML，还是用原生DOM的方法？
在性能上两者相差无几，但是从代码量上分析，推荐使用innerHTML。

#### 节点克隆
使用克隆已有元素，更新页面内容
``element.cloneNode()``替代``document.createElement()``
在性能上会稍微快一点
#### HTML集合
类似``document.getElementByTagName()``方法返回的就是一个HTML集合。``document.images``属性返回的同样是一个HTML集合。

***事实上HTML集合一直与文档保持着连接，每次需要最新的信息，都会重复执行查询的过程。这正是低效之源。***
将html集合拷贝到普通数组，再进行操作，会大大提升效率。

#### 元素节点
在某些情况下，只需访问元素节点，比如不需要注释和文本节点。大部分浏览器提供的API只返回元素节点


| 属性名 | 被替代的属性 |
| :-: | :-: |
| children | childNodes |
| childElementCount | childNodes.length |
| firstElementChild | firstChild |
| lastElementChild | lastChild |
| nextElementSibling | nextSibling |
| previousElementSibling | previousSibling |

##### 选择器API
``document.querySelectorAll("#menu a")``查询id为menu中的所有a标签静态列表

#### 重绘与重排
浏览器下载完所有组件，会解析并生成两个内部数据结构
dom树:表示页面机构
渲染树:表示DOM节点如何显示

重绘就是讲DOM树重新排列，重绘就是重新渲染。***这两个操作都会导致Web应用程序的UI反应迟钝***

##### 最小化重排和重绘
* 使用cssText属性修改样式
* 批量修改DOM
    * 使元素脱离文档流
    
        1.隐藏元素(display:none)
        2.在DOM之外创建一个子树，然后拷贝进文档流
        3.将元素拷贝到一个脱离文档的节点中，修改副本，再放回去    
    * 对其应用多重改变
    * 把元素待会文档中

``document.creatDocumentFragment()``***在文档之外创建并更新一个文档片段***``appendDataToElement()``***添加data到文档片段中***    

#### 使用事件委托来减少事件处理器
 



