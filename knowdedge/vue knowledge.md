### vue的生命周期，以及相应的特点

### **Vue.use**
安装 Vue.js 插件。
- 如果插件是一个对象，必须提供 install 方法。
- 如果插件是一个函数，它会被作为 install 方法。
- install 方法调用时，会将 Vue 作为参数传入。该方法需要在调用 new Vue() 之前被调用。
- 当 install 方法被同一个插件多次调用，插件将只会被安装一次。

### **v-model 原理**
VUE实现双向数据绑定的原理就是利用了 Object.defineProperty() 这个方法重新定义了对象获取属性值(get)和设置属性值(set)的操作，实现了数据劫持。
