# Vue

## 基础

### 安装

- **不支持** IE8 及以下版本

- 更新日志

  https://github.com/vuejs/vue/releases

- 安装方式有多种：

  + `<script>` 标签引入

  + 通过 `npm` 安装

    ```shell
    # 默认安装最新稳定版
    $ npm install vue
    ```

  + 其它方式详见官网：

    https://cn.vuejs.org/v2/guide/installation.html

### 介绍

#### 是什么

- 可以轻松构建 SPA（Single Page Application） 应用程序
- 通过 **指令** 扩展了 HTML，通过 **表达式** 绑定数据到 HTML
- **最大程度上解放了 DOM 操作**

#### Vue 特点

- MVVM

  + Model

  + View

  + ViewModel

    ! [MVVM 图示](./images/MVVM.png)

- 数据驱动视图（data driven view）

- 面向数据

- 组件化

  + 组件由 HTML、CSS、JavaScript 构成

#### Vue 的优缺点

- 上手简单
- 简洁的 API
- 轻量高效
- 灵活的组件系统
- 强大的生态系统
  + Vue Router
  + Vuex
- 开源

#### 可以做什么

- 一切和 Web 用户界面相关的都可以使用 Vue 来做
- 对 SEO 没要求的应用
- 更加侧重于 SPA 应用的程序
- 单产品型的应用程序
- 桌面应用程序
- 管理系统
- 混合 APP
- 移动 APP

#### 发展历史

​	https://github.com/vuejs/vue/releases

- Vue.js 由尤雨溪个人正式发布于 2014 年 2 月，并开源于 Github
- 2015 年 10 月 27 日，正式发布 1.0
- 2016 年 8 月 1 日，正式发布 2.0
- 目前 Vue 2.0 最新版本为 2.6.11

#### 对比其他框架

​	https://cn.vuejs.org/v2/guide/comparison.html

### Vue 实例

- 创建实例

- 实例选项
  + el 挂载元素
  + data 数据
  + methods 方法
  + 生命周期钩子（详见后面生命周期钩子）
  + ...
  
- 实例数据 data
  + 响应式数据
  + 注意事项：
    * 只有 data 里被代理的属性是响应的，也就是说，值的任何改变都会触发视图的重新渲染
    * 如果实例创建之后添加新的属性到实例上，它不会触发视图更新
    * 也就是说，视图需要的数据必须在初始化实例时就定义，否则 vue 会发出警告
  
- 实例方法 methods
  + methods 中的方法不能使用箭头函数，否则绑定的是 window
  + 不能与属性同名
  + 事件绑定不需要调用，传参需要调用
  + ES6 为对象成员提供了一种简写的方法：
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>Document</title>
    </head>
    <body>
      <div id="app">
        <h1>{{ message }}</h1>
        <button @click="handleClick">Click</button>
      </div>
      <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
      <script>
        const app = new Vue({
        data: {
          message: 'Hello World!'
        },
        methods: {
          // handleClick () {}  <=>  handleClick: function() {}  （前者是后者的简写）
          handleClick () {
            console.log('hello vue.js!')
          }
        },
        // 生命周期钩子
        beforeCreate () {
          console.log('beforeCreate')
        },
        created () {
          console.log('created')
        },
        beforeMount () {
          console.log('beforeMount')
        },
        mounted () {
          console.log('mounted')
        },
        beforeUpdate () {
          console.log('beforeUpdate')
        },
        updated () {
          console.log('updated')
        },
        activated () {
          console.log('activated')
        },
        deactivated () {
          console.log('deactivated')
        },
        beforeDestroy () {
          console.log('beforeDestroy')
        },
        destroyed () {
          console.log('destroyed')
        },
        errorCaptured () {
          console.log('errorCaptured')
        },
        }).$mount('#app')
      </script>
    </body>
  </html>
  ```

### 数据绑定

### 指令



