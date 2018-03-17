# 理解Generator-语法

> ES6标准入门学习笔记

执行Generator函数会返回一个遍历器对象。

## 基本用法

``` javascript
function * foo() {
  yield 1
  yield 2
  return 3
}
let g = foo()
g.next() // {value: 1, done: false}
g.next() // {value: 2, done: false}
g.next() // {value: 3, done: true}
g.next() // {value: undefined, done: true}
```

每次调用next方法就会返回一次数据，即yield语句的值。done为true时即不再有下一次数据。

Generator函数的行为可以看作一个可遍历的数据结构的实现。

## yield

yield即Generator函数的暂停标志。

1. 外层代码执行next()
2. 内层代码运行至yield语句
3. 返回yield后的语句的值给外层代码，暂停执行内层代码
4. 继续外层代码
5. 内层没有剩下yield时运行至return语句或者函数结束，返回return的值或者undefined

yield不能用于普通函数中。

yield表达式如果用在另一个表达式中，其优先级低于除了括号、等号、形参之外的位置。需要时应添加圆括号。

## Generator与Iterator

Generator函数返回就是一个Iterator，因此其返回值可以直接赋值给`[Symbol.Iterator()]`

这个对象的`[Symbol.Iterator()]`就是它自身。

```javascript
g.[Symbol.Iterator()] === g //true
```

## next方法

next方法可以带有一个参数，作为上次next()所对应的yield语句的返回值。

```javascript
var out = 'out'
var get = yield out
next() //第一次next时，其返回值为yield右侧'out',内层函数暂停在赋值号右侧
next()
```

实际上yield作为右结合性运算符，首先接受右面的表达式的值传给外面，外面下一次调用next时再将传入的值作为自己的返回值继续运算，这样就实现了暂停的功能。

