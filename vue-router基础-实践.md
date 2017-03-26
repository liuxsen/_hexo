---
title: vue-router基础+实践
date: 2017-03-03 15:52:45
tags: vue
---

> 可以使用npm直接安装插件
```
npm install vue-router --save
```

执行命令完成vue-router的安装，并在package.json中添加了vue-router的依赖。

```
"dependencies": {
   ...
   "vue-router": "^2.1.0"
   ...
 }
 ```


> 如果是要安装在开发环境下，则使用以下命令行：


```
npm install vue-router --save-dev

"devDependencies": {
  ...
  "vue-router": "^2.1.0",
  ...
}
```

```
直接下载/CDN
https://unpkg.com/vue-router/dist/vue-router.js
 <script src="/path/to/vue.js"></script>
 <script src="/path/to/vue-router.js"></script>
```


## 路由实现


**一个最简单的单页面应用**
```js
//app.js
import Vue from 'vue'
import App from './App'
import VueRouter from 'vue-router'
import Page01 from './components/page01'
import Page02 from './components/page02'

Vue.use(VueRouter) // 全局安装路由功能

// 定义路径
const routes = [
  { path: '/', component: Page01 },
  { path: '/02', component: Page02 },
]
// 创建路由对象
const router = new VueRouter({
  routes
})
new Vue({
  el: '#app',
  template: '<App/>',
  components: { App },
  router
})
App.vue
<template>
  <div id="app">
    <router-link to="/">01</router-link>
    <router-link to="/02">02</router-link>
    <br/>
    <router-view></router-view>
  </div>
</template>
page01.vue
<template>
  <div>
    <h1>page01</h1>
  </div>
</template>
page02.vue
<template>
  <div>
    <h1>page02</h1>
  </div>
</template>
```


1. npm安装vue-router
2. Vue.use(VueRouter)全局安装路由功能
3. 定义路径数组routes并创建路由对象router
4. 将路由注入到Vue对象中
5. 在根组件中使用<router-link>定义跳转路径
6. 在根组件中使用<router-view>来渲染组件
7. 创建子组件

**路由的跳转**

#### router-link

router-link标签用于页面的跳转

```html
<router-link to="/page01">page01</router-link>
```
点击router-link标签router-view就会渲染路径为/page01的页面。

**router.push**

**通过JS代码控制路由的界面渲染**

````js
// 字符串 字符串为路径
router.push('home')
// 对象 
router.push({ path: 'home' })
// 命名的路由
router.push({ name: 'user', params: { userId: 123 }})
// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
实例中的语法：
// 字符串
this.$router.push('home')
// 对象
this.$router.push({ path: 'home' })
// 命名的路由
this.$router.push({ name: 'user', params: { userId: 123 }})
// 带查询参数，变成 /register?plan=private
this.$router.push({ path: 'register', query: { plan: 'private' }})

//router.replace
//push方法会向 history 栈添加一个新的记录，而replace方法是替换当前的页面，不会向 history 栈添加一个新的记录。
<router-link to="/05" replace>05</router-link>
this.$router.replace({ path: '/05' })

//router.go
//控制history记录的前进和后退
// 在浏览器记录中前进一步，等同于 history.forward()
this.$router.go(1)
// 后退一步记录，等同于 history.back()
this.$router.go(-1)
// 前进3步记录router.go(3)
this.$router.go(3)
//传参方式
//由跳转的过程中会传递一个object，我们可以通过watch方法查看路由信息对象。
watch: {
  '$route' (to, from) {
      console.log(to);
      console.log(from);
  },
}
控制台看到的路由信息对象
{
  ...
  params: { id: '123' },
  query: { name: 'jack' },
  ...
}
params
路由配置文件中定义参数
{
  // 订单详情
  path: '/order/detail/:orderId',
  name: 'orderDetail',
  component: OrderDetailView
}
路径后面的/:orderId就是我们要传递的参数
this.$router.push({ path: '/order/detail/441'});
此时路由跳转的地址
//http://localhost:3000/#/order/detail/441
组件中获取数据
<h2>{{ $route.params.orderId }}</h2>
console.log(this.$route.params.orderId)
//query
//query传递数据的方式就是URL常见的查询参数

<router-link :to="{ path: '/order/detail', query: { id: item.id, stateId: item.stateId }}">

this.$router.push({path: '/order/detail', query: {id: orderIdCache}});
///获取数据和params是一样
<h2>{{ $route.query.orderId }}</h2>
console.log(this.$route.query.orderId)
```