> **`vue的生命周期，以及相应的特点`**

> **`Vue.use`**

安装 Vue.js 插件。
* 如果插件是一个对象，必须提供 install 方法。
* 如果插件是一个函数，它会被作为 install 方法。
* install 方法调用时，会将 Vue 作为参数传入。该方法需要在调用 new Vue() 之前被调用。
* 当 install 方法被同一个插件多次调用，插件将只会被安装一次。

> **`v-model 原理`**

VUE实现双向数据绑定的原理就是利用了 Object.defineProperty() 这个方法重新定义了对象获取属性值(get)和设置属性值(set)的操作，实现了数据劫持。

> **`watch的实现原理`**

> **`diff算法的原理`**

参考文档：[详解diff的算法](https://www.cnblogs.com/wind-lanyan/p/9061684.html)

1. newVnode和oldVnode进行同层级比较
2. 判断是否是相同节点
	- 相同节点，值得比较
		- 找到对应的真实dom，称为el
		- 判断Vnode和oldVnode是否指向同一个对象，如果是，那么直接return
		- 如果他们都有文本节点并且不相等，那么将el的文本节点设置为Vnode的文本节点。
		- 如果oldVnode有子节点而Vnode没有，则删除el的子节点
		- 如果oldVnode没有子节点而Vnode有，则将Vnode的子节点真实化之后添加到el
		- 如果两者都有子节点，则执行updateChildren函数比较子节点，这一步很重要
	- 不同节点，不值得比较
		- 直接替换
