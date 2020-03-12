---
title: contenteditable=true的div在安卓上的坑
date: 2018-06-20 17:55:53
tags: 
categories: 
- 前端
- 坑
---

`contenteditable=true`的`div`，在安卓手机上获取焦点时，总是会在光标下方出现小水滴，点击按钮时还不会自动隐藏，很恶心。

最后用一个不显示的input，当每次点击按钮时，focus这个input，然后在blur，可以解决这一问题
