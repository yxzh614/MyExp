### C2

`defer` 属性 

脚本会被延迟到整个页面解析完毕后执行 

* 不能保证顺序

`async` 属性

异步脚本，一定会在load事件前执行

* 不要修改DOM

~~script内部的javascript代码可以用注释包含，但一样可以执行~~

noscript标签用于浏览器没有开启脚本时的提示信息

### C3

* 永远区分大小写
* 标识符以字母 、_ 、$ 开头
* 首字母小写其他单词大写
* `"use strict"`严格模式

数据类型：

* undefined
* null
* boolean
* number
* string
* object
* 
`typeof` 操作符

是一个操作符，可以直接后面接表达式，或者使用函数调用。

不推荐使用

1. undefined

    未声明的

    **如果将undefined赋值给变量，那么这个变量其实不是未声明的，只不过取其值会得到undefined。其在RHS和LHS中不会报错。**

2. null

    一般只有直接的赋值才会产生null，通常用作空对象指针。

3. boolean

    所有的值都可以转换成boolean

| 类型      | ToTrue               | ToFalse     |
| --------- | -------------------- | ----------- |
| boolean   | true                 | false       |
| string    | 非空字符串           | ""          |
| number    | 非零值（包括无穷大） | 0和NaN      |
| object    | 任何对象             | null        |
| undefined | X                    | 永远是false |

4. number

    IEEE754

    1. 整数

        十进制 八进制0（严格模式无效） 十六进制0x

        计算时最终都会转成十进制

    1. 浮点数

        整值的浮点数会被自动解析成整数

        可用科学计数法e表示

        不准确：0.1+0.2!==0.3

        5e-324 ~ 1.7976931348623157e+308

        Number.MIN_VALUE === Number.NEGATIVE_INFINITY
        Number.MAX_VALUE === Number.POSITIVE_INFINITY

        NaN 非数字值 NaN!==NaN

        `isNaN()`

        有隐式转换

        `Number()` `parseInt()` `parseFloat()`

        `Number()`转换完全是十进制或十六进制的字符串。转换对象时先调用对象的`valueOf()`，然后再调用`toString()`按字符串处理。

        `parseInt()`从字符串首个非空格开始立即识别一个十进制或十六进制整数。忽视小数点
        -|-
        -|-
        ".1"  |  NaN
        "0x"   | NaN
        "0x1"  | 1
        "1.1"  | 1
        "s1"   | NaN

        添加第二个参数代表进制。

        `parseFloat()`遇到的第一个小数点有效。只解析十进制

5. string

    转义字符算一个长度


