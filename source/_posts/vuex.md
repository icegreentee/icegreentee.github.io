---
title: vuex
date: 2019-10-18 18:22:00
categories:
- 前端
tags:
- vuex
---

# vuex

建立store.js

```vue
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    number:0,
  },
  mutations: {
    ADD(state){
      state.number++
    },
    SUB(state){
      state.number--
    }
  },
  actions: {

  }
})
```

在main.js中,将状态从根组件“注入”到每一个子组件中

```vue
new Vue({
  render: h => h(App),
  store
}).$mount('#app')

```

在子组件中可以通过$store.state.number进行调用

## state属性

类似与vue中data属性，用于存放属性，键值对。可以通过 mutations 和 actions 来改变state的值。使用this.$store.state.属性名称 来获取相应的值。

## getters属性

getters我们类比到vue中，那么它应该是 computed了 我们在使用的时候要使用 this.$store.getters.属性名   。用法也和computed类似，它实际上是调用一个方法，然后获取到的数据是经过一系列处理后并且return回来的数据。

##  mutations

类似与vue的methods。可以通过调用其中的函数来修改state的值。this.$store.commit('ADD')来调用mutations中的方法。

## actions属性

actions属性用法和mutations类似，但是actions我们是不可以修改state的 需要在actions通过commit来调用mutations来修改数据，那么action的意义何在呢？处理异步事件就要用action来做了呀。调用方法是，this.$store.dispatch("action的名字",参数)

actions 方法的第一个参数是context，类似与store实例，可以调用 `context.commit` 提交一个 mutation，或者通过 `context.state` 和 `context.getters` 来获取 state 和 getters。

常用法，获取context中的commit方法，提交commit调用mutations来修改数据

```js
actions: {
  increment ({ commit }) {
    commit('increment')
  }
}
```



综合示例

```
// store.js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    number:0,
  },
  mutations: {
    ADD(state){ 
      state.number++
    },
    SUB(state){
      state.number--
    },
    ADDPARAM(state,param){
      if (typeof param !== 'number'){
        param = 0
      }
      state.number = state.number + param
    } 
  },
  actions: {
    ASYNCADD(context,param){  //这里我们传入context上下文，里面包含 commit, state ,getters 这三个属性都可以通过context来调用到并且触发内部方法
      setTimeout(function(){
        context.commit('ADDPARAM',param)
      },1000)
    }
  },
  getters:{
    getNumber(state){   //getter的书写方法
      return state.number + 100
    }
  }
})
```



```
<!-- children.vue -->
<template>
  <div class="children">
    <h1>This is an children page</h1>
    <button @click="add">
      +
    </button>
      {{$store.state.number}}
      {{$store.getters.getNumber}}
      <button  @click="sub">
      -
    </button>
    

    <button @click="actAdd">action</button>
  </div>
</template>

<script>
  export default{
    name: 'children',
    methods: {
      add() {
```

## modules

Vuex 允许我们将 store 分割成**模块（module）**。每个模块拥有自己的 state、mutation、action、getter

```js
const moduleA = {
  state: { ... },
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: { ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})
```