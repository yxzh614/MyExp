# 深入理解JavaScript

### 笔记

_原文地址：http://www.cnblogs.com/tomxu/archive/2011/12/15/2288411.html_

## 1. 编写高质量JavaScript代码的基本要点

#### var

变量提升

通过var创建的全局变量（任何函数之外的程序中创建）是不能被删除（delete）的。

无var创建的隐式全局变量（无视是否在函数中创建）是能被删除的。

#### for

 循环操作 （例如循环DOM，数组）将长度缓存 提升性能
```
for (var i = 0, max = myarray.length; i < max; i++) {
   // 使用myarray[i]做点什么
}
```

for循环的变形：

```
    //第一种变化的形式：
    var i, myarray = [];
    for (i = myarray.length; i–-;) {
       // 使用myarray[i]做点什么
    }

    var myarray = [],
    i = myarray.length;
    while (i–-) {
       // 使用myarray[i]做点什么
    }
```
#### for-in
for-in循环应该用在非数组对象的遍历上，使用for-in进行循环也被称为“枚举”。

也可用在数组上，但是数组的额外属性也会被枚举。并且不能保证顺序。

会枚举原型链上的属性。可以使用`hasOwnProperty()`过滤掉原型的属性。

使用`Object.prototype.hasOwnProperty.call()`来避免内部有新的`hasOwnProperty`。

不进行过滤可以提高速度。

#### 避免隐式类型转换

始终使用===和!==操作符。

#### eval()

不要使用。

_eval is devil._

同理在任何以字符串形式插入代码的情况（函数构造等）都要避免。

#### parseInt()

第二个参数指定进制，不要忽略。

其他转换至数字的方法：
```
+"08" // 结果是 8
Number("08") // 8
```
这些方法通常比`parseInt()`要快，后者并不是简单的转换。
```
parseInt("8isme") // 8
+ "8isme" //undefined
Number("8isme") //undefined