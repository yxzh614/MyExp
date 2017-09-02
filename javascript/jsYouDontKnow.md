# 上卷
## Part 2
### This

This 更优雅的方式来隐式传递一个对象引用引用

#### 几种绑定方式
1. 默认绑定

    不适用于其他方式时使用的绑定方式。

    绑定至全局变量。在`use strict`模式下绑定至`undefined`。

2. 隐式绑定


    ```
    function foo() {
        console.log(this.a)
    }

    var obj = {
        a: 2,
        foo: foo, //这里只是对foo的一个引用
    }

    obj.foo() //2 在对象上调用
    ```
    在对象上调用，将this绑定到这个对象上。

