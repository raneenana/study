# Vue实现数据驱动视图的核心原理
### 一 什么是数据驱动视图
- 数据驱动是vuejs最大的特点。在vuejs中，所谓的数据驱动就是当数据发生变化的时候，用户界面发生相应的变化，开发者不需要手动的去修改dom。
### 二 MVVM框架

Vuejs的数据驱动是通过MVVM这种框架来实现的。MVVM框架主要包含3个部分:model、view和 viewmodel。

- Model:指的是数据部分，对应到前端就是javascript对象

- View:指的是视图部分，对应前端就是dom

- Viewmodel:就是连接视图与数据的中间件