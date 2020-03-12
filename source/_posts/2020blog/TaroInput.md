---
title: TaroInput
p: 2020blog/TaroInput
date: 2020-03-12 11:11:40
tags:
---

### 在使用Taro开发小程序过程中，遇到一个关于Input组件的问题

>问题描述：在onBlur中修改input的值，不生效，修改input的Value，会有value和展示的值不一致的问题

<!-- more -->

### 在微信的官方文档中写到
>bindinput说明：
键盘输入时触发，event.detail = {value, cursor, keyCode}，keyCode 为键值，2.1.0 起支持，处理函数可以直接 return 一个字符串，将替换输入框的内容。

### 而在其他的触发方法中，并不能直接修改输入框中的内容

### 最终的解决方法是
``` javascript
{showInput ?
    <Input
    className='input'
    value={number + ''}
    onBlur={this.onChangeNum}
    onInput={this.checkNum}
    type='number'
    focus={showInput}
  /> : 
  <Text className='input' onClick={this.focusInput}>{number}</Text>} 
```

### 用一个text代替input展示，问题就解决了