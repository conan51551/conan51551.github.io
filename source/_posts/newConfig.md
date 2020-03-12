---
title: webpack动态配置环境
date: 2019-01-31 17:38:34
tags: webpack
categories:
- 前端
- webpack
---

最近优化MPVue小程序的项目，由于小程序必须有ext.json文件，并且项目中的一些配置都在其中，如URL路径，但是每次变更环境都要手动修改，为了避免这些麻烦，决定在webpack打包时动态修改

<!-- more -->

-------

在webpack的插件配置中发现如下代码

``` javascript
new CopyWebpackPlugin([{
      from: './**/.json',
      to: ''
    }, {
      context: 'src/'
    }
}
```
这就是MPVue默认生成app.json和ext.json的配置
决定在其复制之前根据打包命令读取各个环境的配置来生成对应的ext.json文件


-------

我默认文件是json，内容类似

``` javascript
{
  "pro": {
    *******
  },
  "test0": {
    *******
  }
}
```

``` javascript
let configPath = path.resolve(’填你自己默认配置文件的路径‘);
//这段node代码请根据各自情况修改
function copyExt(content){
  if(!!process.env.DEV_ENV && process.env.DEV_ENV.indexOf('/')<0){
    let apiData = fs.readFileSync(configPath)
    apiData = JSON.parse(apiData.toString());
    content = JSON.parse(content.toString());
    let api = apiData[process.env.DEV_ENV];
    let ext =  content['ext'];
    for(let _key in api){
      ext[_key] = api[_key];
    }
    return JSON.stringify(content);//这里建议转成string
  }else{
    return content
  }
}
```
最后在webpack中配置如下

``` javascript
 new CopyWebpackPlugin([{
  from: './app.json',
  to: ''
},
{
  from: './ext.json',
  to: 'ext.json',
  transform:function(content){
    return copyExt(content) //这里调用你写的拷贝方法，
    //会在dist生成之前调用transform，返回的data写入dist/ext.json中
  }
}], {
  context: 'src/'
}),
```

由于每次手动在start命令后输入很不爽，故引用`inquirer`在配置的时候可以选择具体传入的环境,引入`shelljs`可以在node中运行命令
``` javascript
  #!/usr/bin/env node

require('shelljs/global');
const Inquirer = require('inquirer');

Inquirer.prompt([{
  type: 'list',
  name: 'env_test',
  message: '请选择测试环境序号',
  choices: ['test0','test1','testx', 'pro']
}]).then((answers) => {
  let env_test = answers['env_test'];
  echo(`项目的启动命令 ${env_test}`)
  exec(`项目的启动命令 ${env_test}`);
});
```

在`package.json`中调用`"start": "node ${脚本的位置}",`即可

**文中的配置试用所有webpack打包的项目，此处以MPVue:1.0.13举例，由于新版MPVue在`"start": "node build/dev-server.js wx"`后面加了wx，我为了方便脚本编写，将wx的配置写死了，估不需要在新增的配置后加wx，读者根据各自实际情况做调整**
