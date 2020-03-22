---
layout:           post
title:            ruby 安装
subtitle:         mac os 10.13.6
date:             2019-06-19
anthor:           caiyun
header-img:       img/header/19-06-19-ruby-install-header.jpg 
catalog:          true
tags:             
    - tools
---

> 原文链接：https://www.jianshu.com/p/dfc12df2b7e6

* 先安装 rvm
  * 命令为:  `$ curl -L https://get.rvm.io | bash -s stable`
  * 安装完成后，需要重新加载 rvm 环境，有以下两种方式：
    * 可以重新打开一个 terminal，重开的 terminal 会自动加载 rvm 环境
    * 运行命令：`$ source ~/.rvm/scripts/rvm` 
  * 检查是否已经安装成功
    * 命令为： `rvm -v`
    * 安装成功会输出类似信息: `rvm 1.29.8 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]`

* 然后安装 ruby
  * `rvm autolibs read-only # read more here:https://rvm.io/rvm/autolibs`
  * `rvm install ruby`

* 查看 ruby 版本信息
  * `ruby -v`
    * ruby 安装成功后，会看到类似信息：`ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin17]`
