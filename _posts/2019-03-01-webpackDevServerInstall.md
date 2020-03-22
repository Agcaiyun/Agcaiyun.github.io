---
layout:           post
title:            webpack-dev-server 安装
subtitle:         
date:             2019-03-01
anthor:           caiyun
header-img:       img/header/19-03-01-webpack-dev-server-header.jpg 
catalog:          true
tags:             
    - tools
---

在**项目文件根目录**（通常会有 package.json 文件）下，执行命令：
npm install webpack-dev-server --save-dev
**执行上面命令，会默认安装最新的 webpack-dev-server**

如果要安装特定版本的 webpack-dev-server 的话，可以执行命令：
npm install webpack-dev-server@x.x.x --save-dev

在安装过程中，可能会报错
可能报错一：
![在安装过 npm -i -D webpack-cli 后仍提示安装](https://upload-images.jianshu.io/upload_images/6970677-585b5b3edd44a0a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

有时候**已经执行了 npm i -D webpack-cli 命令**，并且成功安装了 webpack-cli ，但是还出现这样的报错，如果出现这种情况，可能是 webpack-dev-server 安装的不正确，要在项目文件根目录（通常会有 package.json 文件）下执行安装命令

在安装成功后，在这里可以看到相关文件：
![image.png](https://upload-images.jianshu.io/upload_images/6970677-c99f2a8e821ae618.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个报错很可能是 webpack-dev-server 的版本与 webpack 版本不匹配的原因

在我的项目中，webpack 版本是 3.x.x  ，可以将 webpack-dev-server 的版本限制在 2.x.x

比如： 
webpack: 3.12.0
webpack-dev-server: 2.11.3
限制 webpack-dev-server 的版本后，就可以正常执行 webpack-dev-server 命令了~
![image.png](https://upload-images.jianshu.io/upload_images/6970677-4002261d695a9283.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
