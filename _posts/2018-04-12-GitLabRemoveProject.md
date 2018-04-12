---
layout:           post
title:            GitLab 如何删除一个 Porject？
subtitle:         时间:2018/04/12   环境:win10 x64
date:             2018-04-12 
anthor:           caiyun
header-img:       img/GitLabRemoveProject-img/18-04-12-header.jpg 	 
catalog:          true
tags:
    - tools
---
> 本文首发于 [Caiyun Blog](http://agcaiyun.cn/ ),作者 [@Caiyun](https://github.com/Agcaiyun),  如果您喜欢想转载,这是我的荣幸,您只需要保留原文链接就好啦,谢谢哦 ^_^

> 今天需要将 GitLab 中一个私人Project 删掉，通常来说删除一个项目挺简单的，但是因为删除操作在项目中有内容时被隐藏了，所以花了一些时间才找到，于是将找到的过程分享出来


### 删除 GitLab Project
* 登录 GitLab 之后看到的界面是这样的
![sign-in](http://ow2akcnvb.bkt.clouddn.com/sign-in.png)
* 点击需要删除的项目中，会看到下图，然后点击左下角的 Setting 
![setting](http://ow2akcnvb.bkt.clouddn.com/setting.png)
* 然后点击 Advanced settings 右侧的 Expand
![expand](http://ow2akcnvb.bkt.clouddn.com/expand.png)
* 在展开后的页面中一直向下拉（拉到最底部），然后会看到 Remove project 的红色警告提示
![remove](http://ow2akcnvb.bkt.clouddn.com/remove.png)
* 点击 Remove 按钮之后会看到让输入项目名称确认删除的提示
![confirm](http://ow2akcnvb.bkt.clouddn.com/confirm.png)
* 输入项目名称，并且点击 confirm 确认按钮之后，项目就会被删除啦~~

### 重命名 GitLab Project
* 如果需要重命名，可以在这里操作
![rename](http://ow2akcnvb.bkt.clouddn.com/rename.png)




