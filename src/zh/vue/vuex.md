# Vuex
##### 1、什么是vuex？
- 每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。

##### 2、初始化vuex
（1）下载vuex

```
cnpm i vuex -D
```


（2）建一个store文件夹（store/index.js）

```
// 初始化vuex

import Vue from 'vue';
import Vuex from 'vuex';

// 引入module
import app from './module/app';

Vue.use(Vuex);

// 生成一个vuex实例
export default new Vuex.Store({
  modules: {
    app
  }
})
```
（3）在store文件夹里建一个module文件夹用来存放数据（store/module/app.js）

```
// 存放数据的地方
const state = {
  num: 100
}

// 派生数据（很少用）
const getters = {
    doubleNum(state){
        return state.num*2
    }
}

// 同步改变
const mutations = {
  changeNum(state, payload){
    state.num = payload;
  }
}

// 异步改变
// action提交的是mutation，而不是直接更变状态。
// action可以包含任意异步操作。
const actions = {  
<!-- 分发action：
	应用场景：当一次action对应的数据的更改，必须依赖另外一个action中的数据更改时，必须在本此action中先去触发另外一个action操作；
    另外一个action可能为同步，也可能为异步，如果为异步需要借助promise或者async函数； -->
    <!--changeNumAsync(context, payload){-->
        
    <!--}-->
    changeNumAsync({commit}, payload){
        commit('changeNum', payload)
    }
}

export default {
  // 命名空间
  namespaced: true, // 配合module使用
  state,
  actions,
  getters,
  mutations
}
```
（4）在main.js里面引入store

```
import Vue from 'vue'
import App from './App.vue'

import store from './store'

new Vue({
  el: '#app',
  store,
  render: h => h(App)
})

```
（5）辅助函数

```
mapState辅助函数
写法：
对象写法：
computed：mapState({
//写法一：箭头函数可使代码更简洁
	count:state=> state.count 
//写法二：传字符串参数 'count' 等同于 `state => state.count`
	count:state=> state.count 
	
//写法三：为了能够使用 `this` 获取局部状态，必须使用常规函数
	count(state){ 
return state.count+this.a 

	}
})
数组写法：
当映射的计算属性的名称与 state 的子节点名称相同时
computed:mapState([
	“count”
])

mapActions辅助函数
在组件中分发action:
methods: {
    ...mapActions([
      'increment' // 映射 this.increment() 为 this.$store.dispatch('increment')
    ]),
    ...mapActions({
      add: 'increment' // 映射 this.add() 为 this.$store.dispatch('increment')
    })
  }
```

（6）在页面中使用
```
<template>
  <div>
    <button @click="changeNum('+')">+</button>
    <span>{{num}}</span>
    <button @click="changeNum('-')">-</button>
  </div>
</template>
<script>
  export default {
    name: 'app',
    computed: {
      num() {
        return this.$store.state.app.num
      }
    },
    methods: {
      changeNum(type) {
        if (type == '+') {
          // this.$store.commit('changeNum', this.num+1)
          this.$store.dispatch('changeNumAsync', this.num+1)
        } else {
          this.$store.commit('changeNum', this.num-1)
        }
      }
    },
    mounted(){
      console.log(this.$store)
    }
  }
</script>

```

