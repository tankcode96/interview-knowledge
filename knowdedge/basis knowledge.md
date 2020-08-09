>### **js 基本数据类型**
共七种，Number、String、Boolean、BigInt、Symbol、Null、Undefined

>### **js 复杂数据类型**
共一种，Object

>### **判断数据类型的方法**
共四种方式，分别是
- typeof
```js
typeof ${操作数}
// or
typeof(${操作数})

注意：
// typeof null将返回object。因为在 JS 的最初版本中，使用的是 32 位系统，为了性能考虑使用低位存储了变量的类型信息，000 开头代表是对象，然而 null 表示为全零，所以将它错误的判断为 object，然后被 ECMAScript 沿用了 。
// typeof不能准确判别对象类型究竟是什么具体对象。
```
- instanceof
```js
'abc' instanceof String // false
new String('abc') instanceof String // true
// 基本类型的数据使用instanceof始终判断false，因为基本类型不是对象

注意：
(() => {}) instanceof Function // true
(() => {}) instanceof Object // true
null instanceof Object // false
```
- constructor 判断原型的构造函数
```js
[].constructor === Array // true
123.constructor === Number // true
null.constructor // TypeError
undefined.constructor // TypeError
···

注意：
// null和undefined是无效的对象，因此是不会有constructor存在的，这两种类型的数据可以通过第四种方法来判断。
// JS对象的constructor是不稳定的，这个主要体现在自定义对象上，当prototype被重写后，原有的constructor会丢失，constructor会默认为Object
```
- prototype 判断原型
```js
// 此方法适用于所有的类型判断
Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1')
```

>### **重排和重绘**
当DOM的变化引发了元素几何属性的变化，比如改变元素的宽高，元素的位置，导致浏览器不得不重新计算元素的几何属性，并重新构建渲染树，这个过程称为“重排”。完成重排后，要将重新构建的渲染树渲染到屏幕上，这个过程就是“重绘”。

>### **从输入URL到页面加载的过程**
[深度广度俱佳的解答](https://segmentfault.com/a/1190000013662126)

>### **Event loop 事件循环**
主线程循环不断地从任务队列中读取事件，这种运行机制成为事件循环。

>### **原型**
- 碧霞：每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性
- 坤明：每个实例的构造函数都有一个指针(prototype)指向一个对象，这个对象就是原型，原型具有属性，而实例会继承原型的属性。

>### **原型链**
对象通过隐式属性__proto__指向父类原型，直到指向Object原型为止，这样就形成了一个原型指向的链条，专业术语称之为原型链。

>### **闭包**
闭包是指有权访问另一个函数作用域中的变量的函数。创建闭包的常见方式就是在一个函数内部创建另一个函数。

>### **BFC**
[BFC的解释](https://blog.csdn.net/sinat_36422236/article/details/88763187 '什么是BFC')

块格式化上下文，是块盒子布局过程发生的区域，也是浮动元素与其它元素交互的区域。
- BFC如何产生呢？
  - 根元素，即HTML标签
  - float的值不为none
  - position的值不为static或relative
  - overflow的值不为visible
  - display的值为inline-block 、table-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid 
- BFC有什么特性呢？
  - 内部元素会在垂直方向上一个接一个的排列
  - 垂直方向上，属于同一个BFC的两个相邻的盒子的margin会重叠
  - 子元素不会超出包含它的块
  - BFC的区域不会与float元素的区域重叠
  - 计算BFC的高度时，浮动的子元素也参与计算
  - BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然

>### **类和继承（es5实现方法 + es6实现方法）**
ES5实现方法：
- 原型链继承
  - 缺点：
    - 每个实例对**引用类型**属性的修改都会被其他的实例共享
    - 创建的实例无法自定义自己的属性

- 借助构造函数继承
  - 优点：
    - 解决了每个实例对引用类型属性的修改都会被其他的实例共享的问题
    - 子类可以向父类传参
  - 缺点：
    - 无法复用父类的公共函数
    - 每次子类构造实例都得执行一次父类函数

- 原型链继承和借用构造函数合并
  - 优点:
    - 解决了每个实例对引用类型属性的修改都会被其他的实例共享的问题
    - 子类可以向父类传参
    - 可实现父类方法复用
  - 缺点:
    - 需执行两次父类构造函数，第一次是Child.prototype = new Parent()，第二次是Parent.call(this, name)造成不必要的浪费

- 原型式继承
  - 缺点：
    - 每个实例对引用类型属性的修改都会被其他的实例共享
- 寄生式继承
  - 缺点：
    - 无法复用父类函数，每次创建对象都会创建一遍方法
- 寄生组合式继承
  - 缺点：
    - 不必为了指定子类型的原型而调用父类型的构造函数
ES6实现方法：
  - 通过类的extends关键字来实现继承

>### **promise**
promise 是异步编程的一种解决方案：从语法上讲，promise是一个对象，从它可以获取异步操作的消息；promise有三种状态：pending(等待态)，fulfiled(成功态)，rejected(失败态)；状态一旦改变，就不会再变。

promise主要是用来解决两个问题：
1. 回调地狱
2. 代码中需要严格控制执行顺序的部分

>### **前端性能优化**
- http层
  - DNS解析缓存
  - tcp连接，可用http2.0，进行多路复用、使用二进制格式、压缩请求包
  - 减少http请求数
  - 文件适当合并
  - 图片合并，使用雪碧图
  - 适当使用懒加载
- 缓存
  - 强缓存 expires设置过期时间、cache-control
  - 协商缓存 Last-Modified/If-Modified-Since、Etag/If-None-Match
- 浏览器渲染
  - 脚本文件后移，放在body标签的底部
  - 减少重排和重绘

>### **跨域**
只要`协议`，`域名`，`端口`有任何一个的不同，就被当作是跨域
- jsonp
  - 服务器返回一个脚本文件，里面是一个回调函数和回调函数的json格式的参数
  - 执行脚本文件里的回调，进行请求，获得数据
- 服务器代理
  - 服务器没有不存在跨域问题，通过服务器去代替浏览器去请求资源，可以实现跨域
- 服务器设置Access-Control-Allow-Origin HTTP响应头
- 通过document.domain+iframe来跨子域(只有在主域相同的时候才能使用该方法)
  - 主域名相同的情况下设置document.domain

>### **cookie、session、sessionStorage、localStorage**

>### **let const var**
- var
  - 只有全局作用域和函数作用域的概念，没有块级作用域的概念
  - 存在`变量提升`的特性
  - 允许重复声明
- let、const
  - 只有块级作用域的概念
  - 在当前作用域顶部到变量声明位置之间，存在`暂时性死区`
  - 不允许重复声明
  - const 变量一旦被赋值，就不可以再赋值，并且在声明时必须经过初始化

>### 事件流
事件流描述的是从页面中接受事件的顺序，**IE的事件流是事件冒泡流(event bubbling)，而Netscape的事件流是事件捕获流(event capturing)**

>### DOM事件流
 ‘DOM2级事件’规定的事件流包含3个阶段，`事件捕获阶段`、`处于目标阶段`、`事件冒泡阶段`。首先发生的事件捕获为截获事件提供机会，然后是实际的目标接收事件，最后一个阶段是事件冒泡阶段，可以在这个阶段对事件做出响应。

>### **事件代理**
- 本来应该加在子元素身上的事件，我们却把事件加在了其父级身上，通过查找event对象里记录的事件源可以知道发生事件的子元素。
- 好处：
  - 第一个好处是效率高，比如，不用for循环为子元素添加事件了
  - 第二个好处是，js新生成的子元素也不用新为其添加事件了，程序逻辑上比较方便


>### **冒泡和捕获**
冒泡和捕获分别是IE和网景提出的两种事件流的概念。
  - 事件冒泡，即事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点
  - 事件捕获，即不太具体的DOM节点应该更早接收到事件，而最具体的节点应该最后接收到事件
