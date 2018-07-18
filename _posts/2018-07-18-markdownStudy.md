[参考网址](https://www.cnblogs.com/nifengs/p/5104763.html)

location 是 JavaScript 中管理地址栏的内置对象，比如 location.href 管理页面的 url，用 location.href = newUrl 就可以直接将页面重定向到新的 url。而 location.hash 则是可以用来获取或设置页面的标签值。比如 http://domain/#admin 的 location.hash = '#admin'。

## window.location.hash 简单应用
### #的含义
`#`代表网页中的一个位置。其右面的字符就是该位置的标识符。比如：http://www.example.com/index.html#print 就代表网页中 index.html 的 print 位置。浏览器读取这个 url 后，会自动将 print 位置滚动到可视区域。

为网页位置指定标识符，有两个方法。一是使用锚点，比如`<a name="print"></a>`，二是使用id属性，比如`<div id="print" >`。

### HTTP请求不包括#
`#`是用来指导浏览器动作的，对服务器端完全无用。所以，HTTP请求中不包括#。

比如，访问下面的网址:

　　http://www.example.com/index.html#print

浏览器实际发出的请求是这样的：

　　GET /index.html HTTP/1.1

　　Host: www.example.com

可以看到，只是请求 index.html，根本没有 "#print" 的部分。

### #后的字符

在第一个#后面出现的任何字符，都会被浏览器解读为位置标识符。这意味着，这些字符都不会被发送到服务器端。

比如，下面URL的原意是指定一个颜色值：

　　http://www.example.com/?color=#fff

但是，浏览器实际发出的请求是：

　　GET /?color= HTTP/1.1

　　Host: www.example.com

可以看到，"#fff"被省略了。只有将#转码为%23，浏览器才会将其作为实义字符处理。也就是说，上面的网址应该被写成：

　　http://example.com/?color=%23fff
　　
### 改变#不触发网页重载

单单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页。

比如，从

　　http://www.example.com/index.html#location1

改成

　　http://www.example.com/index.html#location2

浏览器不会重新向服务器请求index.html。

### 改变#会改变浏览器的访问历史

每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用"后退"按钮，就可以回到上一个位置。

这对于ajax应用程序特别有用，可以用不同的#值，表示不同的访问状态，然后向用户给出可以访问某个状态的链接。

值得注意的是，上述规则对IE 6和IE 7不成立，它们不会因为#的改变而增加历史记录。

### window.location.hash读取#值

window.location.hash这个属性可读可写。读取时，可以用来判断网页状态是否改变；写入时，则会在不重载网页的前提下，创造一条访问历史记录。