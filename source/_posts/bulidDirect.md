---
title: bulidDirect
date: 2017-10-11 11:17:20
tags: direct
categories: 
- direct
---

## 下载与安装模拟器

这里推荐的是Oracle家族的[VirtualBox模拟器](https://www.virtualbox.org/),个人使用下来的感受是做开发用的模拟器完全碾压VM!
<!-- more -->
## 安装和配置模拟器

1.软件一直默认安装好即可!
2.新建一个node的linux虚拟镜像
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_1.png)
3.一路默认直到建好,然后设置网卡
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_2.png)
4.设置系统盘片,前往下载Centos镜像
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_3.png)
5.都设置完成后,进入centos系统安装!
6.最好选择英文,不推荐中文(不是为了秀,确实选中文也没什么用的)
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_4.png)
7.选择默认软件包: SOFTWARE SELECTION
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_5.png)
8.左栏选择基础web开发包，右栏选择开发者工具包
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_6.png)
9.选择系统安装位置
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_7.png)
10.默认已经选择了一块磁盘，注意这里先取消选中，再重新选择上
![](http://ovftx8ppu.bkt.clouddn.com/VirtualBox_8.png)
11.开始安装系统。。。

## 安装完成后的配置步骤

1.修改网卡配置

vi /etc/sysconfig/network-scripts/ifcfg-enp0s3

onboot=yes

2.重启网卡服务

systemctl restart network

*以上的cenos系统完成后，接下来就是nginx的搭建*

1、下载nginx-rtmp-module：
nginx-rtmp-module的官方github地址：https://github.com/arut/nginx-rtmp-module
使用命令：
` git clone https://github.com/arut/nginx-rtmp-module.git  `
将nginx-rtmp-module下载到linux中。

2、安装nginx：

```
wget http://nginx.org/download/nginx-1.8.1.tar.gz  
tar -zxvf nginx-1.8.1.tar.gz  
cd nginx-1.8.1  
./configure --prefix=/usr/local/nginx  --add-module=../nginx-rtmp-module  --with-http_ssl_module    
make && make install  
```
本次默认安装目录为：/root， add-module为下载的nginx-rtmp-module文件路径。
安装时候可能会报错没有安装openssl，需要执行命令：
`yum -y install openssl openssl-devel    `
3、修改nginx配置文件：
`vi /usr/local/nginx/conf/nginx.conf  `
加入以下内容：

```
rtmp {    
    
    server {    
    
        listen 1935;  #监听的端口  
    
        chunk_size 4000;    
          
           
        application hls {  #rtmp推流请求路径  
            live on;    
            hls on;    
            hls_path /usr/share/nginx/html/hls;    
            hls_fragment 5s;    
        }    
    }    
}  
```

**此处注意，要用mkdir创建/usr/share/nginx文件夹**
hls_path需要可读可写的权限。
修改http中的server模块：

```
server {  
    listen       81;  
    server_name  localhost;  
  
    #charset koi8-r;  
  
    #access_log  logs/host.access.log  main;  
  
    location / {  
        root   /usr/share/nginx/html;  
        index  index.html index.htm;  
    }  
  
    #error_page  404              /404.html;  
  
    # redirect server error pages to the static page /50x.html  
    #  
    error_page   500 502 503 504  /50x.html;  
    location = /50x.html {  
        root   html;  
    }  
```

当然了，root可以跟据自己的需求来改的。
然后启动nginx:
`/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf   `

*接下来就是obs推流服务了*

首先记得配置nginx服务器的各个端口
![](http://ovftx8ppu.bkt.clouddn.com/obsDirect.png)

开始推流之前，在obs中填写推流的内容，此处以test为例
![](http://ovftx8ppu.bkt.clouddn.com/obsPush.png)

5、观看直播（拉流）
观看直播就比较简单了，可以简单的使用h5的vedio标签就可以观看了。
可以访问http://xxx:81/hls/mystream.m3u8来观看直播，其中xxx为你的服务器IP地址

以上关于obs推流方面还有不太明白的小伙伴，这是[飞机票](http://blog.csdn.net/zph1234/article/details/52846223)



