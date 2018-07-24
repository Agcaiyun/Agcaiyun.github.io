---
layout:           post
title:            深浅拷贝
subtitle:         深浅拷贝详解  
date:             2018-07-24 
anthor:           caiyun
header-img:       img/18-04-01-header.jpg 	 
catalog:          true
tags:
    - JavaScript
---

## 内置类型
JS 中有其中内置类型，分为基本类型和对象*对象又叫做引用类型*，其中基本类型有六种，分别为：`null` `undefined` `boolean` `number` `string` `symbol`
* 字符串在一些其他语言中是被当做对象使用的，属于引用类型，但在js里是基本类型
* string类型的实际值还是存储在堆内存中的，但是js把string当做基本类型来处理 ，不存在引用值的情况

## 堆内存 与 栈内存
保存在**栈内存**中的数据必须是大小固定的数据，所以**基本数据类型**保存在栈内存中，而**引用类型**的大小不固定，只能保存在**堆内存**中，但是我们可以把引用类型的地址写在栈内存中供我们访问

## 浅拷贝
浅拷贝：浅拷贝是拷贝引用，拷贝后的引用都是指向同一个对象的实例，彼此之间的操作会互相影响

如下代码为*浅拷贝*的一个例子

```
var color1 = ['red','green'];
var color2 = color1;//拷贝
console.log(color2)//['red','green'];
color1.push('black') ;//改变color1的值
console.log(color2)//['red','green','black']
```
因为我们只是拷贝了引用类型的地址，而不是真正的该地址对应的基本类型的值，所以，不管是操作 color1 还是 color2 ，本质上都是**操作同一个数组对象**

此时：该拷贝的含义在内存中的表现为：
![shallowCopyGraph](http://ow2akcnvb.bkt.clouddn.com/shallowCopyGraph.png)
对数组的操作中，`concat` `slice` 方法也是浅拷贝，所以在用的时候要注意对原数组的保护


## 深拷贝
深拷贝：深拷贝不是简单的拷贝引用，而是在堆中重新分配内存，并且把源对象实例的所有属性都进行新建拷贝，以保证深拷贝的对象的引用图不包含任何原有对象或对象图上的任何对象，拷贝后的对象与原来的对象是完全隔离的


深拷贝在内存中的表现为：
![deepCopyGraph](http://ow2akcnvb.bkt.clouddn.com/deepCopyGraph.png)
这时候，Array2 虽然原本是由 Array1 拷贝来的，但是把 Array1 这个引用类型上的属性和实例一起在堆内存中拷贝了一份，Array2 的引用指向新的堆内存，这时候再改变 Array1 或 Array2 中的属性或实例的时候，就不会再互相影响了

### JSON对象的parse和stringify
JSON 对象是 ES5 中引用的新类型（支持的浏览器为IE8），JSON 对象 parse 方法将 JSON 字符串反序列化为 JS 对象，stringify 方法可以将 JS 对象序列化成 JSON 字符串，借助这个方法，可以实现对象的深拷贝。

代码示例为：
```
var source = {
    name:"source",
    child:{
        name:"child"
    }
}
var target = JSON.parse(JSON.stringify(source));
//改变target的name属性
target.name = "target";
console.log(source.name);   //source
console.log(target.name);   //target
//改变target的child
target.child.name = "target child";
console.log(source.child.name);  //child
console.log(target.child.name);  //target child
```

从代码输出可以看出，拷贝后的 target 与 source 完全隔离，两者之间不会再互相影响。

该方法用法较为简单，可以满足基本的深拷贝需求，而且能够处理 JSON 格式表示的所有数据类型，但是对于*正则表达式* *函数类型* 等**无法进行深拷贝**（而且会直接丢失相应的值），同时如果*对象中*存在*循环引用*的情况，也**无法正确处理**

### lodash中的_.clone()和_.cloneDeep()
* _.clone(value)
    * 创建一个 value 的浅拷贝
    * 支持 arrays、array buffers、 booleans、 date objects、maps、 numbers， Object objects, regexes, sets, strings, symbols, 以及 typed arrays
    * 参数对象的可枚举属性会拷贝为普通对象
    * 一些**不可拷贝**的对象，例如：error object、functions、DOM nodes 以及 WeakMaps 会返回空对象

* _.cloneDeep(value)
    * 这个方法 除了会递归拷贝 value，其他与 _.clone 类似

```
let arr = {
    name: 'arr',
    length: '100',
    width: '1000',
	brr: {
		a: 1,
        b: 2,
        c: 3,
        d: {
            aa: 11,
            bb: 22,
            cc: 33,
            dd: 44,
            ee: 55
        }
    }
}

let array1 = _.cloneDeep(arr)

array1.brr.d.aa = 123

array1.brr.d.aa    // 123
arr.brr.d.aa      // 11
 
```

### jQuery中的extend复制方法
jQuery 中的 extend 方法可以用来扩展对象，这个方法可以传入一个参数：`deep``(true or false)`表示是否执行深拷贝（如果是深拷贝则会执行递归拷贝）

这个方法的基本思路就是如果碰到 array 或者 object 的属性，那么就执行递归复制，这也导致了对于 *Date* *Function* 的引用类型 **无法支持**

### 参考文献
* https://yuchengkai.cn/docs/zh/frontend/
* https://segmentfault.com/a/1190000008838101
* https://www.cnblogs.com/tracylin/p/5346314.html