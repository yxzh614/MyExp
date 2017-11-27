# 考核2

二阶段开始JS的学习，没有编程基础的人可以从等级1开始看起，对自己能力有信心的可以跳过前面的部分。

## 等级1

### a 语言本身：

* 知道什么是语句
* 学会常见的操作符（+-*/%!=:?）的使用
* 学会常见关键字（if,else,for,while,switch,var,function,return）的使用
* 知道js的数据类型

### b 熟悉以下代码结构：

* 顺序结构
* 分支结构
* 循环结构

## 等级2

知道对象的概念，对象上简单的操作

  对象（object）是一种数据类型，区别于一般的数据类型，其持有**属性**，几乎任何一个对象都长成这样：
  ```javascript
  {
    attr1: 'value1',
    attr2: 'value2',
  }
  ```
  基本写法为一对花括号包裹，里面是“属性名`:`值”，“`,`”作为分隔符
  _也可以作为结束符（在最后一条属性后面也加上逗号）方便插入删除属性。_

  属性可以理解为“对象所拥有的变量”，也就是说属性也拥有自己的数据类型，它可以是普通的数字，也可以是另一个对象甚至是函数

### 等级3

函数的简单理解与使用

函数是可以执行的一段子程序，一般长这样：

```javascript
function myFunction() {
  console.log('it is running')
}
myFunction()
```

* 声明与调用

声明：函数声明 函数名（参数表） { 语句体 }

调用：函数名（传入的参数）

声明是指在程序中说明一个可用的名字，让你在想用它的时候真的可以用，function是专门用于声明函数的。

调用指的是作为函数调用，`myFunction`和`myFunction()`的区别是前者获得变量的值，后者对这个函数进行调用后获得执行结果（内部的return）

参数相当于在内部定义的变量，并且在调用时自动将传入的参数赋值给对应的参数。

* 返回值

返回值代表着内部的代码执行完了之后返回给外部的一个值，这个值可以是任何类型。对于没有return语句或者有但是没有执行的函数调用将会返回`undefined`

！一些高级函数用法：

* 递归

```javascript
function foo(n) {
  if(n) return n * foo(--n)
  return 1
}
//计算n的阶乘
```

* 回调函数

```javascript
function foo() {
  return function callBack() {
    console.log('this is call back')
  }
}
foo()()
//返回值为函数
```

* 立即执行函数

```javascript
(function foo() {
  console.log('run immediatly')
})()
//也可以这样套括号：(function foo(){}())
```

* 匿名函数

```javascript
function useTwice(func) {
  func()
  func()
}
useTwice(function () {
  console.log('boom!')
})  //boom!boom!

```

### 等级4

#### DOM操作

DOM(document object model)指的是浏览器的文档对象模型，简单讲对于网页中展示出的树型结构的元素提供了一组方法来对其进行操作，常见的有节点的增删查改。