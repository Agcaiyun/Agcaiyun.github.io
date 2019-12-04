---
layout:           post
title:            JS 实现二进制与十进制的相互转换
subtitle:         JavaScript 实现二进制与十进制的相互转换 
date:             2018-12-13
anthor:           caiyun
header-img:       img/2018-12-13-transform-header.jpg	 
catalog:          true
tags:
    - JavaScript
---

# JS实现十进制与二进制的互相转换

> 用 `javascript` 实现十进制与二进制之间的转换，在网上能找到不少例子，但很多都少考虑了**二进制小数**转换为十进制的情况，所以在一些摸索和实现之后，想把这种情况的实现分享给你

## 需求分析
* 二进制和十进制都可能是 *整数*和*浮点数（小数）*
* 当然也可能是正数和负数（因为负数只需提取一个负号（-），所以该文章以正数为例）

## 十进制转换为二进制
### 该转换可以用 toString() 方法来实现
* `toString()` 方法返回一个表示该对象的字符串
* 语法：`numberObject.toString(radix)`
    * 描述：把数字转换为对应的字符串
    * `radix`： 可选。规定表示数字的基数
    
* `radix`：2 ~ 36 之间的整数。若省略该参数，则使用基数 10。但是要注意，如果该参数是 10 以外的其他值，则 `ECMAScript` 标准允许实现返回任意值
* 返回值类型：`string`

所以，如果想将十进制数转换为二进制数（整数和小数都可以用这种方法），只需要使用 `numberObject.toString(radix)` 方法即可。
示例：
```
const decimalNum = 123 
console.log(decimalNum.toString(2))  // "1111011"
const decimalFloatNumber = 123.125
console.log(decimalFloatNumber.toString(2))  // "1111011.001"
```
因为 `toSting()` 返回的是表示该对象的**字符串**，所以如果最终结果是要二进制数值的话，可以再用 `Number()` 函数转换一下即可。

## 二进制转换为十进制
> 网上例子基本都是用 `parseInt(string, radix)`，但如果二进制数有小数部分，那小数部分的数值会被直接舍去，不符合一些场景的需求设定

实现二进制（整数部分&小数部分）转换为十进制的一种方法是：将二进制数分为整数和小数两部分，分别转换为十进制数，然后再组合成最终的十进制数值

### 二进制整数部分转换为十进制
这部分很简单，直接用 `parseInt(string, radix)` 就可以啦~

* `parseInt()` 函数可解析一个字符串，并返回一个整数
* `parseInt(string, radix)`
    * `string`：	必需。要被解析的字符串
    * `radix` ：     可选。表示要解析的数字的基数
* radix：该值介于 2 ~ 36 之间。如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。如果该参数小于 2 或者大于 36，则 `parseInt`() 将返回 `NaN`。

### 二进制小数部分转换为十进制
先不用代码实现，整理整理思路，根据转换原则，就是将小数点后的每位二进制数都转换成十进制数，然后将各个位的十进制数加起来，就是完整的小数部分的十进制数了。
比如：1111011.111 的小数部分为：111

转换过程为：

<table>
    <tr>
        <td>小数部分:</td>
        <td>1</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>基数的多少次幂:</td>
        <td>2^(-1)</td>
        <td>2^(-2)</td>
        <td>2^(-3)</td>
    </tr>
    <tr>
        <td>每位数字转换过程为：</td>
        <td>1 * (2^(-1)) </td>
        <td>1 * (2^(-2))</td>
        <td>1 * (2^(-3))</td>
    </tr>
    <tr>
        <td>用十进制数值表示为：</td>
        <td>0.5</td>
        <td>0.25</td>
        <td>0.125</td>
    </tr>
    <tr>
        <td>二进制小数部分转换为十进制数后为：</td>
        <td colspan="3" style="text-align: center">0.5 + 0.25 + 0.125</td>
    </tr>
</table>

对应代码实现为：
* 将二进制数的整数部分和小数部分分别取出
    * 先将二进制数转换为字符串
    * 用 `split` 方法，取出二进制数的整数部分和小数部分
```js
const binaryFloatNum = 1111011.111
const binaryFloatNumStr = binaryFloatNum.toString()
console.log(binaryFloatNumStr)  // "1111011.111"
const binaryFloatNumArr = binaryFloatNumStr.split(".")
console.log(binaryFloatNumArr)  // ["1111011", "111"]
```
* **将小数部分转换为十进制数**
    * 取出小数部分
    * 将小数部分的**每位**取出
    * 将取出的**每位**分别转换为十进制数
    * 将转换之后的各个十进制数相加，得到由整个二进制小数部分转换成的十进制数
    
```js
const binaryFloatPartStr = binaryFloatNumArr[1]  //  "111"
const binaryFloatPartArr = binaryFloatPartStr.split("")  //  ["1", "1", "1"]

/**
* 将 binaryFloatPartArr 数组中的每项转换为对应的小数部分的十进制数
* @param decimalArray 二进制小数部分中由小数各位组成的数组
*/
function eachBinaryFloatPartToDecimal (binaryFloatPartArr) {
    return binaryFloatPartArr.map((currentValue, index) => {
        return Number(currentValue) * Math.pow(2, (-(index + 1)))
    })
}

const eachDecimalFloatPartNum = eachBinaryFloatPartToDecimal(["1", "1", "1"])
console.log(eachDecimalFloatPartNum)  // [0.5, 0.25, 0.125]

/**
* 将 binaryFloatPartArr 数组中的每项转换为对应的小数部分的十进制数
* @param decimalArray 二进制小数部分中由小数各位组成的数组
*/
const deciamlFloatPartNum = eachDecimalFloatPartNum.reduce((accumulator, currentValue) => {return accumulator + currentValue})
console.log()  // 0.875
```
## 将整个二进制小数转换为十进制数的程序为：
> ps： 将下面程序复制到控制台可直接运行
```js
/**
* 将二进制小数部分转换为十进制数
* @param binaryFloatPartArr 二进制小数部分中由小数各位组成的数组
*/
function eachBinaryFloatPartToDecimal(binaryFloatPartArr) {
    return binaryFloatPartArr.map((currentValue, index) => {
        return Number(currentValue) * Math.pow(2, (-(index + 1)))
    })
}

/**
* 将二进制小数（包含整数部分和小数部分）转换为十进制数
* @param binaryNum 二进制数（可能是整数，也可能是小数）
*/
function binaryFloatToDecimal(binaryNum) {
    // 如果该二进制只有整数部分则直接用 parseInt(string, radix) 处理
    if (Number.isInteger(binaryNum)) {
        return parseInt(binaryNum, 2)
    } else {
        const binaryFloatNumArr = binaryNum.toString().split(".")

        // 将二进制整数转换为十进制数
        const binaryIntParStr = binaryFloatNumArr[0]
        const decimalIntPartNum = parseInt(binaryIntParStr, 2)

        // 将二进制小数部分转换为十进制数
        const binaryFloatPartArr = binaryFloatNumArr[1].split("")
        const eachDecimalFloatPartNum = eachBinaryFloatPartToDecimal(binaryFloatPartArr)
        const deciamlFloatPartNum = eachDecimalFloatPartNum.reduce((accumulator, currentValue) => { return accumulator + currentValue })
        return decimalIntPartNum + deciamlFloatPartNum
    }
}

console.log(binaryFloatToDecimal(1111011.111))  // 123.875
console.log(binaryFloatToDecimal(1111011))  // 123
console.log(binaryFloatToDecimal(0.111))  // 0.875
```
