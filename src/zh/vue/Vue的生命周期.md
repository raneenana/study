#  Vue的生命周期  
### beforeCreate
  在实例初始化之后，数据观测和event/watcher事件配置之前被调用

###  created
  再挂在开始之前被调用，相关的render函数首次被调用

### mounted
  el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内。
  这个钩子函数在渲染期间不会被调用

###  beforeUpdate
  数据更新时调用，发生在虚拟Dom打补丁之前服务器端渲染时不被调用，只有初次渲染会在服务端进行

### updated 
  由于数据更改而导致虚拟DOM重新渲染的时候调用该函数  
  当这个函数调用的时候，组件DOM已经更新所以可以执行依赖于DOM的操作

###  activated
  keep-alive组件激活时调用

###  deactivated 
  keep-alive组件停用时调用

### beforeDestroy
  实例销毁前调用

### destroyed
  Vue实例销毁后调用，调用后Vue实例所指示的东西都会解除绑定，所有事件监听都会被销毁，所有的子实例也会被销毁

### errorCaptured
  当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。

### 生命周期图示
![Alt text](../../.vuepress/public/lifecycle.png)