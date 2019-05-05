# Vue实现数据驱动视图的核心原理
### 一 什么是数据驱动视图
数据驱动是vuejs最大的特点。在vuejs中，所谓的数据驱动就是当数据发生变化的时候，用户界面发生相应的变化，开发者不需要手动的去修改dom。
### 二 MVVM框架

Vuejs的数据驱动是通过MVVM这种框架来实现的。MVVM框架主要包含3个部分:model、view和 viewmodel。

1， Model:指的是数据部分，对应到前端就是javascript对象

2， View:指的是视图部分，对应前端就是dom

3， Viewmodel:就是连接视图与数据的中间件  

注：数据(Model)和视图(View)是不能直接通讯的，而是需要通过ViewModel来实现双方的通讯。当数据变化的时候，viewModel能够监听到这种变化，并及时的通知view做出修改。同样的，当页面有事件触发时，viewMOdel也能够监听到事件，并通知model进行响应。Viewmodel就相当于一个观察者，监控着双方的动作，并及时通知对方进行相应的操作

# defineProperty
### 语法：
```
object.defineProperty（obj，prop，descriptor）
obj: 需要定义属性的对象
prop：需要定义或修改的属性名称
descript：将要被定义或修改的属性描述符
```
### 返回值：
被传递给函数的对象
### 属性
1， Writable 属性
当且仅当该属性的writable为true时，value才能被赋值运算符改变。默认为 false。  
  当writable属性设置为false时，该属性被称为“不可写”。它不能被重新分配。
```
var o = {}; // Creates a new object

Object.defineProperty(o, 'a', {
  value: 37,
  writable: false
});

console.log(o.a); // logs 37
o.a = 25; // No error thrown
// (it would throw in strict mode, even if the value had been the same)
console.log(o.a); // logs 37. The assignment didn't work.
```

2，configurable
当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。

3，enumerable
当且仅当该属性的enumerable为true时，该属性才能够出现在对象的枚举属性中。默认为 false。

4，value
该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。

5，get
一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是会传入this对象（由于继承关系，这里的this并不一定是定义该属性的对象）。
默认为 undefined。

6，一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。当属性值修改时，触发执行该方法。该方法将接受唯一参数，即该属性新的参数值。
默认为 undefined。
```
function Archiver() {
  var temperature = null;
  var archive = [];

  Object.defineProperty(this, 'temperature', {
    get: function() {
      console.log('get!');
      return temperature;
    },
    set: function(value) {
      temperature = value;
      archive.push({ val: temperature });
    }
  });

  this.getArchive = function() { return archive; };
}

var arc = new Archiver();
arc.temperature; // 'get!'
arc.temperature = 11;
arc.temperature = 13;
arc.getArchive(); // [{ val: 11 }, { val: 13 }]
```
### 继承属性
如果访问者的属性是被继承的，它的 get 和set 方法会在子对象的属性被访问或者修改时被调用。如果这些方法用一个变量存值，该值会被所有对象共享。