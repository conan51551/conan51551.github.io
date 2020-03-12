---
title: 史上最简单的Hexo+GitHub的博客搭建教程
tags:
  - blog
date: 2017-08-09 15:26:33
categories:
- 前端
- blog
---

>先把各自的官网来一发
>**GItHub:**https://github.com      *国外的代码托管平台*
>**Coding:**https://coding.net      *国内的代码托管平台,速度快,以及私有项目*
>**Hexo:**https://hexo.io/      *快速、简洁且高效的博客框架*
>**NexT:**http://theme-next.iissnan.com      *精于心，简于形的博客主题*
>安装前电脑需要先安装git,node
<!-- more -->
-------------------

### 第一步
- 注册GitHub/Coding
- 创建repository
![git1](http://ohlizmtv0.bkt.clouddn.com/git1.png)
- 写项目名,看格式, **(自己的github名).github.io**  *我这里因为已经创建过了,所以用'godd636'来代替一下*
![git2](http://ohlizmtv0.bkt.clouddn.com/git2.png)
- 获取到https的项目地址,后面要用到
![git3](http://ohlizmtv0.bkt.clouddn.com/git3.png)

### 第二步
依次执行下面的代码
```
npm install hexo-cli -g  //全局安装hexo
hexo init 自己的博客名     //初始化博客
cd 自己的博客名            //进入博客文件夹
npm install        //安装必备组件
hexo server              //本地启动博客服务
```
此时如果看到下面的样子就表示成功了
![hs](http://ohlizmtv0.bkt.clouddn.com/hexoserver.png)
打开浏览器输入:localhost:4000 即可看到本地博客了
![localhostblog](http://ohlizmtv0.bkt.clouddn.com/localhostblog.png)
### 第三步
>这一步是最重要的了,就是部署到GitHub/Coding上

- 修改项目下的_config.yml文件
- 添加最下面的部署地址,就是第一步复制到的地址,如果需要同时部署到GitHub和Coding就像我这样写两个!
![config](http://ohlizmtv0.bkt.clouddn.com/config.png)
- 开始部署
![dg](http://ohlizmtv0.bkt.clouddn.com/hexodg.png)
- **这个时候不出意外,应该是要报错的!因为没有引入git的中间件**
- 此时看官方的部署文档,发现需要这个
![hexogit](http://ohlizmtv0.bkt.clouddn.com/hexogit.png)

- **项目目录安装hexo-deployer-git**
![gitsave](http://ohlizmtv0.bkt.clouddn.com/gitsave.png)
- 再次部署 
```
hexo d -g
```
- *可能需要输入github的账户和密码*所以最好配置一下SSH
```
//在Git Bash下输入
ssh-keygen -t rsa -C "你的github账户邮箱"  //一直回车直到完成
//然后输入
clip < ~/.ssh/id_rsa.pub
```
- 打开github
![setting](http://ohlizmtv0.bkt.clouddn.com/setting.png)
- 添加新SSH
![setting](http://ohlizmtv0.bkt.clouddn.com/zhantie.png)
- **之后部署就不需要密码了!**
- 浏览器直接访问 **账户名.github.io** 即可
- 其他一些创建新文章之类的直接看[hexo文档](https://hexo.io/zh-cn/docs/writing.html)即可!
![writing](http://ohlizmtv0.bkt.clouddn.com/writeing.png)

### 转载自https://godd6366.github.io/ 