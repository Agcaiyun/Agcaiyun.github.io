---
layout:           post
title:            markdown 语法
subtitle:         常用md语法总结
date:             2018-07-20
anthor:           caiyun
header-img:       img/17-10-02-header.jpg 
catalog:          true
tags:             
    - Tools
---

<a href="http://wowubuntu.com/markdown/">markdown语法学习网址</a>

## 兼容 HTML
* 不在 Markdown 涵盖范围之内的标签，都可以直接在文档中用 HTML 撰写。
* 要制约一些如 `<div>` `<table>` `<pre>` `<p>` 等标签，必须在**前后加上空行**与其他内容区隔开，并且要求他们的开始标签和结尾标签**不能用制表符或空格**来缩进。
* HTML 的区段（行内）标签如 `<span>` `<cite>` `<del>` 可以在 Markdown 的段落、列表或是标题里随意使用。依照个人习惯，甚至可以不用 Markdown 格式，而直接采用 HTML 标签来格式化。举例说明：如果比较喜欢 HTML 的 `<a>` 或 `<img>` 标签，可以直接使用这些标签，而不用 Markdown 提供的链接或是图像标签语法。

* 和处在 HTML 区块标签间不同，Markdown 语法在 HTML 区段标签间是有效的。    比如：  
    ```
    aaa
    
    <table>
        <tr>
            <td>aa</td>
            <td>aa</td>
            <td>aa</td> 
        </tr>
        <tr>
            <td>aa</td>
            <td>aa</td>
            <td>aa</td>   
        </tr>
    </table>
    
    aaa
    ```
    在预览模式下看到的会是：
    
    aaa
    
    <table>
        <tr>
            <td>aa</td>
            <td>aa</td>
            <td>aa</td> 
        </tr>
        <tr>
            <td>aa</td>
            <td>aa</td>
            <td>aa</td>   
        </tr>
    </table>
    
    aaa


## 区块引用 Blockquotes
* 区块引用可以嵌套（例如：引用内的引用），志瑶根据层次加上不同数量的　`>`
    ```
    > 我是第一层引用
    >
    > > 我是第二层引用
    >
    > 我是第一层引用
    ```     
    将显示为：
    
    > 我是第一层引用
    >
    > > 我是第二层引用
    >
    > 我是第一层引用

* 引用的区块内，也可以使用其他的 Markdown 语法，包括标题、列表、代码区块等

    ```
    > ## 这是一个标题。
    > 
    > 1.   这是第一行列表项。
    > 2.   这是第二行列表项。
    > 
    > 给出一些例子代码：
    > 
    >     return shell_exec("echo $input | $markdown_script");
    ```
    
    显示为：
    
    > ## 这是一个标题。
    > 
    > 1.   这是第一行列表项。
    > 2.   这是第二行列表项。
    > 
    > 给出一些例子代码：
    > 
    >     return shell_exec("echo $input | $markdown_script");


## 列表
* 列表项目可以包含多个段落，每个项目下的段落必须缩进四个空格或者一个制表符
    ```
    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.
    
        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.
    
    2.  Suspendisse id sem consectetuer libero luctus adipiscing.
    ```
    显示为：
    
    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.
    
        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.
    
    2.  Suspendisse id sem consectetuer libero luctus adipiscing.

* 如果要在列表项目内放入引用，那 `> ` 就要缩进  
    ```
    1. A list item with a blockquote:
        > This is a blockquote
        > inside a list item.
    2. Another ltem with a blockquote:
    > 这个引用没有缩进，就会是一个单独的引用而不是在列表内的引用
    ```
    
    显示为：
    
    1. A list item with a blockquote:
        > This is a blockquote
        > inside a list item.
        
    2. Another ltem with a blockquote:
    > 这个引用没有缩进，就会是一个单独的引用而不是在列表内的引用


* 如果要放代码块的话，该区块就要缩进**两次**，也就是*8个空格或者2个制表符*

    ```
    * 这是个列表，其中包含一个代码块
            
            我是一个代码块，我前面有两个制表符
    ```
    显示为：
    * 这是个列表，其中包含一个代码块
            
            我是一个代码块，我前面有两个制表符

## 数字-句点-空白
*   如果在行首出现  数字-句点-空白 的情况，会被 Markdown 视为有序列表，为了避免这样的状况，我们可以在句点前面加上反斜杠.

    比如：
    ``` 
    1. happy
    2. honey

    1\. happy
    2\. honey
    ```
    
    显示为：

    1. happy
    2. honey

    1\. happy
    2\. honey
    
## 代码区块
* 在 Markdown 中，只需要简单地缩进4个空格或者1个制表符，就可以了。
    比如：
    ```
    Here is an example of AppleScript:

    tell application "Foo"
        beep
    end tell
    ```
    显示为：
    
    Here is an example of AppleScript:
    
        tell application "Foo"
            beep
        end tell
        
## 分割线
* 可以在一行中用三个以上的星号、减号、底线来建立一个分割线，行内不能有其他东西。或者也可以在星号或者减号中间插入空格。
    比如：
    ```
    * * *
    ***
    ******
    ---
    - - -
    __________________
    ```
    显示为：
    
    * * *
    ***
    ******
    ---
    - - -
    __________________

## 链接
* 要建立一个行内式的链接，只需要在方括号后面紧跟着圆括号并插入网址链接即可。如果还想要加上链接的 title 文字，只需要在网址后面用双引号把 title 文字包起来即可。

    比如：
    ```
    This is [an example](http://example.com/ "Title") inline link.
    
    [This link](http://example.net/) has no title attribute.
    ```
    显示为：
    
    This is [an example](http://example.com/ "Title") inline link.
    
    [This link](http://example.net/) has no title attribute.
    
* 如果是要链接到同样主机的资源，可以使用相对路径

    比如：
    ```
    See my [about](/about/ "Title")  page for details.
    ```
    显示为：
    
    See my [about](/about/ "Title")  page for details.
    
## 其他链接
* Markdown 支持以比较简短的自动链接形式来处理网址和电子邮件信箱，只要是用尖括号包起来， Markdown就会自动把它转成链接。一般网址的链接文字就和链接地址一样
    比如：

    ```
    <http://example.com/>
    
    <address@example.com>
    ```
    
    显示为：
    
    <http://example.com/>
    
    <address@example.com>
    
    
## 代码

* 如果要在代码区段中插入反引号，可以用多个反引号开启和结束代码片段

    比如：
    ```
    ``This is a literal backtick (`) here ``
    ```
    显示为：
    
     ``This is a literal backtick (`) here ``
* 代码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号

    ```
    A single backtick in a code span: `` ` ``
    ```
    显示为：
    
    A single backtick in a code span: `` ` ``
    
## 反斜杠
* Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号
* Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

```
\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
```

