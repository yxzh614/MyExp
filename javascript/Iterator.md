# 理解JavaScript-Iterator

> ES6标准入门学习笔记

Iterator（遍历器接口）提供了一种访问机制，部署了该接口的数据结构可以实现遍历功能。（称为可遍历的）

Iterator的作用有三个：

* 为各种数据提供统一、方便的接口
* 按次序访问数据结构的成员
* ES6中的新语法：for of

Itreator的用法：每次调用next方法都会返回数据结构中的下一个成员直到结束。

返回值的格式为`{value: value, done: false}`。其中value为返回的数据值，done为是否还有下一个元素。

## 默认Iterator接口

什么样的数据解构是“可遍历的”？

ES6规定，默认的遍历器接口定义在数据结构的Symbol.iterator属性。只要数据结构具有这个属性，就可以认为它是可遍历的。

example：

``` javascript
const o = {
  let num = 0;
  [Symbol.iterator]: function () {
    return {
      next: function () {
        return {
          value: num++,
          done: false
        }
      }
    }
  }
}
//无限返回+1后的值。
//【执行】Symbol.iterator属性就会返回一个遍历器对象。
//该属性只是一个函数。
//遍历器对象上的next方法用于返回值。
```

原生具备遍历器属性的数据结构有：

* Array
* Map
* Set
* String
* TypedArray
* arguments对象
* NodeList对象

对象Object是没有这个属性的，因为对象中的属性通常是无序的。

对于类似数组的对象，因为它有着和数组类似的结构但没有实现遍历器，可以直接将`[][Symbol.iterator]`部署到对象的`Symbol.itreator`上来实现遍历器接口。

## 调用Iterator的场合

* 解构赋值
* 扩展运算符
* yield*
* 接受数组作为参数的场合
* for of

## return和throw

除了next方法外，遍历器还具有return和throw方法。这两个是可选的。

return方法是在遍历过程发生提前退出时调用的方法。必须返回一个对象。

throw是用来配合Generator函数使用的。

## 计算法

遍历器对象上有entries、keys、values三个方法，分别是返回键值对、返回键、返回值的方法，数组、Set、Map遍历时一般选择其中一种方式来返回值。

## for of 循环

for of 可以对部署了遍历器接口的数据结构进行遍历。

1. 数组

``` javascript
const arr = ['a', 'b', 'c']
for (let v of arr) {
  console.log(v)
}
// a b c
```

for of 遍历数组时只返回索引对应的值，没有该数组作为对象拥有的其他属性。for in 则会遍历arr.foo此类属性。

2. Set&Map

遍历顺序为先入先遍历，Set返回的时一个值，Map返回的是一个数组[key, value]。

3. 类数组对象

其中已经部署遍历器接口的可以直接使用for of，未部署的可以先转换成数组再使用for of。

4. 对象

for in 可以直接遍历键名，for of需要部署遍历器接口才能使用。

解决办法：使用Object.keys(o)来生成数组。使用Generator函数包装（见下期）

## 其他的遍历方法

1. for循环遍历：最基础，最麻烦。
2. forEach方法：略简单，不能跳出。
3. for in ：数组for in遍历的是索引;数组for in会遍历其他手动添加的键以及原型链上的键；不能保证顺序。
4. for of 语法简洁，行为统一

总结：遍历器接口为JavaScript提供了一个统一的数据结构操作方法，有助于编写更加严格的数据结构，提升了代码的稳定性。

参考：ES6标准入门（第三版） 阮一峰 著