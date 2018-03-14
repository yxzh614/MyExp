# 前端

作者：汪汪

链接：[知乎专栏](https://zhuanlan.zhihu.com/p/22606894)

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

* 前言

这篇文章是对我大四秋招以来面试的总结，里面包含前端面试知识的方方面面，目前本人已经拿到腾讯offer，希望能对后面找工作的学习学妹们有所帮助。腾讯面试对基础比较看重，然后需要你有两三个比较好的项目，一面重视面试者对前端基础的把握，还要手写代码，不过不难，二面部门的leader面，这一面比较难，面试官会对你的项目细节进行深挖，所以说项目要牛逼一点，最后还会有一道逻辑题（我没有答上来），三面是HR面，如果你想进大公司的话，下面这些技术是肯定要掌握的：html5，css3，JavaScript，略懂一点jQuery源码，Node.js，express，mongoose，数据库mongodb。大公司问的核心在于JavaScript。如果下面的知识点你都可以打上来，恭喜你拿下bat不是问题--2016-11-11写转载请注明出处，码这么多字不容易。

## 一、 HTML&CSS

### CSS盒模型

手写基本元素布局

box-sizing: 当你设置一个元素为 `box-sizing: border-box;` 时，此元素的内边距和边框不再会增加它的宽度。而是压缩内容区的宽度

背景显示在border上

7个水平属性的和通常为父级元素的width，其中只有左右外边距和width可以设置为auto。当计算的和无法满足父元素的width的时候，用户代理将右外边距重置为auto（从左向右的语言）,外边距可以设置负值

### HTML5新特性
(https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML)
#### 标签语义化

HTML5解决了如何为文档做出详细定义的问题（例如div标签语意混乱）
[HTML标签列表](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)

#### 使用音视频元素可以直接插入视频

`<video><audio>`

#### 对表单的改进

`<input>`标签拥有更多功能[在这里查看](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input)

#### 新增很多api，比如获取用户地理位置的window.navigator.geoloaction

#### websocket

#### 缓存

#### web worker

#### cookie，sessionStorage，localeStorage的区别

cookie是存储在浏览器端，并且随浏览器的请求一起发送到服务器端的，它有一定的过期时间，到了过期时间自动会消失。sessionStorage和localeStorage也是存储在客户端的，同属于web Storage，比cookie的存储大小要大有8m，cookie只有4kb，localeStorage是持久化的存储在客户端，如果用户不手动清除的话，不会自动消失，会一直存在，sessionStorage也是存储在客户端，但是它的存活时间是在一个回话期间，只要浏览器的回话关闭了就会自动消失。

#### 多个页面之间如何进行通信

使用cookie，使用web worker，使用localeStorage和sessionStorage

#### 浏览器的渲染过程

1. 根据html构建dom树
2. 根据CSSg构建render树
3. 构建布局树

#### 重构 回流

浏览器的重构指的是改变每个元素外观时所触发的浏览器行为，比如颜色，背景等样式发生了改变而进行的重新构造新外观的过程。重构不会引发页面的重新布局，不一定伴随着回流，回流指的是浏览器为了重新渲染页面的需要而进行的重新计算元素的几何大小和位置的，他的开销是非常大的，回流可以理解为渲染树需要重新进行计算，一般最好触发元素的重构，避免元素的回流；比如通过通过添加类来添加css样式，而不是直接在DOM上设置，当需要操作某一块元素时候，最好使其脱离文档流，这样就不会引起回流了，比如设置position：absolute或者fixed，或者display：none，等操作结束后在显示。

## JS

### 基本数据类型

### 基本关键字

### 闭包

利用作用域不可视原理

### new操作符

``` JavaScript
var a = new A()
//new操作符创建了一个新对象,并将左值的this指向这个对象
a.__proto__ === A.prototype // true

```

### call与apply

将fn函数内部的this指向obj:`fn.call(obj)`或`fn.apply(obj)`