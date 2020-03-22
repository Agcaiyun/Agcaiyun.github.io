---
layout:           post
title:            mac中更新 node 版本信息
subtitle:         方式：用命令行操作
date:             2019-05-21
anthor:           caiyun
header-img:       img/header/19-05-21-node-update-header.jpg 
catalog:          true
tags:             
    - tools
---

> 参考链接：[https://www.jianshu.com/p/114490ec1bd8](https://www.jianshu.com/p/114490ec1bd8)

* 清除 node.js 的 cache
  * `sudo npm cache clean -f`
* 安装 n 工具，这个工具是专门来管理 node 版本的
  * `sudo npm install -g n`
* 用 n 工具安装最新版本的 node.js（这一步才是真正的安装最新版本 node 的命令，不能省略哦）
  * `sudo n stable`
* 再次查看 node 的版本
  * `node -v`