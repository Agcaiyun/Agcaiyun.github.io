---
layout:           post
title:            如何用下面的div遮蔽上面的div
subtitle:         原谅我一生不羁放纵爱自由
date:             2017-12-20
anthor:           caiyun
header-img:       img/17-12-20-header.jpg 
catalog:          true
tags:             
    - css
---


> 有时候兄弟 div 之间的遮蔽（或者说覆盖，重叠）是我们需要避免或者需要解决的问题，但是有时候也需要故意实现这种效果
> 缘起：今天因为工作，需要完成两个兄弟 div 互相遮蔽的效果，走了一些弯路，所以在这里记录一下，希望能给你一些帮助

* 需求很简单，可以简单用下图来表示：
![image.png](http://upload-images.jianshu.io/upload_images/6970677-7a588b4bcb5cfd21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 需要实现的效果如下图：
![image.png](http://upload-images.jianshu.io/upload_images/6970677-9c110968b32eb8ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 实现过程分析：
实现这样的效果很快就会想起用 `position` 定位，最常用的是 `relative` 和 `absolute`有句口诀是：`子绝父相`，意思是：父亲相对定位，孩子相对于父亲绝对定位，这样孩子就可以在父亲容器中定位实现需要的布局效果，但是现在 `div1`  `div2` 是兄弟关系，而 `position:absolute` 的定位是相对于除了 `static` 定位以外的**父元素**进行定位的，并且 `div1` 宽高不能确定，所以只靠这两个 `div` 不太容易实现，那就可以给这两个 `div` 一个共同的父亲，父亲相对定位，`div2` 相对父亲绝对定位，并且绝对定位的 `top` `right` `bottom` `left` 都为零，这样就完全覆盖了父亲，因为 `position:absolute` 会使元素脱离标准文档流，所以 `div2` 不会占用标准文档流的空间，所以 `div2` 盖住了父元素也就是盖住了 `div1`，这样就实现了兄弟元素中 `div2` 对 `div1` 的全遮蔽效果

* 上代码
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .parent {
            position: relative;
        }

        .up {
            background: red;
            color: #fff;
        }

        .down {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            background: #000;
            opacity: 0.7
        }
    </style>
</head>

<body>
    <div class="parent">
        <div class="up">
          我只是随意写的一些文字,用于将 div1 撑开,我的多少决定了 div1 能被撑开多少,也就是 div1 的宽高由这些文字的多少来决定而不是给定的数值
        </div>
        <div class="down">
        </div>
    </div>
</body>

</html>
```
* 实现效果如下如：
> 为了便于区分 div2 是否完全覆盖了 div1 在代码中用了 opacity 属性

![image.png](http://upload-images.jianshu.io/upload_images/6970677-2f01888bb18a7ecf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 你可以试着添加更多的文字，看看是否还会是完全覆盖的~~

