---
title: mocha
date: 2017-10-19 16:23:42
tags: test
categories: 
- 前端
- test
---

## 测试框架Mocha+webpack搭建教程
<!-- more -->
### 安装mocha
`npm install --global mocha`
### 创建webpack项目
新建一个文件夹，cd进入文件夹，输入
`npm init`
创建webpack的项目
![](http://ovftx8ppu.bkt.clouddn.com/webpackMocha.jpeg)
在test command填入
`mocha --compilers js:babel-core/register`
*`mocha`为运行测试的命令，默认运行test下的\*.**test.js文件，`--compilers`参数后面紧跟一个用冒号分隔的字符串，冒号左边是文件的后缀名，右边是用来处理这一类文件的模块名。上面代码表示，运行测试之前，先用`babel-core/register`模块，处理一下.js文件。由于这里的转码器安装在项目内，所以要使用项目内安装的Mocha；如果转码器安装在全局，就可以使用全局的Mocha***
然后就一直回车，创建完成


运行
`npm i --D chai babel-core babel-preset-es2015`
安装chai和es2015模块

创建一个.babelrc文件

```
{
    "presets": [ "es2015" ]
}
  ```
  文件中配置将es6转成es2015，方便之后的书写
  
  文件下手动创建src和test文件，src用来存放要测试的js
  
```
export function compare(a, b) {
    return b * a;
}
```

test文件下创建一个*.test.js的测试脚本

```
'use strict';

var _compare = require('../src/compare.js');

var expect = require('chai').expect;

describe('乘法函数的测试', function () {
  it('1 乘 1 应该等于 1', function () {
    expect( _compare.compare(1, 1)).to.be.equal(1);
  });
});
```

之后就可以通过
`npm run test`
来运行测试脚本

到此一套测试的用例就搭建完成，在阮一峰博客有mocha更详细教程，此处只是将webpack和mocha合并起来，方便mocha的使用。
此处附上阮一峰博客的[飞机票](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)
